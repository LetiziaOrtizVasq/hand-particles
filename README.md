# hand-particles — PromoUPSA 2026

Experiencia interactiva de realidad aumentada para la feria vocacional de **Ingeniería de Sistemas UPSA**.  
Un solo archivo HTML — sin frameworks, sin dependencias locales. Diseñado para proyectarse sobre tela blanca.

## Correr

```bash
node server.js
```

Abre `http://localhost:8080` automáticamente. Permite el acceso a la cámara cuando el browser lo pida.

---

## Filtros disponibles

| # | Filtro | Descripción |
|---|--------|-------------|
| 1 | **Particles** | ~6500 partículas en color #035447 forman "PROMO UPSA"; la mano las dispersa con física de resorte y glow |
| 2 | **Garden** | Flor pixel-art que abre/cierra según la apertura de la mano. Flores disponibles: Pixel Daisy, Pixel Sunray, Pixel Rose |
| 3 | **Face** | HUD con esquinas en #035447, scan line, ID aleatorio y coordenadas ficticias |
| 4 | **Wireframe** | Malla triangulada 3D sobre la mano con scan line de escáner |
| 5 | **Hacker** | Comandos de terminal reales cayendo en lluvia; la mano activa "ACCESO CONCEDIDO" |
| 6 | **Animal Gesture** | Muestra imágenes de animales según el gesto detectado (ver tabla abajo) |
| 7 | **Retro Portrait** | Efecto fotografía 1-bit con dithering Floyd-Steinberg, galería con descarga, copia y exportación a Instagram Story |

**Botón de cámara** (esquina superior derecha): alterna entre Color / B&N / Sin cámara.

---

## Animal Gesture — gestos

| Gesto | Animal |
|-------|--------|
| ✌️ Paz (índice + medio) | Hámster |
| 👍 Pulgar arriba | Gato |
| ✋ Mano abierta | Gato 2 |
| 🙌 Manos en cabeza (ambas manos abiertas, separadas) | Gato 3 |
| ✊✊ Doble puño (ambas manos cerradas) | Hámster 2 |
| 🤟 Shocker (pulgar + meñique) | Gato 4 |

---

## Stack

| Qué | Cómo |
|-----|------|
| Detección de mano | [MediaPipe Hands](https://cdn.jsdelivr.net/npm/@mediapipe/hands/) — CDN |
| Detección facial | [MediaPipe Face Detection](https://cdn.jsdelivr.net/npm/@mediapipe/face_detection/) — CDN |
| Cámara | [MediaPipe Camera Utils](https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils/) — CDN |
| Tipografía | Space Grotesk + Inter + IBM Plex Mono — Google Fonts CDN |
| Renderizado | Canvas 2D API — vanilla JS |
| Servidor | Node.js `http` nativo |

---

## Decisiones de diseño

### Proyección sobre tela blanca
Todo el diseño está pensado para proyectarse sobre tela blanca: los elementos oscuros/negros y el color UPSA `#035447` son visibles, el blanco se funde con la tela. El fondo del canvas es transparente salvo en filtros específicos.

### Un solo archivo HTML
Todo el CSS y JS está embebido en `index.html`. No hay build step, no hay bundler, no hay node_modules.

### Sistema de colores
El color principal es el **verde UPSA** (`#035447`). Se usa en partículas, flores Garden, marco Face y acento general. El acento global `const ACCENT` y `const A` permiten cambiarlo en una sola línea.

### Canvas overlay
El canvas cubre toda la pantalla (`position: fixed; inset: 0`). El video es `display: none` y se dibuja en el canvas al inicio de cada frame con `ctx.scale(-1,1)` para el espejo. Los landmarks de MediaPipe se convierten a coordenadas de pantalla con `sx = (1 - lm.x) * W`.

---

## Requisitos

- Node.js (cualquier versión reciente)
- Chrome o Edge (recomendado)
- Webcam
