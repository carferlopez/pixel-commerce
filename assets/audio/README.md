# Audio — Pixel Commerce

## Cómo reemplazar los sonidos

Los tres archivos de esta carpeta son **stubs vacíos**. Reemplázalos con tus propios sonidos.

### Archivos esperados

| Archivo | Uso | Duración recomendada |
|---|---|---|
| `click.wav` | Clic en verb buttons | < 0.2 s |
| `notify.wav` | Notificaciones flotantes | < 0.5 s |
| `ambient.mp3` | Música de fondo en loop | 30 s – 3 min |

### Dónde conseguir sonidos gratis (CC0)

**[freesound.org](https://freesound.org)**
— Filtra por licencia **CC0** (Creative Commons Zero = uso libre sin atribución)
— Búsquedas recomendadas:
  - `"ui click"` → sonido de interfaz pixelada
  - `"notification chime"` → campanilla breve
  - `"chiptune loop"` → música ambiente estilo 8-bit
  - `"retro game music"` → ambient loop

**[opengameart.org](https://opengameart.org)**
— Filtrar por CC0 en la búsqueda
— Sección "music" tiene loops chiptune listos para usar

### Para desactivar el audio

En `data/config.json`, cambia:
```json
"audio": { "enabled": false }
```

### Formatos aceptados

- WAV → máxima compatibilidad para efectos cortos
- MP3 → recomendado para el ambient (menor tamaño de archivo)
- OGG → alternativa a MP3, misma calidad menor tamaño

El motor usa `new Audio()` nativo del navegador — no hace falta ninguna librería.
