# Web de la boda — Blanca & Javi

Guía rápida para dejarlo todo funcionando.

## 1. Fotos de la pareja, la iglesia y la finca

La web busca estas imágenes exactas. Crea una carpeta `images/` junto a `index.html`
y coloca ahí (con esos mismos nombres) tus propias fotos:

- `images/hero.jpg` → foto de portada de Blanca y Javi (horizontal, ideal 1600×1200 o más)
- `images/iglesia.jpg` → foto de la Parroquia de Santiago Apóstol
- `images/finca.jpg` → foto de la Hacienda del Álamo

Si no existen, la web muestra un fondo de color liso con un aviso — no rompe nada,
simplemente no se ve tan bonita hasta que las añadas.

## 2. La música (Heartbeats, José González)

No puedo incluir el archivo de la canción por derechos de autor. Debéis:

1. Conseguir el mp3 de forma legal (compra en Bandcamp/iTunes, o exportar desde vuestra
   propia librería si ya la tenéis comprada).
2. Crear una carpeta `audio/` junto a `index.html`.
3. Guardar el archivo como `audio/heartbeats.mp3`.

La web ya está preparada: al tocar el botón "Reproducir Heartbeats" en la portada, sonará.
(Los navegadores no permiten reproducir audio automáticamente sin que el usuario interactúe
primero, así que el botón es necesario — es lo habitual en cualquier web de boda.)

## 3. Subida de fotos de los invitados y confirmaciones de asistencia

Ambas cosas usan el mismo "backend" gratuito con Google Apps Script. Son 15 minutos:

1. Crea DOS carpetas en tu Google Drive:
   - Una para las fotos, por ejemplo **"Fotos boda Blanca y Javi"**.
   - Otra para las confirmaciones, por ejemplo **"Confirmaciones boda Blanca y Javi"**.
2. Abre cada una y copia su ID de la URL:
   `drive.google.com/drive/folders/`**`ESTE_TROZO_ES_EL_ID`**
