# 🖼️ Laboratorio: CSS Media Queries e Imágenes Responsivas

Este laboratorio te guía paso a paso por las propiedades CSS más importantes para hacer imágenes responsivas, y te enseña a usar **media queries** para adaptar el diseño a distintos tamaños de pantalla.

---

## 1) Requisitos previos

- Un navegador moderno (Chrome, Edge, Firefox, Safari).
- Un editor de código (se recomienda VS Code).
- Conocimientos básicos de HTML y selectores CSS.

---

## 2) Archivos del proyecto

| Archivo | Función |
|---|---|
| `index.html` | La página web — **no modifiques este archivo** |
| `custom.css` | Tu área de trabajo — **todo tu código va aquí** |
| `README.md` | Este tutorial |

Abre `index.html` en tu navegador. Deberías ver una página con una imagen hero, tarjetas de demostración y una cuadrícula de fotos. Cambia el tamaño de la ventana del navegador para observar cómo cambian (o no, todavía) los elementos.

> 💡 **Tip:** En Chrome o Edge, abre las DevTools → activa la barra de dispositivos (Ctrl+Shift+M) para simular distintos tamaños de pantalla fácilmente.

---

## 3) Objetivos de aprendizaje

Al terminar este laboratorio podrás:

- Usar `object-fit` y `object-position` para controlar cómo las imágenes llenan un contenedor.
- Usar `aspect-ratio` para mantener proporciones fijas.
- Escribir **media queries mobile-first** con breakpoints `min-width`.
- Construir una cuadrícula **CSS Grid responsiva** que cambia de columnas según el breakpoint.
- Usar `prefers-color-scheme` para soportar el modo oscuro (ejercicio bonus).

---

## 4) Ejercicios (paso a paso)

Abre `custom.css` en tu editor. Cada ejercicio está marcado con un bloque de comentarios y marcadores `✏️ TU TURNO` que indican exactamente dónde escribir tu código.

---

### Ejercicio 1 — `object-fit` y `object-position`

**Objetivo:** Hacer que los tres marcos de imagen muestren sus imágenes correctamente usando `object-fit`.

Cada marco tiene un contenedor de tamaño fijo. La propiedad `object-fit` le indica al navegador cómo redimensionar el elemento `<img>` dentro de ese contenedor.

| Valor | Comportamiento |
|---|---|
| `cover` | Llena el marco, recorta si es necesario, conserva la proporción |
| `contain` | Muestra la imagen completa dentro del marco, puede dejar espacio vacío |
| `fill` | Estira la imagen para llenar el marco, puede distorsionarla |
| `none` | Sin redimensionado, puede desbordar el contenedor |

**Pasos:**
1. En `custom.css`, localiza los bloques `.frame-cover`, `.frame-contain` y `.frame-position`.
2. Agrega `height: 200px` a cada regla `.frame-*`.
3. Aplica el valor correcto de `object-fit` a cada `.showcase-img` dentro de esos marcos.
4. En `.frame-position`, experimenta con valores de `object-position` como `top`, `bottom`, `left`, `right` o `50% 20%`.

<details>
<summary>💡 Solución</summary>

```css
.frame-cover {
  height: 200px;
}
.frame-cover .showcase-img {
  object-fit: cover;
}

.frame-contain {
  height: 200px;
}
.frame-contain .showcase-img {
  object-fit: contain;
}

.frame-position {
  height: 200px;
}
.frame-position .showcase-img {
  object-fit: cover;
  object-position: top;
}
```
</details>

---

### Ejercicio 2 — `aspect-ratio`

**Objetivo:** Hacer que el contenedor `.frame-aspect` siempre mantenga una proporción 16:9 sin importar el ancho de la pantalla.

La propiedad `aspect-ratio` define la relación preferida entre el ancho y el alto de un elemento. Combinada con `object-fit: cover`, las imágenes siempre llenarán un recuadro perfectamente proporcional.

**Pasos:**
1. Localiza `.frame-aspect` en `custom.css`.
2. Agrega `aspect-ratio: 16 / 9;`.
3. Agrega `object-fit: cover;` a `.frame-aspect .showcase-img`.
4. Cambia el tamaño del navegador y observa la tarjeta — el recuadro de imagen siempre debe ser más ancho que alto.

<details>
<summary>💡 Solución</summary>

```css
.frame-aspect {
  width: 100%;
  aspect-ratio: 16 / 9;
  overflow: hidden;
}

.frame-aspect .showcase-img {
  object-fit: cover;
}
```
</details>

---

### Ejercicio 3 — Imagen Hero: Media Queries Mobile-First

**Objetivo:** Hacer que la imagen hero sea más alta en pantallas grandes usando media queries con `min-width`.

**Mobile-first** significa que primero escribes el estilo para la pantalla más pequeña (sin media query), y luego usas `@media (min-width: ...)` para mejorar progresivamente el diseño en pantallas más grandes.

