### Notebooks de Jupyter en Hugging Face Hub

Los notebooks de Jupyter son un formato muy popular para compartir código y análisis de datos en el ámbito del aprendizaje automático y la ciencia de datos. Son documentos interactivos que pueden contener código, visualizaciones y texto.

---

### Abrir modelos en Google Colab y Kaggle

Cuando visitas la página de un modelo en el Hugging Face Hub, verás un nuevo botón “Google Colab” o “Kaggle” dentro del menú desplegable **“Usar este modelo”**. Al hacer clic, se genera un notebook listo para ejecutarse, con el código básico para cargar y probar el modelo.
Esto es ideal para hacer prototipos rápidos, pruebas de inferencia o experimentos de fine-tuning — todo desde el navegador.

> **Opción de Google Colab y Kaggle para modelos en el Hub**

También puedes acceder directamente al notebook listo para usar agregando `/colab` o `/kaggle` a la URL del modelo.

**Ejemplo**:
Modelo Gemma 3 4B IT:
🔗 Modelo: `https://huggingface.co/google/gemma-3-4b-it`
🔗 Colab: `https://huggingface.co/google/gemma-3-4b-it/colab`
🔗 Kaggle: `https://huggingface.co/google/gemma-3-4b-it/kaggle`

> Si un repositorio del modelo contiene un archivo llamado `notebook.ipynb`, se usará este archivo personalizado para Colab y Kaggle en lugar del notebook autogenerado.
> Esto permite a los autores ofrecer ejemplos más detallados o avanzados, manteniendo la integración de un solo clic.
> Ejemplo: [`NousResearch/Genstruct-7B`](https://huggingface.co/NousResearch/Genstruct-7B)

---

### Visualización de notebooks en el Hub

Los archivos de notebook de Jupyter (normalmente con extensión `.ipynb`) son archivos JSON. Aunque pueden abrirse como texto, no están diseñados para ser leídos por humanos directamente.

El Hub tiene soporte para **renderizar notebooks**, es decir, mostrarlos de forma legible y visual.
Esto se aplica a notebooks dentro de cualquier tipo de repositorio en el Hub: **modelos, datasets y Spaces.**

---

### Abrir en Google Colab

**Google Colab** es un entorno gratuito de notebooks Jupyter que no requiere instalación y funciona completamente en la nube.
Los notebooks alojados en el Hub tienen un botón **“Abrir en Colab”** que permite ejecutarlos en Colab con un solo clic. Ideal para ejecutar pruebas sin tener que configurar nada localmente.
