## 🔜 Próximos pasos

Las siguientes secciones resaltan funciones e información adicional que puedes encontrar útil para **aprovechar al máximo los repositorios Git** en el Hugging Face Hub.

---

### 🤖 Cómo gestionar repositorios programáticamente

Hugging Face permite acceder a los repositorios usando **Python** mediante la librería [`huggingface_hub`](https://github.com/huggingface/huggingface_hub). Las operaciones que ya exploramos, como descargar repositorios y subir archivos, están disponibles en esta librería, junto con muchas otras funciones útiles.

Si prefieres usar Git directamente, revisa las siguientes secciones.

---

### 📚 Aprendiendo más sobre Git

Un buen punto de partida para seguir aprendiendo sobre Git es este [tutorial de Git](https://git-scm.com/docs/gittutorial). Si quieres una explicación más profunda, puedes revisar las [guías de Git en GitHub](https://guides.github.com/introduction/git-guide/).

---

### 🌿 Cómo usar ramas (branches)

Para trabajar de forma colaborativa y desarrollar nuevas funciones sin afectar el código en producción, puedes usar **ramas**. Estas te permiten separar el código “en progreso” del código “listo para producción”, y además, permiten que varias personas trabajen sin conflictos frecuentes.

También puedes usar ramas para hacer pruebas experimentales, y definir buenas prácticas de gestión de ramas para todo tu equipo.

📘 Aprende sobre ramas en este [tutorial interactivo de Learn Git Branching](https://learngitbranching.js.org/).

---

### 🔖 Usar etiquetas (tags)

Git permite etiquetar commits para marcar hitos importantes en tu proyecto. Puedes usar etiquetas en tus repositorios del Hub para:

* Identificar versiones importantes del proyecto
* Realizar pruebas A/B
* Clonar un repositorio en un punto específico del tiempo

El cliente de `huggingface_hub` también admite descargar archivos desde un commit etiquetado.

📘 Aprende más en esta [entrada de DevConnected sobre etiquetas](https://devconnected.com/how-to-create-git-tags/).

---

### 🌀 Cómo duplicar o bifurcar un repositorio (incluyendo archivos LFS)

Si deseas copiar un repositorio, existen dos opciones dependiendo de si quieres **conservar el historial de Git**:

---

#### 🔁 Duplicar **sin historial de Git**

En muchos casos, si solo quieres tu propia copia del código, **no necesitas el historial**. Puedes duplicarlo fácilmente usando la herramienta **Repo Duplicator**:

* Necesitarás generar un **token de acceso de usuario**
* Puedes leer más al respecto en la [documentación de seguridad](https://huggingface.co/docs/hub/security).

---

#### 🌿 Duplicar **con historial (Fork)**

Un fork es una copia completa del repositorio incluyendo su historial de commits. Puedes bifurcar tus propios repositorios o los de otros para experimentar con ellos.

🔧 Nota: Necesitarás instalar:

* Git LFS
* CLI de Hugging Face (`huggingface-cli`)

⚠️ No puedes usar `git clone` o `git fork` de forma tradicional si el repo tiene archivos LFS. Necesitas manejar correctamente los punteros de LFS para evitar errores.

El proceso puede tardar dependiendo de tu ancho de banda, ya que implica **descargar y volver a subir los archivos LFS**.

---

### Ejemplo práctico: Fork manual de un repo

Supongamos que tienes un repo llamado `upstream` y creaste un nuevo repositorio `myfork` en Hugging Face.

#### 1. Crea el repositorio destino (ej. `myfork`) en

👉 [https://huggingface.co](https://huggingface.co)

#### 2. Clona tu nuevo fork:

```bash
git clone git@hf.co:me/myfork
```

#### 3. Descarga archivos pequeños (no-LFS):

```bash
cd myfork
git lfs install --skip-smudge --local
git remote add upstream git@hf.co:friend/upstream
git fetch upstream
```

#### 4. Descarga archivos grandes (LFS):

```bash
git lfs fetch --all upstream
```

⏳ Esto puede tardar según tu velocidad de descarga.

#### 5a. Para sobrescribir completamente el historial:

```bash
git reset --hard upstream/main
```

#### 5b. Para hacer un rebase del historial:

```bash
git rebase upstream/main
```

Resuelve los conflictos si aparecen.

---

#### 6. Prepara los archivos LFS para subirlos:

```bash
git lfs install --force --local
huggingface-cli lfs-enable-largefiles .
```

#### 7. Finalmente, sube tu fork:

```bash
git push --force origin main
```

⏫ Esto puede tardar según tu velocidad de subida.

¡Listo! Ahora tienes **tu propio fork** o **repo rebased** en el Hub 🎉

---

¿Deseas que también te cree un **script automatizado en Python para duplicar y mantener sincronizado un repo de Hugging Face con LFS**, por ejemplo, para backups o training distribuidos?
