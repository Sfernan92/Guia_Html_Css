# Guía básica de HTML y CSS

Una guía breve para empezar a entender cómo se estructura una página web y cómo se le aplica estilo.

HTML organiza el contenido. CSS decide cómo se ve ese contenido.

## Contenido

1. [Qué son HTML y CSS](#qué-son-html-y-css)
2. [Estructura mínima de una página](#estructura-mínima-de-una-página)
3. [Etiquetas HTML habituales](#etiquetas-html-habituales)
4. [Clases, id y atributos data-*](#clases-id-y-atributos-data-)
5. [El DOM](#el-dom)
6. [Selectores CSS](#selectores-css)
7. [Inspeccionar una página con DevTools](#inspeccionar-una-página-con-devtools)
8. [Mini práctica](#mini-práctica)

---

## Qué son HTML y CSS

**HTML** significa *HyperText Markup Language*. Usa etiquetas para organizar el contenido de una página: títulos, párrafos, enlaces, imágenes o tablas.

**CSS** significa *Cascading Style Sheets*. Define la apariencia: colores, tamaños, fuentes, márgenes y distribución de los elementos.

Una forma simple de recordarlo:

| Tecnología | Función | Comparación |
|---|---|---|
| HTML | Estructura y significado del contenido | El esqueleto de una casa |
| CSS | Aspecto visual del contenido | La pintura y decoración |

---

## Estructura mínima de una página

Una página HTML suele comenzar así:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi primera página</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <h1>Hola, mundo</h1>
    <p>Esta es mi primera página web.</p>
  </body>
</html>
```

- `<!DOCTYPE html>`: indica que el documento usa HTML moderno.
- `<html>`: contiene toda la página.
- `<head>`: incluye información para el navegador, como el título de la pestaña o el enlace al CSS.
- `<body>`: contiene lo que las personas ven en la página.
- `<link rel="stylesheet" ...>`: conecta el HTML con el archivo CSS.

---

## Etiquetas HTML habituales

Las etiquetas suelen tener una apertura y un cierre:

```html
<p>Este texto es un párrafo.</p>
```

| Etiqueta | Uso | Ejemplo |
|---|---|---|
| `<h1>` a `<h6>` | Títulos y subtítulos | `<h1>Título principal</h1>` |
| `<p>` | Párrafos | `<p>Texto descriptivo</p>` |
| `<a>` | Enlaces | `<a href="https://example.com">Visitar</a>` |
| `<img>` | Imágenes | `<img src="foto.jpg" alt="Descripción">` |
| `<ul>` y `<li>` | Listas | `<li>Primer elemento</li>` |
| `<div>` | Contenedor genérico | `<div>Contenido</div>` |
| `<article>` | Contenido independiente | Una ficha de producto o una noticia |

### Ejemplo: ficha de un libro

```html
<article class="libro" data-id="B-104">
  <h2>Python para análisis de datos</h2>
  <p class="precio descuento">15,99 €</p>
</article>
```

Este bloque representa una ficha de libro. Contiene un título y un precio.

---

## Clases, id y atributos data-*

Los atributos aportan información adicional a una etiqueta HTML.

### `class`

Una clase sirve para agrupar elementos y aplicarles estilos. Varios elementos pueden compartir la misma clase.

```html
<p class="precio">19,99 €</p>
<p class="precio">24,99 €</p>
```

Un elemento puede tener varias clases separadas por espacios:

```html
<p class="precio descuento">15,99 €</p>
```

Este párrafo tiene las clases `precio` y `descuento`.

### `id`

Un `id` identifica un elemento concreto dentro de una página. Debe ser único.

```html
<h1 id="titulo-principal">Catálogo de libros</h1>
```

### `data-*`

Los atributos `data-*` guardan datos personalizados asociados a un elemento. No cambian por sí mismos la apariencia de la página.

```html
<article class="libro" data-id="B-104" data-categoria="programacion">
```

En este ejemplo, `data-id` guarda el código del libro y `data-categoria` guarda su categoría.

| Atributo | Para qué sirve |
|---|---|
| `class="precio"` | Identifica o agrupa elementos de precio |
| `id="titulo-principal"` | Identifica un único elemento de la página |
| `data-id="B-104"` | Guarda un dato adicional sobre el elemento |

---

## El DOM

Cuando el navegador interpreta el HTML, crea una estructura en forma de árbol llamada **DOM** (*Document Object Model*).

```text
html
└── body
    ├── h1
    └── article.libro
        ├── h2
        └── p.precio
```

En el ejemplo anterior, `h2` y `p.precio` son hijos de `article.libro`.

`p.precio` significa: “el elemento `p` que tiene la clase `precio`”. No es una etiqueta nueva.

Entender el DOM ayuda a localizar datos correctamente dentro de una página web.

---

## Selectores CSS

Un selector CSS indica qué elemento o conjunto de elementos queremos seleccionar.

```css
p {
  color: #172033;
}
```

Este selector afecta a todos los párrafos.

| Selector | Qué selecciona |
|---|---|
| `p` | Todos los párrafos |
| `.precio` | Elementos con clase `precio` |
| `#titulo-principal` | El elemento con ese `id` |
| `article.libro` | Artículos con clase `libro` |
| `article.libro h2` | Títulos `h2` dentro de cada libro |
| `.precio.descuento` | El mismo elemento con ambas clases |
| `[data-id]` | Elementos que tienen el atributo `data-id` |
| `.product_pod .price_color` | Elementos con clase `price_color` dentro de un elemento con clase `product_pod` |

### Dos clases en el mismo elemento

```css
.precio.descuento {
  color: #c2410c;
  font-weight: bold;
}
```

No hay espacio entre `.precio` y `.descuento`: selecciona un elemento que tiene ambas clases.

### Un elemento dentro de otro

```css
.product_pod .price_color {
  color: #1b998b;
}
```

Aquí sí hay un espacio. Significa: selecciona los elementos con clase `price_color` que estén dentro de un elemento con clase `product_pod`.

---

## Inspeccionar una página con DevTools

Las herramientas de desarrollo del navegador, conocidas como **DevTools**, permiten revisar el HTML y CSS de una página.

1. Abre una página pública de práctica, por ejemplo [Books to Scrape](https://books.toscrape.com/).
2. Haz clic derecho sobre un título o un precio.
3. Elige **Inspeccionar**.
4. Observa la etiqueta HTML, sus clases y los elementos que la rodean.

Por ejemplo, en Books to Scrape puedes encontrar una estructura parecida a esta:

```html
<article class="product_pod">
  <h3><a title="A Light in the Attic">A Light in the Attic</a></h3>
  <p class="price_color">£51.77</p>
</article>
```

Así puedes reconocer que cada libro está dentro de `article.product_pod` y que su precio usa la clase `price_color`.

---

## Mini práctica

Descarga los archivos `index.html` y `styles.css` de este repositorio en tu ordenador. Después, prueba a cambiar valores en `styles.css`.

Ideas para experimentar:

1. Cambia el color de `.precio`.
2. Modifica el tamaño del título `h1`.
3. Añade un segundo libro usando la misma estructura HTML.
4. Crea una nueva clase llamada `agotado` y úsala para mostrar un libro no disponible.

---

## Resumen

- HTML organiza y da significado al contenido.
- CSS cambia el aspecto visual de ese contenido.
- El DOM representa el HTML como una jerarquía de elementos.
- Las clases, los atributos `id` y `data-*` aportan información sobre los elementos.
- Los selectores CSS ayudan a localizar elementos concretos.
- DevTools permite inspeccionar una página para entender cómo está construida.

> Conocer HTML y CSS no exige ser desarrollador web. Para análisis de datos, ayuda a entender dónde están los datos y cómo identificarlos con precisión.
