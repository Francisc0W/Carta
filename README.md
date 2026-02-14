# 💌 Nuestro Aniversario — Carta de Amor Interactiva

Una experiencia web romántica e interactiva diseñada como regalo de aniversario. El proyecto presenta una animación de sobre que se abre al tocarlo, revelando una tarjeta personalizada con un **árbol de corazones**, **pétalos cayendo** y un **contador en tiempo real** del tiempo transcurrido juntos.

---

## 🌟 Vista Previa

| Pantalla 1: Sobre cerrado | Pantalla 2: Tarjeta abierta |
|---|---|
| Sobre animado con sello de corazón, solapa que se abre y corazones flotantes de fondo. | Carta de amor con texto en cascada, árbol cuya copa forma un corazón hecho de pétalos `❤`, y contador de tiempo. |

---

## ✨ Características

### 🎭 Pantalla 1 — El Sobre
- **Sobre realista** con cuerpo, solapa y sello de corazón central.
- **Animación de apertura**: la solapa se abre con rotación 3D (`rotateX`) y la carta asoma hacia arriba.
- **Corazones flotantes** decorativos en el fondo con animación infinita.
- **Texto pulsante** "Toca para abrir ❤" que invita a la interacción.
- Compatible con **toque (touch)** y **clic** para máxima compatibilidad.

### 💌 Pantalla 2 — La Tarjeta
- **Texto en cascada**: título, párrafos y firma aparecen secuencialmente con animaciones `fade-in` + `slide-up`.
- **Árbol de corazones**: un tronco con textura de corteza y una copa formada por ~480 pétalos `❤` distribuidos uniformemente dentro de la forma matemática de un corazón.
- **Pétalos cayendo**: animación continua de pétalos desprendiéndose del árbol con trayectoria realista de viento.
- **Contador en tiempo real**: muestra días, horas, minutos y segundos transcurridos desde la fecha de inicio de la relación.

---

## 🛠️ Tecnologías Utilizadas

| Tecnología | Uso |
|---|---|
| **HTML5** | Estructura semántica del documento |
| **CSS3** | Animaciones, gradientes, `clip-path`, media queries, `safe-area-inset` para iPhone |
| **JavaScript** (Vanilla) | Lógica de interacción, generación dinámica del árbol, contador en tiempo real |
| **Google Fonts** | Tipografías *Playfair Display* (títulos/firma) y *Nunito* (texto) |

---

## 📁 Estructura del Proyecto

```
Proyecto/
├── Amor.html      # Archivo único con HTML, CSS y JS integrados
└── README.md      # Este archivo
```

> 📝 Todo el proyecto está contenido en un **único archivo HTML** autocontenido, sin dependencias externas más allá de Google Fonts. Esto facilita compartirlo y abrirlo en cualquier dispositivo.

---

## 🚀 Cómo Usar

### Abrir localmente
1. Descarga o clona el repositorio.
2. Abre el archivo `Amor.html` en cualquier navegador moderno.

### Compartir por WhatsApp u otras plataformas
1. Sube `Amor.html` a un servicio de hosting estático como:
   - [GitHub Pages](https://pages.github.com/)
   - [Netlify](https://www.netlify.com/)
   - [Vercel](https://vercel.com/)
   - [Tiiny.host](https://tiiny.host/) (ideal para archivos individuales)
2. Comparte el enlace generado.

---

## ⚙️ Personalización

### 📅 Cambiar la fecha de inicio
Edita la línea dentro del bloque `<script>` en `Amor.html`:

```javascript
// 9 de Octubre de 2025, 12:00 AM
const fechaInicio = new Date(2025, 9, 9, 0, 0, 0);
```

> ⚠️ **Nota:** En JavaScript, los meses van de `0` (enero) a `11` (diciembre). Por lo tanto, `9` equivale a **octubre**.

### ✍️ Cambiar los textos de la carta
Modifica el contenido dentro del bloque `<div class="columna-texto">`:

```html
<span class="titulo-principal" id="txt-1">Para el amor de mi vida:</span>
<span class="parrafo" id="txt-2">Si pudiera elegir un lugar seguro, sería a tu lado.</span>
<span class="parrafo" id="txt-3">Cuanto más tiempo estoy contigo más te amo.</span>
<div class="firma" id="txt-4">— Te amo —</div>
```

### 🎨 Cambiar los colores del árbol
Los colores de los pétalos de la copa se definen en el array `colores` dentro de la función `construirArbol()`:

```javascript
var colores = [
    '#b01030', '#c2185b', '#d81b60', '#ad1457',  // rojos profundos
    '#cc1a1a', '#d42b2b', '#e63946',              // rojos
    '#e84a5f', '#d44d5c', '#f06292',              // rosas medios
    '#ff6b81', '#ff8a9b', '#ffb3c1'               // rosas claros
];
```

### 🌸 Ajustar la densidad de pétalos
Cambia el número `480` en la función `construirArbol()` para más o menos pétalos en la copa:

```javascript
while (colocados < 480 && intentos < 5000) {
```

---

## 📱 Compatibilidad

| Plataforma | Estado |
|---|---|
| 🖥️ Desktop (Chrome, Firefox, Edge, Safari) | ✅ Compatible |
| 📱 iPhone (Safari, Chrome) | ✅ Optimizado con `safe-area-inset` y `touch` events |
| 📱 Android (Chrome, Samsung Internet) | ✅ Compatible |
| 📱 iPhone SE / pantallas pequeñas | ✅ Media queries específicas para ≤375px |

### Optimizaciones para móvil
- **Viewport** configurado con `viewport-fit=cover` y `user-scalable=no`.
- **Safe areas** para iPhones con notch (`env(safe-area-inset-*)`).
- **Apple Web App** meta tags para experiencia fullscreen.
- **Touch events** (`touchend`) para respuesta inmediata en iOS.
- **Diseño responsive** con 3 breakpoints: desktop, ≤768px y ≤375px.

---

## 🧮 Detalle Técnico: Forma del Corazón

La copa del árbol utiliza la **ecuación implícita del corazón**:

```
(x² + y² - 1)³ - x²y³ ≤ 0
```

Se emplea *rejection sampling* (muestreo por rechazo) para distribuir pétalos uniformemente dentro de esta forma, generando puntos aleatorios y verificando si caen dentro de la curva.

---

## 🎬 Flujo de Animaciones

```
1. Usuario toca/clickea el sobre
   └─► Solapa se abre (rotación 3D, 0.8s)
       └─► Carta asoma del sobre (0.6s, delay 0.4s)
           └─► Sobre desaparece (fade out 0.8s, delay 1.1s)
               └─► Tarjeta aparece (fade in + scale, 1s)
                   ├─► Textos en cascada (350ms + 280ms × i)
                   ├─► Contador visible (delay 1.5s)
                   └─► Pétalos cayendo (cada 280ms, delay 1.8s)
```

---

## 📄 Licencia

Este proyecto es un regalo personal. Siéntete libre de usarlo, modificarlo y compartirlo con tus seres queridos. ❤️

---

> *Hecho con mucho amor 💕*
