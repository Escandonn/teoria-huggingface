## 🚀 Empezando con Repositorios en Hugging Face

Esta guía para principiantes te enseñará las habilidades básicas que necesitas para **crear y administrar un repositorio** en el Hub de Hugging Face. Cada sección se basa en la anterior, pero si ya tienes experiencia puedes saltar al punto que necesites.

---

### 📋 Requisitos previos

🔹 Si solo usarás la **interfaz web** del Hub, **¡no necesitas instalar nada!**
🔹 Si prefieres trabajar desde la **terminal**, necesitarás:

1. Tener instalado **Git** en tu sistema:
   👉 [Instalar Git](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Instalando-Git)

2. Instalar **Git LFS (Large File Storage)** para manejar archivos grandes (como pesos de modelos e imágenes):
   👉 [Instalar Git LFS](https://git-lfs.github.com/)

3. Instalar la herramienta de línea de comandos de Hugging Face:

   ```bash
   python -m pip install huggingface_hub
   huggingface-cli login
   ```

   Esto te permitirá autenticarte y subir archivos desde la terminal.

---

## 🏗️ Crear un Repositorio

Puedes hacerlo fácilmente desde la web:

1. Visita 👉 [https://huggingface.co/new](https://huggingface.co/new)

2. Completa la información:

   * **Propietario del repositorio**: puede ser tu cuenta personal o una organización a la que pertenezcas.
   * **Nombre del modelo**: este será el nombre del repositorio.
   * **Visibilidad**: elige si quieres que sea **público** o **privado**.
   * **Licencia**: puedes dejarlo en blanco por ahora. Más info: [Licencias en Hugging Face](https://huggingface.co/docs/hub/licenses).

3. Una vez creado, verás una página como esta:

   ![Modelo creado](https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/hub/model_repo_created.png)

4. Se te pedirá crear una **Model Card** (opcional en este momento si solo estás probando).

---

## 📂 Agregar archivos a un repositorio

### 🔸 Desde la Web

1. Haz clic en la pestaña **Files**.
2. Pulsa **Add file**.
3. Elige una de estas dos opciones:

#### ➕ Crear un nuevo archivo

Te abrirá un editor donde puedes:

* Escribir el nombre del archivo.
* Agregar contenido.
* Guardar el archivo con un mensaje de commit.
* ✅ Opcional: puedes marcar **"Open as a pull request"** para abrir un PR en vez de subir directamente al repositorio.

#### 📤 Subir un archivo desde tu equipo

Selecciona el archivo local y escribe un mensaje de commit.
También puedes abrirlo como Pull Request si lo deseas.

---

### 🔸 Desde la Terminal (usando Git)

#### 📥 Clonar el repositorio

```bash
git clone https://huggingface.co/<tu-usuario>/<nombre-del-modelo>
cd <nombre-del-modelo>
```

O si es un dataset:

```bash
git clone https://huggingface.co/datasets/<tu-usuario>/<nombre-del-dataset>
cd <nombre-del-dataset>
```

También puedes usar **SSH** (recomendado si quieres evitar tener que escribir tu contraseña cada vez):

```bash
git clone git@hf.co:<tu-usuario>/<nombre-del-modelo>
cd <nombre-del-modelo>
```

💡 **Nota:** Debes haber agregado tu **clave pública SSH** en los ajustes de tu cuenta de Hugging Face para hacer push con SSH.

---

### 🧰 Configuración para archivos grandes

Si vas a manejar archivos mayores a 10 MB (como modelos entrenados), necesitas activar Git LFS:

```bash
git lfs install
```

Si alguno de tus archivos supera los 5 GB, también ejecuta:

```bash
huggingface-cli lfs-enable-largefiles .
```

💡 Hugging Face agrega automáticamente reglas para archivos grandes en el archivo `.gitattributes`, pero si usas tipos de archivos no comunes, puedes añadirlos así:

```bash
git lfs track "*.mi_extension"
```

---

## ⬆️ Subir archivos al repositorio (push)

1. **Agrega tus archivos al repositorio local.**
2. Luego ejecuta:

```bash
git add .
git commit -m "Primera versión del modelo"
git push
```

✅ ¡Listo! Ahora puedes ver tu repositorio actualizado en Hugging Face.

---

## 🕓 Ver historial de cambios

Cada vez que haces un ciclo `add → commit → push`, Git guarda una nueva versión (commit).

Puedes ver el historial así:

1. En la página del repositorio, haz clic en **"History: X commits"**.
2. Haz clic en cualquier commit para ver exactamente qué cambios fueron hechos.

---

## 📌 Tips adicionales

* Si usas HTTP en vez de SSH, es probable que se te pida usuario/contraseña cada vez que haces `push`.
* Para evitar eso:

  * Usa **SSH**.
  * O configura un *credential helper* de Git para guardar tu acceso.

---

## 🎥 ¿Prefieres aprender en video?

Esta guía también está disponible en formato visual en la documentación oficial.

---

¿Quieres que te ayude a crear un repositorio real paso a paso con archivos de ejemplo (como un modelo o dataset)?
