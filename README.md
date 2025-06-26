# ☁️ Laboratorio Cloud 1 | LemonCode

URL del despliegue: [https://sergio-jc.github.io/cloud-lab-1/](https://sergio-jc.github.io/cloud-lab-1/)

![image](https://github.com/user-attachments/assets/e2e0a1cd-b8d9-4ca3-ae3c-0520aa959480)

## 📖 Overview

Este laboratorio tiene como objetivo desplegar una aplicación estática en **GitHub Pages** de forma manual. Para este ejercicio, se ha utilizado **Astro** como generador de sitios estáticos. 

---

### 📌 Creación del proyecto

Se creó un pequeño proyecto con **Astro** configurado en su modo estático. Para este entorno se desarrolló una plantilla HTML sencilla con algunos estilos básicos, a modo de ejemplo.

```bash
npm create astro@latest
```

### 📌 Validación de la build

Para asegurarme de que el proyecto se generaba correctamente, ejecuté:

```
npm run build
```

Esto generó la carpeta `dist/` con los archivos estáticos necesarios para usar en Github Pages.

### 📌 Creación de la rama `gh-pages`

Una vez obtenemos los ficheros estáticos de la carpeta `/dist` tenemos que subirlos en un rama llamada `gh-pages` para que se inicie el proceso automático de Github Pages para el despliegue de nuestro sitio web.

```bash
git switch -c "gh-pages"
```
El anterior comando crea y te muve a la rama `gh-pages` donde tendrás que soltar todos los archivos de la carpeta `/dist`.

### 📌 Despliegue automático

Para el proceso de desplique simplemente tenemos que publicar la rama con nuestros cambios y se dispararán varios procesos automáticamente que podrás monitorear en la tab Actions de tu repositorio.

![image](https://github.com/user-attachments/assets/f4b8c2d6-05a3-401c-8f9e-52b932d9dc36)

Al finalizar estos procesos obtendrás el URL del despliegue: [https://sergio-jc.github.io/cloud-lab-1/](https://sergio-jc.github.io/cloud-lab-1/)