```
Móvil (base) → Pequeño → Mediano → Grande → Extra Grande
(sin query)     576px      768px     992px     1200px
```

**Pasos:**
1. Localiza `.hero-img` en `custom.css`. Establece `height: 200px` como valor base.
2. Agrega una media query para **≥ 576px** que defina `height: 280px`.
3. Agrega una media query para **≥ 768px** que defina `height: 350px`.
4. Agrega una media query para **≥ 992px** que defina `height: 450px`.
5. Agrega una media query para **≥ 1200px** que defina `height: 520px`.

Observa la **barra indicadora de breakpoints** en la parte superior de la página mientras cambias el tamaño — te muestra qué breakpoint está activo en cada momento.

<details>
<summary>💡 Solución</summary>

```css
.hero-img {
  width: 100%;
  display: block;
  object-fit: cover;
  height: 200px;
}

@media (min-width: 576px) {
  .hero-img { height: 280px; }
}

@media (min-width: 768px) {
  .hero-img { height: 350px; }
}

@media (min-width: 992px) {
  .hero-img { height: 450px; }
}

@media (min-width: 1200px) {
  .hero-img { height: 520px; }
}
```
</details>

---

### Ejercicio 4 — Cuadrícula Responsiva con CSS Grid

**Objetivo:** Hacer que `.responsive-grid` cambie de 1 columna en móvil hasta 4 columnas en pantallas extra grandes.

`grid-template-columns: repeat(N, 1fr)` divide el contenedor en `N` columnas de igual ancho.

| Breakpoint | Columnas |
|---|---|
| Base (móvil) | 1 |
| ≥ 576px (sm) | 2 |
| ≥ 768px (md) | 2 |
| ≥ 992px (lg) | 3 |
| ≥ 1200px (xl) | 4 |

**Pasos:**
1. Localiza `.responsive-grid` en `custom.css`.
2. Establece `grid-template-columns: repeat(1, 1fr);` como valor base.
3. Escribe cuatro reglas `@media (min-width: ...)` aumentando las columnas según la tabla de arriba.

<details>
<summary>💡 Solución</summary>

```css
.responsive-grid {
  display: grid;
  gap: 1.25rem;
  grid-template-columns: repeat(1, 1fr);
}

@media (min-width: 576px) {
  .responsive-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 768px) {
  .responsive-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 992px) {
  .responsive-grid { grid-template-columns: repeat(3, 1fr); }
}

@media (min-width: 1200px) {
  .responsive-grid { grid-template-columns: repeat(4, 1fr); }
}
```
</details>

---

### Ejercicio 5 — BONUS: Modo Oscuro con `prefers-color-scheme`

**Objetivo:** Responder a la preferencia de modo oscuro del sistema operativo del usuario usando una media query.

`@media (prefers-color-scheme: dark)` se activa cuando el usuario tiene su sistema en modo oscuro. Puedes cambiar colores automáticamente — sin necesidad de JavaScript.

**Pasos:**
1. Localiza la sección bonus al final de `custom.css`.
2. Escribe `@media (prefers-color-scheme: dark) { ... }`.
3. Dentro, define:
   - `body`: fondo `#121212` y color de texto `#f0f0f0`
   - `.r-card`: fondo `#1e1e1e` y borde `#444`
4. Cambia tu sistema operativo a modo oscuro y recarga la página.

<details>
<summary>💡 Solución</summary>

```css
@media (prefers-color-scheme: dark) {
  body {
    background-color: #121212;
    color: #f0f0f0;
  }
  .r-card {
    background-color: #1e1e1e;
    border-color: #444;
  }
}
```
</details>

---

## 5) Sube tus cambios al repositorio

Una vez que termines los ejercicios, sube tu trabajo:

```bash
git add custom.css
git commit -m "Laboratorio CSS media queries e imágenes completado"
git push origin main
```

---

## 6) Referencia rápida

| Propiedad | ¿Qué hace? |
|---|---|
| `object-fit: cover` | Llena el contenedor, recorta la imagen, conserva la proporción |
| `object-fit: contain` | Muestra la imagen completa, puede dejar espacio vacío |
| `object-position` | Controla qué parte de la imagen es visible al recortar |
| `aspect-ratio: 16/9` | Fija la relación ancho/alto del contenedor |
| `width: 100%` | La imagen ocupa todo el ancho del padre |
| `max-width: 100%` | Evita que la imagen desborde su contenedor |
| `height: auto` | La altura se ajusta proporcionalmente al ancho |
| `background-size: cover` | El fondo llena el área, se recorta si es necesario |
| `@media (min-width: Xpx)` | Aplica estilos a partir de ese breakpoint |
| `@media (prefers-color-scheme: dark)` | Aplica estilos en modo oscuro |

---

*Laboratorio CSS Media Queries — FCA Informática UNAM*