3. Ve a [script.google.com](https://script.google.com) → **Proyecto nuevo**.
4. Borra el contenido de ejemplo y pega el contenido del archivo `apps-script.gs`.
5. Completa las dos líneas:
   ```js
   const FOLDER_ID = "...";       // ID de la carpeta de fotos
   const RSVP_FOLDER_ID = "...";  // ID de la carpeta de confirmaciones
   ```
6. Arriba a la derecha, **Implementar → Nueva implementación**.
   - Tipo: **Aplicación web**
   - Ejecutar como: **Yo** (tu cuenta)
   - Quién tiene acceso: **Cualquier usuario**
7. Autoriza los permisos que te pida Google (es tu propio script, es seguro).
8. Copia la URL que te da ("URL de la aplicación web").
9. Abre `index.html`, busca la línea:
   ```js
   const APPS_SCRIPT_URL = "PON_AQUI_TU_URL_DE_APPS_SCRIPT";
   ```
   y sustituye **únicamente el texto entre comillas** por tu URL real. No toques nada
   más en esa zona del código — la comprobación de si está bien configurada es automática.

A partir de ahí:
- La pestaña "Recuerdos" subirá las fotos a la carpeta de fotos y las mostrará en la galería.
- La pestaña "Confirmar asistencia" creará automáticamente, la primera vez que alguien
  confirme, una hoja de cálculo llamada **"Confirmaciones de asistencia - Boda Blanca y Javi"**
  dentro de la carpeta de confirmaciones, con una fila por cada persona: fecha, nombre,
  apellidos, si asiste, acompañante y alergias/condiciones médicas. Podéis abrirla en
  cualquier momento desde Drive como una hoja de Excel normal.

## 4. Publicar la web (para que los invitados puedan entrar desde el móvil)

Necesitas alojar estos archivos en algún sitio con una URL pública. Las opciones más
sencillas y gratuitas:

- **GitHub Pages**: sube la carpeta a un repositorio de GitHub y actívalo en Settings → Pages.
- **Netlify** o **Vercel**: arrastra la carpeta a netlify.com/drop y te da una URL al instante.

## 5. El código QR

En la pestaña "Recuerdos" hay ya un QR de ejemplo. En cuanto tengas la URL definitiva
de la web publicada, genera el QR real en <https://www.qr-code-generator.com> o similar,
apuntando a `TU_URL_DEFINITIVA/#recuerdos`, e imprímelo para las mesas.
También puedes simplemente editar en `index.html` la URL dentro del `src` de `qrImg`
(reemplazando el texto tras `data=` por tu URL codificada).

## 6. Contenido pendiente de completar

En la pestaña "Info útil" he dejado la estructura lista pero con marcadores:

- **Alojamiento**: sustituir las 3 tarjetas de ejemplo por vuestro listado real de hoteles.
- **Restaurantes/chiringuitos**: he puesto sugerencias genéricas de la zona; conviene
  que las confirméis o cambiéis por vuestras recomendaciones concretas.
- **Transporte**: revisad horarios y líneas más cerca de la fecha, pueden cambiar.

## 7. Hora de la ceremonia

Ya está puesta: 12:00 del mediodía, tanto en la sección "La ceremonia" como en la
nueva pestaña "El día".

## 8. Fecha límite para confirmar asistencia

He puesto el **1 de marzo de 2027** como fecha orientativa en el formulario. Cambiadla
en `index.html` (pestaña "Confirmar asistencia") si preferís otra.

## 9. El juego "Atrapa el ramo"

Hay una pestaña nueva con un mini-juego (estilo el dinosaurio de Chrome). Cada partida
guarda el nombre y la puntuación en una hoja de cálculo nueva, **"Puntuaciones del juego
- Boda Blanca y Javi"**, que se crea sola dentro de la misma carpeta de confirmaciones
(`RSVP_FOLDER_ID`) — no hace falta configurar nada adicional si ya tienes el backend
funcionando para las confirmaciones y las fotos.

## 12. Sección "Gracias por acompañarnos" (aportación económica)

Al final de la pestaña "Inicio" hay una sección nueva con hueco para el número de
cuenta, una foto y los teléfonos de contacto. Falta por vuestra parte:

- **Foto**: añadid un archivo `images/fotofinal.jpeg` (mismo nombre exacto, en
  minúsculas) junto a las demás fotos.
- **Número de cuenta**: en `index.html`, busca el texto `IBAN por confirmar` y
  sustitúyelo por vuestro IBAN.
- **Teléfonos**: busca las dos apariciones de `Teléfono por confirmar` (una para
  Blanca, otra para Javi, en ese orden) y pon cada número.

## 13. Solución de problemas

### "La web dice que se ha subido bien pero no aparece en Drive"

Esto pasaba por dos motivos, ya corregidos:

1. **El `FOLDER_ID` no era válido.** Solo debe ir el identificador, sin nada más detrás.
   En una URL como `drive.google.com/drive/folders/1Ymmxt0iYqomcvw4pJ_NUnj6Z7dNKreaf?hl=es`,
   el ID es únicamente `1Ymmxt0iYqomcvw4pJ_NUnj6Z7dNKreaf` — hay que quitar el `?hl=es`.
2. **La web no comprobaba si Drive respondía con error.** Ahora sí lo hace: si algo
   falla, veréis un mensaje de error real en pantalla en lugar de un falso "subido bien".

**Importante:** cada vez que edites el archivo `apps-script.gs` (por ejemplo, para
corregir el FOLDER_ID), tienes que volver a publicarlo para que el cambio surta efecto:

1. En script.google.com, arriba a la derecha, **Implementar → Administrar implementaciones**.
2. Haz clic en el icono de lápiz (editar) de tu implementación.
3. En "Versión", elige **Nueva versión**.
4. Pulsa **Implementar**.

La URL de la aplicación web no cambia, así que no hace falta tocar nada en `index.html`.

### Los errores que salen al abrir la página con doble clic

- `iglesia.jpg` / `finca.jpg` **Failed to load resource**: es normal, es justo el aviso de
  que faltan esas fotos — desaparece en cuanto las añadas en `images/`.
- `Unsafe attempt to load URL file:///... 'file:' URLs are treated as unique security origins`:
  esto ocurre porque estás abriendo el archivo directamente con doble clic
  (`file:///C:/Users/...`). Los navegadores restringen bastante lo que puede hacer una
  página cuando se abre así — los mapas y, sobre todo, la subida de fotos a Drive pueden
  fallar o comportarse de forma rara en este modo. Es solo un aviso de pruebas locales,
  no significa que la web esté rota.

**Para probarla correctamente**, usa alguna de estas opciones en vez de doble clic:
- Publícala ya en Netlify (arrastra la carpeta a netlify.com/drop, tarda 10 segundos) y
  pruébala desde esa URL — es lo más parecido a como la verán los invitados.
- O, si tienes Python instalado, abre una terminal en la carpeta de la web y ejecuta:
  ```
  python -m http.server 8000
  ```
  y visita `http://localhost:8000` en el navegador.