
---

## 🔁 Pull Requests y Discusiones en Hugging Face Hub

En el Hub, los **Pull Requests (PR)** y las **Discusiones** permiten que la comunidad colabore con los repositorios, ya sean de modelos, datasets o Spaces.

A diferencia de otras plataformas como GitHub, Hugging Face simplifica el proceso para que esté optimizado para el flujo de trabajo en ML:

### ✅ ¿Qué los hace diferentes?

* No se usan *forks*: los colaboradores escriben directamente en una rama especial dentro del mismo repositorio.
* No hay una diferencia rígida entre discusión y PR: ambos se muestran en el mismo lugar.
* Diseñado específicamente para repositorios de **modelos**, **datasets** y **Spaces**.

📌 Puedes habilitar o deshabilitar las *Discusiones y PRs* desde la pestaña **Settings** del repositorio.

---

## 📃 Ver lista de PRs y Discusiones

1. Ve a la pestaña **Community** dentro de cualquier repositorio.
2. Allí verás todas las **Discusiones y PRs** activos o cerrados.
3. Puedes aplicar filtros para ver solo los que estén **abiertos**.

---

## 👀 Visualizar una Discusión o Pull Request

* Dentro de una discusión, puedes leer los comentarios de todos los participantes.
* Si es un **Pull Request**, verás una pestaña llamada **Files changed** donde se muestran todos los archivos modificados.

---

## 📝 Editar el título de una Discusión o PR

Puedes editar el título si:

* Eres el autor de la PR o discusión.
* Tienes permisos de **escritura** o eres propietario del repositorio.

Haz clic en el ✏️ ícono para cambiar el título.

---

## 📌 Fijar una Discusión o Pull Request

Si tienes permisos de escritura, puedes **fijar** cualquier PR o discusión.
🧷 Las discusiones fijadas aparecerán al principio de la lista para mayor visibilidad.

---

## 🔒 Bloquear una Discusión o PR

También puedes **bloquear** discusiones o PRs. Esto:

* Impide que se agreguen nuevos comentarios.
* Mantiene visibles los comentarios anteriores.

---

## ✏️ Edición de comentarios y moderación

Si escribiste un comentario o tienes permisos de escritura:

* Haz clic en el menú contextual (tres puntos) en la esquina superior derecha de tu comentario.
* Allí podrás **editar** el comentario.

Al editarlo:

* Se mostrará un enlace arriba del comentario que lleva al **historial de ediciones**.

También puedes **ocultar un comentario**, pero esto es **irreversible**:
Nadie podrá ver ni modificar el contenido oculto nunca más.

👉 Consulta la sección de **moderación** para saber cómo **reportar comentarios abusivos**.

---

## 🧮 ¿Puedo usar Markdown y LaTeX?

¡Sí! Puedes dar formato a tus comentarios con **Markdown** y escribir fórmulas matemáticas con **LaTeX**.

### Sintaxis para fórmulas:

* `$$ ... $$` para fórmulas en bloque (centradas).
* `\\(...\\)` para fórmulas **en línea**.

Ejemplo:

```markdown
La fórmula de Euler es: \\( e^{i\\pi} + 1 = 0 \\)
```

---

## 💻 ¿Cómo gestionar Pull Requests desde la terminal?

Supongamos que el número de tu Pull Request es `42`.

### 🔽 Clonar el PR en tu equipo:

```bash
git fetch origin refs/pr/42:pr/42
git checkout pr/42
```

🔧 Haz los cambios que desees, y luego:

```bash
git add .
git commit -m "Añado mis cambios"
git push origin pr/42:refs/pr/42
```

---

## 📝 Modo Borrador (Draft mode)

Cuando creas un PR desde “Advanced mode”, por defecto se abrirá en modo **Borrador**.

Esto significa que:

* Los demás verán que estás trabajando en ese PR.
* **No se puede fusionar** (mergear) mientras esté en borrador.

Cuando lo tengas listo, simplemente pulsa el botón **“Publish”** y pasará a estado **Open**.
🔒 *Una vez publicado, no puedes volver a borrador.*

---

## 🧙‍♂️ Para usuarios avanzados: ver todos los PRs con Git

Si eres un experto en Git, puedes traer **todos los PRs** del repositorio localmente modificando tu `refspec`.

### Paso 1: traer todos los PRs

```bash
git fetch origin refs/pr/*:refs/remotes/origin/pr/*
```

### Paso 2: acceder a un PR específico

```bash
git checkout pr/42
```

### Paso 3: subir cambios a ese PR

```bash
git push origin pr/42:refs/pr/42
```

---

¿Quieres que te muestre un ejemplo completo de cómo crear un Pull Request de prueba en Hugging Face desde cero usando terminal y web?
