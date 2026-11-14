# QuitaMarca

Editor de **imágenes y videos** que corre 100 % en el navegador (sin servidor, sin instalar nada y sin subir tus archivos). Pensado para publicarse en **GitHub Pages**.

## Funciones
- **Recortar y girar:** recorte libre o por proporción (1:1, 9:16, 16:9, 4:5), girar 90° y voltear. En video, cortar inicio y fin.
- **Ajustes:** brillo, contraste, saturación y blanco y negro.
- **Texto:** color, tamaño, negrita, contorno; se arrastra a cualquier posición.
- **Logo propio:** sube tu logo, ajusta tamaño y opacidad, y arrástralo.
- **Desenfocar o pixelar** zonas (caras, placas, datos).
- **Quitar marca / logo** rectangular por relleno (inpainting) en imagen y video.
- **Exportar:** PNG o JPG; en video, WebM (o MP4 en Safari) con el audio original.

> Úsalo solo con contenido propio o con licencia. La función de quitar marca no está pensada para material protegido de terceros.

## Publicar en GitHub Pages
1. Crea un repositorio y sube estos archivos a la rama `main`.
2. En el repositorio: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Cada `push` a `main` ejecuta las pruebas y publica el sitio en `https://TU_USUARIO.github.io/NOMBRE_DEL_REPO/`.

Para probarlo en tu equipo basta con un servidor estático:
```bash
python3 -m http.server 8000   # y abre http://localhost:8000
```
(Abrir `index.html` con doble clic también funciona para imágenes; para video es mejor usar el servidor.)

## Cómo está hecho
| Archivo | Qué hace |
|---|---|
| `js/inpaint.js` | Relleno de zonas rectangulares (interpolación + suavizado de Laplace). |
| `js/effects.js` | Desenfoque, pixelado y ajustes de color. |
| `js/render.js` | Orden de edición: girar/recortar → zonas → color → texto y logo. Igual para vista previa y exportación. |
| `js/app.js` | Interfaz, estado y exportación (imágenes con `canvas`, video con `MediaRecorder`). |

## Pruebas
```bash
node tests/inpaint.test.js
node tests/effects.test.js
```

## Limitaciones
- Exportar video es en tiempo real: dura lo mismo que el video, y la pestaña debe quedar abierta y visible.
- El video sale en WebM en Chrome/Edge/Firefox; Safari genera MP4. Requiere un navegador con `MediaRecorder`.
- Quitar marca funciona con zonas **rectangulares y fijas** y rinde mejor sobre fondos simples; en fondos con mucho detalle puede dejar restos.
- Un video muy grande (4K) puede ir lento: usa el tamaño máximo 720p/1080p al exportar.

## Licencia
MIT.




https://colombiahack.github.io/QuitaMarca/
