# Proyecto base para landing pages

Esta carpeta sirve como base reutilizable para crear proyectos front-end de tipo landing page o header empresarial.

## Estructura general

- `index.html`: archivo principal de la página
- `404.html`: página de error 404
- `CSS/`: estilos finales en producción
- `SASS/`: archivos fuente de estilo para organizar el diseño
- `JS/`: scripts del proyecto
- `IMG/`: imágenes y recursos visuales
- `site.webmanifest`: configuración para PWA
- `robots.txt`: configuración para buscadores
- `package.json`: dependencias y scripts de compilación
- `webpack.*.js`: configuración de Webpack

## Flujo recomendado

1. Copia esta carpeta como base para cada nuevo proyecto.
2. Modifica `index.html` y el contenido visual.
3. Ajusta o reemplaza archivos en `SASS/` y `CSS/`.
4. Añade imágenes a `IMG/`.
5. Mantén la estructura para que cada proyecto sea consistente.

## Scripts útiles

```bash
npm install
npm start
npm run build
```

## Para que Sass funcione

Si quieres compilar los estilos desde `SASS` hacia `CSS`, primero instala Sass:

```bash
npm install -D sass
```

Luego ejecuta el watcher para compilar automáticamente:

```bash
npx sass --watch SASS/style.scss CSS/style.css
```

> Importante: debes ejecutar este comando desde la carpeta del proyecto, es decir dentro de `Ejemplo-Projecto`.

Este proyecto funciona como base estándar para reutilizar en diferentes trabajos y mantener una organización limpia.
