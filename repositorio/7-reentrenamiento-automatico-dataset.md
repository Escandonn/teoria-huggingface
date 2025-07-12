

---

# 🔁 Guía: Configurar un sistema automático para reentrenar un modelo cuando cambie un dataset

¡Los **Webhooks** ya están disponibles públicamente!
Con esta guía aprenderás a configurar un **pipeline automático de entrenamiento** en la plataforma de Hugging Face usando:

* **Datasets del Hub**
* **Webhooks**
* **Spaces**
* **AutoTrain**

### 🎯 Objetivo:

Crear un Webhook que escuche cambios en un dataset de clasificación de imágenes y dispare un fine-tuning automático del modelo `microsoft/resnet-50` usando AutoTrain.

---

## ✅ Prerrequisito: Subir tu dataset al Hub

Para este ejemplo, usaremos un dataset de **clasificación de imágenes**.
Aprende cómo subir tu dataset al Hub aquí:
👉 [Documentación oficial sobre datasets](https://huggingface.co/docs/hub/datasets-upload)

---

## 🔔 Crear un Webhook para reaccionar a los cambios del dataset

1. Ve a los **ajustes (Settings)** de tu dataset en el Hub.
2. Crea un **Webhook**.

Configura lo siguiente:

* Selecciona tu dataset como repositorio objetivo.
  Ejemplo: `huggingface-projects/input-dataset`
* Ingresa una **URL falsa o temporal** por ahora (luego la actualizaremos).
* Ingresa una **clave secreta** para mayor seguridad.
* Suscríbete al evento **"Repo update"** para reaccionar a cambios en el contenido.

🖼️ Resultado: tu webhook debería verse así:

> **🔒 Importante:** Guarda la clave secreta, ya que deberás usarla en el Space.

---

## 🧠 Crear un Space que reciba los eventos del Webhook

Necesitamos una forma de recibir los eventos del webhook.
Lo más fácil es crear un **Space** que actúe como servidor.

### Ejemplo de Space:

Encuentra un ejemplo aquí 👉 [Space con Webhook Listener](https://huggingface.co/spaces/huggingface-projects/webhook-listener)

Este Space usa:

* **Docker**
* **FastAPI**
* **Python**
* **uvicorn**

📁 El archivo principal es `src/main.py`.

---

## ⚙️ ¿Qué hace el Space?

1. Inicia una **API HTTP con FastAPI** que escucha en la ruta `/webhook`:

```python
from fastapi import FastAPI
app = FastAPI()

@app.post("/webhook")
async def post_webhook(...):
```

2. Verifica la **cabecera `X-Webhook-Secret`** para asegurar que la petición es válida:

```python
WEBHOOK_SECRET = os.getenv("WEBHOOK_SECRET")

if x_webhook_secret != WEBHOOK_SECRET:
	raise HTTPException(403)
```

3. Parsea el **payload JSON** del evento usando Pydantic:

```python
class WebhookPayload(BaseModel):
	event: WebhookPayloadEvent
	repo: WebhookPayloadRepo
```

El Webhook solo procesará eventos si:

* El evento es de tipo `"update"`.
* El `scope` comienza con `repo.content`.
* El repo es de tipo `dataset`.
* El nombre del dataset coincide con `input_dataset` en tu configuración.

---

## 🤖 Automatizar el reentrenamiento con AutoTrain

Si el evento es válido:

* Se **crea un proyecto AutoTrain**.
* Se **agrega el dataset**.
* Se **inicia el procesamiento**.
* Se publica una **notificación en la pestaña “Community”** del dataset.

```python
def schedule_retrain(payload: WebhookPayload):
	project = AutoTrain.create_project(payload)
	AutoTrain.add_data(project_id=project["id"])
	AutoTrain.start_processing(project_id=project["id"])
	notify_success(project["id"])
```

---

## 🔐 Variables de entorno necesarias

Debes agregar dos secretos en los **ajustes de tu Space**:

* `WEBHOOK_SECRET`: La misma clave definida en el Webhook.
* `HF_ACCESS_TOKEN`: Token de acceso con permisos de escritura.

Puedes crear el token en [tus ajustes de cuenta](https://huggingface.co/settings/tokens).

---

## 🛠️ Configura tu archivo `config.json`

Modifica `config.json` con los valores adecuados:

```json
{
  "target_namespace": "tu-usuario-o-org",
  "input_dataset": "nombre-del-dataset",
  "input_model": "modelo-base-a-reentrenar",
  "autotrain_project_prefix": "prefijo-del-proyecto"
}
```

---

## 🌐 Conecta tu Webhook al Space

1. Abre tu Space.
2. Haz clic en **“Embed this Space”**.
3. Copia la **URL directa**.

🔗 Luego, vuelve a los ajustes del Webhook y reemplaza la URL temporal por esta URL directa del Space.

Claro, aquí tienes un resumen solo con las **problemáticas**:

---

1. **Clasificador de imágenes desactualizado:**
   El modelo no reconoce nuevas categorías o productos subidos en una tienda online.

2. **Análisis de sentimientos anticuado:**
   El modelo no interpreta correctamente nuevas expresiones o formas de hablar en reseñas.

3. **Diagnóstico médico inexacto:**
   El sistema no detecta nuevas patologías o variaciones en imágenes médicas recientes.

4. **Corrección automática limitada:**
   El modelo no comprende nuevos patrones de respuestas de estudiantes.

5. **Detector de noticias falsas obsoleto:**
   El clasificador no identifica nuevas técnicas de desinformación.

---

---