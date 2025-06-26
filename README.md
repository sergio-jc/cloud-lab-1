# ☁️ Laboratorio Cloud | LemonCode

URL del despliegue: [https://sergio-jc.github.io/cloud-lab/](https://sergio-jc.github.io/cloud-lab/)

![image](https://github.com/user-attachments/assets/a2c0fb47-b90b-478b-8e0c-9037db098169)


## 📖 Overview

Este laboratorio tiene como objetivo desplegar una aplicación estática en **GitHub Pages** y posteriormente automatizar este proceso utilizando **GitHub Actions**. Para este ejercicio, se ha utilizado **Astro** como generador de sitios estáticos y se han seguido dos fases bien diferenciadas:  

1. **Deploy manual** utilizando el paquete `gh-pages`.
2. **Automatización del deploy** con un workflow de **GitHub Actions**.

---

## 📦 Fase 1: Deploy manual con `gh-pages`

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

Esto generó la carpeta `dist/` con los archivos estáticos listos para publicar.

### 📌 Instalación de gh-pages

Se instaló el paquete gh-pages para facilitar el despliegue manual de la carpeta `dist/` en la rama gh-pages del repositorio.

```bash
npm install --save-dev gh-pages
```

### 📌 Configuración del script de despliegue

Se añadió el siguiente script en el package.json:

```
"scripts": {
  "deploy": "gh-pages -d dist"
}
```

### 📌 Publicación manual

Finalmente, se ejecutó el despliegue manual con:

```bash
npm run deploy
```

Esto creó automáticamente la rama gh-pages y publicó el sitio estático en GitHub Pages.

---

## ⚙️ Fase 2: Automatización del deploy con GitHub Actions

### 📌 Habilitación de GitHub Pages desde Actions

Antes de configurar la automatización, se habilitó la opción GitHub Actions en la sección Settings > Pages del repositorio, seleccionando el entorno de despliegue correspondiente.

![image](https://github.com/user-attachments/assets/1ecc3ebb-4369-41f6-95e0-7aad3e5ccb27)


### 📌 Creación del workflow

Se creó la carpeta `.github/workflows` y dentro de ella, el archivo `cd.yaml`.

### 📌 Estructura del workflow

El workflow se configuró para ejecutarse en cada push a la rama main.

```yml
name: CD to GH Pages

on:
  push:
    branches:
      - main

jobs:
  cd:
    runs-on: ubuntu-latest
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Install
        run: npm ci

      - name: Build
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dist

      - name: Deploy
        id: deployment
        uses: actions/deploy-pages@v4
```

Con esta configuración, cada vez que se realice un push a la rama main, el workflow se ejecutará automáticamente, generando la build y publicando los cambios en GitHub Pages.
