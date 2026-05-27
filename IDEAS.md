# Ideas para v1.1+

Ideas descartadas de v1.0 por scope. Implementar después de validar ventas.

---

## Easter egg — ventana

Mirar la ventana 3 veces consecutivas revela algo:
- Un mensaje secreto (`"La ciudad nunca duerme. Tú sí deberías."`)
- O un código de descuento en Stripe
- O un item oculto que aparece en el inventario

**Por qué funciona:** es el tipo de detalle que se comparte en Twitter/X. Coste cero de implementación, valor de marketing alto.

**Implementación tentativa:**
```js
// En state: windowClickCount: 0
// En handleHotspot('window', 'Mirar'):
//   state.windowClickCount++
//   if (state.windowClickCount >= 3) triggerEasterEgg()
```

---

## Variantes de producto (talla / color)

Añadir array `variants` a cada item de `catalog.json`.
Ver feedback de Carlos, sesión Día 2.

---

## Multi-item cart (v2.0)

El checkout de v1.0 usa un Stripe Payment Link por producto.
Para v2.0: Stripe Checkout Session via edge function (Cloudflare Workers o Vercel Edge).
Documentar en `UPGRADE.md`.

---

## Animación idle del NPC

Ada debería parpadear o moverse ligeramente cuando no interactúas con ella.
CSS keyframe animation en el sprite, configurable desde `scene.json`.

---

## Segunda escena

Sistema multi-room: `scene.json` permite definir múltiples escenas y transiciones entre ellas.
Fuera del scope por diseño en v1.0 (single-scene).
