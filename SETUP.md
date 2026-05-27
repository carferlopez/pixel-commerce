# Pixel Commerce — Guía de configuración

**Para quién es esto:** alguien que acaba de descargar el pack de Gumroad y quiere tener su tienda funcionando sin escribir código.

---

## 1. Lo que recibes en este pack

```
pixel-commerce/
├── index.html            ← La tienda completa (un solo archivo)
├── SETUP.md              ← Esta guía
├── data/
│   ├── config.json       ← Nombre, colores, fuente, Stripe, sonido
│   ├── catalog.json      ← Tus productos
│   ├── dialogue.json     ← Guión del NPC
│   └── scene.json        ← Fondo y posición de los hotspots
└── assets/
    ├── background.png    ← Imagen de fondo de la tienda
    ├── npc-ada.png       ← Sprite del personaje
    └── audio/            ← Efectos de sonido y música
```

---

## 2. Cómo verlo funcionar en 30 segundos

**Opción rápida (solo demo, sin editar):**
Abre `index.html` en **Firefox** o **Safari**. Verás la tienda demo funcionando.

> ⚠️ Chrome bloquea la carga de archivos locales por seguridad. Para Chrome (y para ver tus cambios al editar), usa la opción siguiente.

**Opción recomendada (para personalizar y ver cambios):**
1. Descarga [VS Code](https://code.visualstudio.com/) — gratis
2. Abre VS Code → Extensions (Ctrl+Shift+X) → busca **Live Server** → instalar
3. Abre la carpeta `pixel-commerce/` en VS Code (File → Open Folder)
4. Haz clic en **Go Live** en la esquina inferior derecha
5. Se abre en tu navegador. Cada vez que guardas un archivo, se actualiza automáticamente

[SCREENSHOT: VS Code con "Go Live" marcado en la barra inferior]

---

## 3. Cambia el fondo

**Para reemplazar la imagen:**
1. Crea o descarga una imagen de **1600 × 900 px** en formato PNG
   (ver `assets/examples/README.md` para herramientas recomendadas)
2. Guárdala como `assets/background.png` — sobreescribe el archivo existente
3. Refresca el navegador

**Para mover los hotspots (las zonas clickables de la escena):**
Los hotspots están definidos en `data/scene.json`. Cada uno tiene un campo `rect` con las coordenadas en píxeles:

```json
{
  "id": "shelves",
  "rect": { "x": 36, "y": 50, "w": 212, "h": 165 }
}
```
→ Zona que empieza en (36, 50), de 212 px de ancho y 165 px de alto.

**Truco para encontrar coordenadas con DevTools:**
1. Abre la tienda con Live Server
2. Pulsa **F12** para abrir DevTools
3. Haz clic en el icono de cursor (arriba-izquierda del panel de DevTools)
4. Pasa el cursor sobre la escena — aparece una capa azul con las coordenadas
5. Anota los valores `x`, `y` y ajusta `w` y `h` según el tamaño del área

[SCREENSHOT: DevTools con el inspector de elementos activo sobre la escena]

---

## 4. Cambia el NPC

**El sprite:**
1. Crea tu sprite en PNG con fondo transparente, aprox. 160 × 280 px
2. Guárdalo como `assets/npc-ada.png` (o el nombre que prefieras)
3. Si cambias el nombre, actualiza `data/scene.json` → `hotspots[id=npc].sprite.src`

**El guión (diálogo):**
Abre `data/dialogue.json`. Funciona con nodos conectados por IDs:

```json
"greeting": {
  "speaker": "Ada",
  "text": "Bienvenido. ¿En qué puedo ayudarte?",
  "choices": [
    { "label": "Ver el catálogo",    "next": "show_catalog" },
    { "label": "Solo miro, gracias.", "next": "goodbye" }
  ]
}
```

- `speaker` → nombre que aparece encima del texto
- `text` → lo que dice el personaje
- `choices` → lista de respuestas del jugador; cada una tiene `label` (texto) y `next` (id del siguiente nodo)
- El nodo `"show_catalog"` abre el modal de productos automáticamente
- El nodo `"goodbye"` cierra el diálogo

El campo `"start"` al principio del archivo indica qué nodo se muestra primero.

---

## 5. Cambia los productos

En `data/catalog.json` cada producto es un objeto JSON. Anatomía completa:

```json
{
  "id": "producto-01",
  "name": "Nombre del producto",
  "description": "Descripción breve. Máximo 2 frases.",
  "price": 49,
  "currency": "EUR",
  "image": "assets/products/mi-imagen.png",
  "badge": "NUEVO",
  "available": true,
  "stripeUrl": "https://buy.stripe.com/TU_LINK_AQUÍ"
}
```

| Campo | Qué hace |
|---|---|
| `id` | Identificador único, sin espacios |
| `name` | Nombre visible en la tienda |
| `description` | Texto descriptivo del producto |
| `price` | Precio numérico (sin símbolo) |
| `currency` | Código de moneda: `"EUR"`, `"USD"`, `"GBP"`… |
| `image` | Ruta a la imagen del producto (200×200 px) |
| `badge` | Etiqueta pequeña: `"NUEVO"`, `"ÚLTIMAS 3"`, `"SOLD OUT"` o `""` para ninguna |
| `available` | `true` muestra botón COMPRAR, `false` muestra AGOTADO |
| `stripeUrl` | Enlace de pago de Stripe |

**Cómo crear un Stripe Payment Link:**
1. Ve a [dashboard.stripe.com](https://dashboard.stripe.com) → Payment Links → + New
2. Añade el producto, el precio y la imagen
3. Haz clic en **Create link** y copia la URL
4. Pégala en el campo `stripeUrl` del producto correspondiente

Documentación oficial: [stripe.com/docs/payment-links](https://stripe.com/docs/payment-links)

---

## 6. Cambia los colores y la fuente

En `data/config.json`, sección `colors`:

```json
"colors": {
  "background": "#1a1a2e",
  "panel":      "#16213e",
  "border":     "#e94560",
  "accent":     "#e94560",
  "text":       "#eaeaea",
  "textDim":    "#888888",
  "verbBg":     "#0f3460"
}
```

Los colores van en formato hexadecimal `#rrggbb`. Usa [coolors.co](https://coolors.co) para crear paletas.

| Variable | Dónde aparece |
|---|---|
| `background` | Fondo general de la tienda |
| `panel` | Paneles y cuadro de diálogo |
| `border` | Todos los bordes y marcos |
| `accent` | Color principal de acento (botones, resaltados) |
| `text` | Texto principal |
| `verbBg` | Fondo de la verb bar |

**Para cambiar la fuente:**
Busca cualquier fuente pixel en [Google Fonts](https://fonts.google.com) y actualiza:

```json
"font": {
  "family": "'VT323', monospace",
  "googleFontsUrl": "https://fonts.googleapis.com/css2?family=VT323&display=swap"
}
```

Fuentes recomendadas estilo pixel: `Press Start 2P`, `VT323`, `Silkscreen`, `Pixelify Sans`.

---

## 7. Cómo publicarlo gratis

**Netlify — la opción más fácil:**
1. Ve a [netlify.com](https://app.netlify.com) → crea una cuenta gratis
2. En el dashboard → **Add new site → Deploy manually**
3. Arrastra la carpeta `pixel-commerce/` entera al área indicada
4. En segundos tendrás un enlace público tipo `tu-tienda.netlify.app`

[SCREENSHOT: Área de drag-and-drop de Netlify con la carpeta del proyecto]

**Para dominio propio (opcional):**
Netlify → tu sitio → Domain settings → Add custom domain → sigue las instrucciones.

**Cloudflare Pages (alternativa):**
Conecta tu repo de GitHub a Cloudflare Pages. Deploy automático en cada push a `main`.

---

*¿Algo no funciona? Revisa que estés usando **Live Server** (no doble clic en el archivo) y que los archivos JSON estén bien formateados. Puedes validar JSON en [jsonlint.com](https://jsonlint.com).*
