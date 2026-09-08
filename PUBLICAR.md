# Publicar Selva gratis, sin Terminal

Usaremos un único camino: GitHub personal → Vercel Hobby → Safari del iPhone.
Necesitas cuentas gratuitas de GitHub y Vercel para administrar la publicación. Quienes abran Selva no necesitan cuenta ni iniciar sesión.
Vercel Hobby es gratuito para uso personal y no comercial, sujeto a sus límites. No elijas Pro, no actives pruebas de pago ni compres un dominio: usaremos la dirección gratuita terminada en .vercel.app.

## 1. Subir Selva a GitHub

1. Abre https://github.com y crea tu cuenta gratuita o entra en ella.
2. Pulsa el botón + de arriba y elige New repository.
3. Escribe `selva` como nombre. Usa tu cuenta personal como propietario y selecciona Private.
4. Activa Add a README file y pulsa Create repository.
5. En el repositorio, pulsa Add file → Upload files.
6. En Finder, abre la carpeta `/Users/antonellatarquini/Documents/New project/selva`.
7. Arrastra **el contenido de esa carpeta** al área de subida de GitHub. Incluye las carpetas `data` e `icons`, y todos los archivos visibles, especialmente `vercel.json`. No arrastres la carpeta contenedora `selva`, ni el proyecto de Next.js que está fuera de ella. No necesitas subir archivos ocultos.
8. Pulsa Commit changes para guardar la subida.
9. Comprueba que `index.html`, `app.js`, `styles.css`, `sw.js`, `manifest.json`, `vercel.json`, `data` e `icons` se ven directamente al entrar al repositorio. No deben quedar dentro de otra carpeta.

## 2. Conectar GitHub con Vercel

1. Abre https://vercel.com/signup.
2. Selecciona el uso personal / plan Hobby gratuito y continúa con GitHub.
3. En el panel, pulsa Add New → Project.
4. Si Vercel pide acceso a GitHub, concede acceso solo al repositorio `selva`.
5. Busca `selva` en Import Git Repository y pulsa Import.

## 3. Publicar gratis

1. Usa `selva` como nombre del proyecto; si ya está ocupado, añade tu nombre.
2. Confirma Framework Preset: Other y Root Directory: ./.
3. La configuración incluida deja vacíos los comandos de instalación y compilación, y publica la carpeta raíz. No añadas comandos, variables de entorno, bases de datos ni servicios.
4. Pulsa Deploy y espera a que la publicación termine con estado Ready.
5. En el proyecto, abre Settings → Domains y copia el dominio de producción terminado en `.vercel.app`. Será parecido a `selva-tu-nombre.vercel.app`, pero debes usar el que Vercel te asigne.
6. Abre `https://` seguido de ese dominio en una ventana privada: Selva debe aparecer sin pedir login. Usa siempre este dominio estable, no una URL temporal de vista previa. Las vistas previas de Vercel pueden pedir cuenta aunque la app pública no la pida.

Ya puedes apagar el Mac. Vercel sirve la app por HTTPS sin que tengas que ejecutar nada.

## 4. Abrirla en el iPhone

1. Envía a tu iPhone el enlace HTTPS de producción.
2. Ábrelo en Safari con conexión a Internet.
3. En Inicio, espera el mensaje «Disponible sin conexión».

## 5. Añadirla a la pantalla de inicio

1. En Safari, pulsa Compartir (el cuadrado con la flecha hacia arriba; puede estar dentro del menú Más).
2. Selecciona Añadir a pantalla de inicio.
3. Si aparece Abrir como app web, déjalo activado.
4. Deja el nombre Selva y pulsa Añadir.
5. Abre Selva desde su nuevo icono, todavía con conexión. Espera otra vez el mensaje de disponibilidad offline.
6. Marca un elemento, cierra y vuelve a abrir Selva para comprobar que se conserva.
7. Activa modo avión, desactiva Wi-Fi y abre Selva otra vez. Comprueba las cinco secciones. Después recupera la conexión.

## Tus checklists

Se guardan en el dispositivo, sin base de datos ni sincronización. Las marcas del Mac o de localhost no se trasladan al iPhone. Usa siempre la app instalada y el mismo dominio. Borrar los datos del sitio puede eliminar las marcas; el sistema también puede liberar almacenamiento, así que no es una copia de seguridad permanente.

## Cuando quieras cambiar el viaje

Puedes editar los archivos de `data` en GitHub con el lápiz y guardar con Commit changes. Mantén los identificadores de los elementos para conservar sus marcas. Cada vez que cambies archivos, cambia también `selva-v3` a un nombre nuevo (por ejemplo `selva-v4`) en `sw.js`. Vercel publicará el cambio automáticamente. Abre Selva con conexión para descargarlo, cierra todas sus ventanas y pestañas, y vuelve a abrir para activar la actualización.

Aunque el repositorio sea privado, la app publicada y sus JSON son accesibles sin login. No pongas contraseñas ni documentación privada en ellos.

## Documentación oficial

- GitHub, subir archivos: https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository
- Vercel, conectar un repositorio: https://vercel.com/docs/git
- Vercel, plan gratuito para uso personal: https://vercel.com/pricing
- Vercel, configuración: https://vercel.com/docs/project-configuration/vercel-json
- Apple, añadir una web como app: https://support.apple.com/en-mide/guide/iphone/iphea86e5236/ios
