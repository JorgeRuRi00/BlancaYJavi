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

## 3. Subida de fotos de los invitados a Google Drive

Esto necesita un pequeño "backend" gratuito con Google Apps Script. Son 10 minutos:

1. Crea una carpeta en tu Google Drive, por ejemplo **"Fotos boda Blanca y Javi"**.
2. Ábrela y copia el ID de la URL:
   `drive.google.com/drive/folders/`**`ESTE_TROZO_ES_EL_ID`**
3. Ve a [script.google.com](https://script.google.com) → **Proyecto nuevo**.
4. Borra el contenido de ejemplo y pega el contenido del archivo `apps-script.gs`.
5. En la línea `const FOLDER_ID = "..."`, pega el ID de tu carpeta.
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
   y sustitúyela por tu URL real.

A partir de ahí, la pestaña "Recuerdos" subirá las fotos a esa carpeta de Drive y las
mostrará en la galería automáticamente.

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

Todavía no la has indicado — está como "se avisará próximamente" en el texto de la
ceremonia. Búscalo en `index.html` (sección "La ceremonia") y complétalo cuando lo sepáis.
