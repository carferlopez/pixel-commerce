# Asset pack — Guía de tamaños y herramientas

## Tamaños requeridos

### `assets/background.png` — Fondo de la tienda
- **Tamaño:** 1600 × 900 px
- **Se renderiza a:** 800 × 450 px con `image-rendering: pixelated` (2× scale)
- Trabaja en el doble de la resolución final para que los píxeles queden nítidos
- Fondo sólido o transparente, sin degradados suaves (el pixel art no los admite bien)

### `assets/npc-*.png` — Sprites de personaje
- **Tamaño:** aprox. 160 × 280 px (se escala a 80 × 140 en pantalla)
- **Fondo:** transparente (PNG-24 con canal alpha)
- Vista frontal, postura neutral
- El offset de posición se ajusta en `data/scene.json` → `sprite.offset`

### Imágenes de producto (para `catalog.json` → `image`)
- **Tamaño:** 200 × 200 px
- **Fondo:** transparente o color plano — evita gradientes
- Se muestra en el modal del catálogo a tamaño completo (relación 1:1)

---

## Herramientas recomendadas

| Herramienta | Precio | Dónde |
|---|---|---|
| **Aseprite** | ~20 € (una vez) | aseprite.com — el estándar para pixel art profesional |
| **Piskel** | Gratis | piskelapp.com — funciona en el navegador, sin instalar nada |
| **Photopea** | Gratis | photopea.com — Photoshop en el navegador, exporta PNG transparente |
| **Libresprite** | Gratis | fork open source de Aseprite |

---

## Guía de paleta de colores

El pixel art funciona mejor con una **paleta limitada y consistente**. Recomendación:

1. Define tu paleta en `data/config.json` → `colors` (máx. 8-16 colores)
2. Usa exactamente esos colores en todos tus assets (fondo, sprites, productos)
3. Esto crea coherencia visual sin esfuerzo adicional

### Paletas de referencia
- **Lospec** (lospec.com/palette-list) — cientos de paletas de pixel art catalogadas
- Paletas recomendadas por tamaño: **DB16** (16 colores), **PICO-8** (16 colores), **Sweetie 16**

---

## Checklist antes de subir

- [ ] `background.png` exportado a 1600×900 px
- [ ] NPC sprite con fondo transparente
- [ ] Imágenes de producto cuadradas (1:1)
- [ ] Todos los assets usan la misma paleta de 16 colores
- [ ] Los hotspots en `scene.json` coinciden con los elementos visuales del fondo
