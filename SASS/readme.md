# Carpeta SASS

Esta carpeta contiene los estilos fuente del proyecto. Los archivos `.scss` se
organizan por responsabilidad para facilitar el mantenimiento, evitar reglas
duplicadas y permitir que el proyecto crezca sin convertir una sola hoja de
estilos en un archivo difícil de mantener.

## Estructura

```text
SASS/
|-- style.scss
|-- _settings.scss
|-- abstracts/
|   |-- _abstracts.scss
|   |-- _functions.scss
|   |-- _mixins.scss
|   |-- _placeholders.scss
|   `-- _variables.scss
|-- base/
|   |-- _animations.scss
|   |-- _base.scss
|   |-- _reset.scss
|   `-- _typography.scss
|-- components/
|   |-- _buttons.scss
|   `-- _components.scss
|-- layout/
|   |-- _footer.scss
|   |-- _forms.scss
|   |-- _grid.scss
|   |-- _header.scss
|   |-- _layout.scss
|   |-- _navbar.scss
|   `-- _sidebar.scss
|-- pages/
|   |-- _home.scss
|   `-- _pages.scss
|-- themes/
|   |-- _default.scss
|   `-- _themes.scss
`-- vendors/
		`-- _vendors.scss
```

Los archivos que comienzan por `_` son parciales: no se cargan directamente
en el HTML. Se incorporan mediante `@use` desde otros archivos Sass.

## Archivos principales

### `style.scss`

Es el punto de entrada de Sass. Importa los grupos principales con `@use` y
debe contener solo la composicion general de la hoja, no los estilos de cada
componente.

Este es el archivo que se compila hacia `CSS/style.css`.

### `_settings.scss`

Contiene configuracion global del proyecto que no encaja en una sola
categoria, por ejemplo opciones de Sass o configuraciones compartidas.
Mantener aqui solo valores de configuracion evita mezclarlos con reglas CSS.

## `abstracts/`

Contiene herramientas reutilizables. Esta carpeta no deberia generar CSS por
si sola.

- `_variables.scss`: colores, fuentes, tamanos, espaciados, breakpoints y
	z-index. Ejemplo: `$color-primary` o `$breakpoint-tablet`.
- `_functions.scss`: funciones Sass que reciben valores y devuelven otros,
	por ejemplo conversiones de unidades o calculos de color.
- `_mixins.scss`: bloques reutilizables para media queries, flexbox,
	transiciones u otras declaraciones repetidas.
- `_placeholders.scss`: selectores `%placeholder` destinados a `@extend`.
	Deben usarse con moderacion para evitar selectores CSS inesperados.
- `_abstracts.scss`: indice que importa variables, funciones, mixins y
	placeholders para poder cargarlos desde un unico punto.

## `base/`

Contiene los estilos globales que afectan a todo el documento.

- `_reset.scss`: normaliza margenes, paddings, cajas, listas y elementos
	HTML para partir de una base consistente.
- `_typography.scss`: familia tipografica, tamanos base, alturas de linea,
	pesos y estilos de encabezados o enlaces globales.
- `_animations.scss`: `@keyframes` y clases de animacion reutilizables.
- `_base.scss`: indice que importa reset, tipografia y animaciones.

Aqui no deben ir estilos exclusivos de una pagina o de un componente.

## `layout/`

Define la estructura grande de la interfaz.

- `_header.scss`: distribucion y apariencia de la cabecera completa, como
	logo, acciones y zonas superiores.
- `_navbar.scss`: navegacion y sus enlaces. Puede vivir dentro del header,
	pero se mantiene separado porque representa una responsabilidad distinta.
- `_footer.scss`: estructura y estilos del pie de pagina.
- `_grid.scss`: contenedores, columnas y reglas generales de grid o flexbox.
- `_forms.scss`: estructura comun de formularios, labels, inputs y mensajes.
- `_sidebar.scss`: barras laterales y sus zonas internas.
- `_layout.scss`: indice que importa todos los parciales de layout.

Estos archivos deben describir la estructura general, no una tarjeta o un
boton concreto.

## `components/`

Contiene piezas reutilizables de la interfaz.

- `_buttons.scss`: bloque `.button` y sus modificadores, por ejemplo
	`.button--primary` o `.button--secondary`.
- `_components.scss`: indice que importa todos los componentes.

Si el proyecto crece, cada componente puede tener su propio parcial, como
`_card.scss`, `_modal.scss`, `_artwork-card.scss` o `_stats.scss`.

Los componentes deben poder reutilizarse en distintas paginas sin depender
de un selector demasiado especifico de una pagina concreta.

## `pages/`

Contiene ajustes exclusivos de una pagina o vista.

- `_home.scss`: composicion de la pagina principal, por ejemplo el hero, la
	seccion de obras destacadas y las estadisticas de la portada.
- `_pages.scss`: indice que importa los estilos de las paginas.

Si una regla solo tiene sentido en la portada, debe ir en `_home.scss` y no
en `components/` o `base/`.

## `themes/`

Contiene variaciones visuales del proyecto.

- `_default.scss`: valores y reglas del tema predeterminado.
- `_themes.scss`: indice que importa los temas disponibles.

Aqui pueden vivir temas claro, oscuro o variaciones de marca. Los valores
compartidos por todos los temas deben permanecer en `abstracts/`.

## `vendors/`

Contiene adaptaciones o estilos necesarios de librerias externas. Por
ejemplo, ajustes de un datepicker o de un framework de componentes.

- `_vendors.scss`: indice de los estilos externos que se hayan incorporado.

No conviene copiar aqui todos los estilos de una libreria si puede cargarse
desde su propio paquete.

## Relacion con BEM

La estructura de carpetas organiza los estilos por responsabilidad; BEM
organiza los nombres de las clases HTML y CSS.

```html
<header class="site-header">
	<nav class="navbar">
		<a class="navbar__link navbar__link--active" href="#">Market</a>
	</nav>
</header>
```

- Bloque: `.navbar`
- Elemento: `.navbar__link`
- Modificador: `.navbar__link--active`

Un bloque reutilizable debe tener sus estilos en `components/` o `layout/`,
segun si es una pieza visual o una zona estructural. Los modificadores deben
servir para variar un bloque sin duplicar todas sus reglas.

## Flujo de trabajo

1. Escribe los estilos fuente en los parciales de `SASS/`.
2. Importa el parcial desde el indice correspondiente.
3. Comprueba que ese indice esta incluido en `SASS/style.scss`.
4. Compila Sass hacia `CSS/style.css`.
5. Enlaza en el HTML unicamente el CSS generado.

Para compilar una vez:

```bash
npx sass SASS/style.scss CSS/style.css
```

Para observar cambios automaticamente:

```bash
npm run sass
```

La salida final es `CSS/style.css`. No se deben editar manualmente los
estilos dentro de ese archivo, porque se sobrescribiran en la siguiente
compilacion.