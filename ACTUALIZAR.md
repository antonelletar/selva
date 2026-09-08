# Actualizar la Selva que ya tienes publicada

No crees otro proyecto ni cambies los ajustes de Vercel. Usaremos el repositorio y el enlace actuales.

1. En GitHub abre tu repositorio `selva` y pulsa **Add file → Upload files**.
2. En Finder, abre **Ir → Ir a la carpeta…** y pega:

   `/Users/antonellatarquini/Documents/New project/selva`

3. Arrastra **el contenido de la carpeta**, no la carpeta entera. Incluye todos los archivos y las carpetas `data` e `icons`. Son menos de 100 archivos. No subas `node_modules`, `.next` ni archivos del proyecto que está fuera de `selva`.
4. Pulsa **Commit changes** para guardar los reemplazos y los archivos nuevos. Deben quedar `index.html` y `vercel.json` en la raíz. Dentro de `data` deben aparecer también `documents.json` y `shopping.json`.
5. En Vercel → **Deployments**, espera a que la última publicación esté **Ready**. El dominio y los ajustes no cambian.
6. Abre la app con conexión para que descargue la nueva versión. Cierra todas las ventanas y pestañas de Selva, incluida la app instalada, y vuelve a abrirla. Si aún aparece la anterior, repite este paso después de un momento con conexión.
7. Debes ver **SELVA NEGRA 2026**, **19–27 SEP**, nueve días y las nuevas listas. No borres los datos del sitio ni desinstales la app para actualizarla.
8. Desde el icono del iPhone, espera **Disponible sin conexión**, marca un elemento y vuelve a abrir para comprobar que se conserva. Prueba también con modo avión y Wi-Fi apagado.

Esta actualización ya incluye el cambio de caché a `selva-v3`. Solo tendrás que aumentar ese número cuando hagas futuras modificaciones de código o datos.

Tus ediciones dentro de la app se guardan en ese dispositivo. No se suben a GitHub y no necesitan una nueva publicación.
