# OncoFarma Summit · Málaga 2026

App web (PWA) para los asistentes al Encuentro de Farmacéuticos Oncológicos de Bayer.
Hotel Catalonia Molina Lario, Málaga · 12–13 junio 2026.

Una sola página, mobile-first, con estética Liquid Glass. Agenda por días, sesión en
curso resaltada en tiempo real, ponentes, sede con mapa y zona práctica. Instalable en
la pantalla de inicio y **funciona offline** una vez abierta.

---

## Subirla a GitHub Pages

### Opción A — desde la web de GitHub (sin consola)

1. Crea un repositorio nuevo en GitHub (público). Por ejemplo: `oncofarma-summit`.
2. Entra en el repo → **Add file** → **Upload files**.
3. Arrastra **el contenido de esta carpeta** (todos los archivos, incluido `.nojekyll`),
   no la carpeta en sí. El `index.html` tiene que quedar en la raíz del repo.
   > Si `.nojekyll` no aparece al arrastrar, créalo en el repo con **Add file → Create new file**,
   > nómbralo `.nojekyll` y déjalo vacío.
4. **Commit changes**.
5. **Settings** → **Pages** → en *Build and deployment*, Source = **Deploy from a branch**,
   Branch = **main** y carpeta **/(root)** → **Save**.
6. Espera 1–2 minutos. La URL aparece arriba en la misma pantalla de Pages:
   `https://TU-USUARIO.github.io/oncofarma-summit/`

### Opción B — desde consola (git)

```bash
cd oncofarma-summit-2026
git init
git add .
git commit -m "OncoFarma Summit PWA"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/oncofarma-summit.git
git push -u origin main
```

Luego activa Pages igual que en el paso 5 de la Opción A.

---

## Comprobar que va bien

- Ábrela en el móvil (en **Safari/iOS** el efecto cristal luce mejor).
- **Instalar como app:** iOS → Compartir → *Añadir a pantalla de inicio*.
  Android/Chrome → menú → *Instalar aplicación*. Arranca sin barra del navegador.
- **Offline:** ábrela una vez con datos, luego activa modo avión y recárgala.
  Carga todo menos el mapa (el mapa es de Google y necesita conexión).

---

## Editar contenido

Todo está en `index.html`, dentro del `<script>` final.

- **Agenda:** array `SESSIONS`. Cada bloque es
  `S("id", día, "inicio", "fin", "tipo", "Título", ["Ponente 1", "Ponente 2"])`.
  Tipos: `opening`, `talk`, `break`, `meal`, `social`. Las fechas usan formato
  `"2026-06-12T19:45"`. El resaltado “en directo” se calcula solo con la hora del dispositivo.
- **Ponentes:** array `SPEAKERS` (nombre, rol, organización). Los avatares y la vinculación
  con sus sesiones se generan automáticamente a partir del nombre.
- **WiFi:** la app remite a recepción. Si tienes red y clave del evento, búscalas en la
  pestaña Práctico (sección *Conexión*) y sustitúyelas en `index.html`.
- **Sede:** dirección y mapa en la sección `view-sede`. El mapa es un `iframe` de Google
  Maps con la dirección; no requiere API key.

> Si cambias contenido y ya habías visitado la app, sube la versión del cache en
> `service-worker.js` (`oncofarma-summit-v1` → `v2`) para que se actualice en los dispositivos.

---

## Dominio propio (opcional)

En **Settings → Pages → Custom domain** puedes apuntar un dominio o subdominio
(p. ej. `summit.ncompany.es`) y añadir el registro CNAME en tu proveedor de DNS.
Las rutas de la app son relativas, así que funciona igual en subdirectorio que en dominio raíz.

---

## Archivos

| Archivo | Para qué |
|---|---|
| `index.html` | La app completa (HTML + CSS + JS, autocontenido) |
| `manifest.webmanifest` | Metadatos PWA: nombre, iconos, color, modo standalone |
| `service-worker.js` | Cache y funcionamiento offline |
| `icon-192/512.png` | Iconos de app (uso normal) |
| `icon-192/512-maskable.png` | Iconos adaptables (Android) |
| `apple-touch-icon.png` | Icono en pantalla de inicio de iOS |
| `favicon.svg` / `favicon.png` | Icono de pestaña del navegador |
| `.nojekyll` | Evita que GitHub Pages procese los archivos con Jekyll |

---

Un evento de Bayer · Farmacéuticos Oncológicos para Farmacéuticos Oncológicos.
