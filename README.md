# Selva

**Para publicar sin Terminal, sigue [PUBLICAR.md](PUBLICAR.md).** El proyecto está preparado para GitHub y Vercel Hobby, sin dependencias ni servicios de pago. Solo necesitas cuentas gratuitas para publicarlo; usar Selva no requiere login.

PWA mobile-first para un roadtrip en van. HTML, CSS y JavaScript vanilla; sin frameworks, dependencias ni compilación. Los datos incluidos son ejemplos, no reservas reales ni una ruta verificada.

## Ejecutar localmente

Desde esta carpeta, con Python 3 instalado:

```sh
python3 -m http.server 8080 --bind 127.0.0.1
```

Abre http://localhost:8080. No abras `index.html` con doble clic: `file://` no permite cargar los JSON ni registrar el service worker correctamente.

## Instalar en iPhone

Publica la carpeta en un alojamiento estático con **HTTPS**, abre su URL en Safari y espera a que Inicio muestre «Lista para acompañarte sin conexión». Pulsa Compartir → Añadir a pantalla de inicio → Añadir (activa «Abrir como app web» si aparece). Abre también la app instalada con conexión una primera vez. Después podrás consultar todas las secciones en modo avión.

Una dirección HTTP de la red local (por ejemplo `http://192.168…`) no es un contexto seguro para el service worker en iPhone. `localhost` sirve para pruebas en el propio ordenador; para probar la PWA desde el teléfono utiliza HTTPS con certificado válido.

## Archivos

- `index.html`: estructura, metadatos iOS y navegación.
- `styles.css`: diseño adaptable, controles táctiles y zonas seguras de iPhone.
- `app.js`: vistas, itinerario expandible y checklist persistente.
- `manifest.json`: instalación, colores e iconos.
- `sw.js`: precarga offline de la app y todos los datos.
- `icons/`: PNG de 192, 512 y 180 píxeles; el de 512 también sirve como maskable.
- `data/trip.json`: título, fechas, kilómetros y viajeros.
- `data/itinerary.json`: días, actividades y lugar de pernocta.
- `data/checklist.json`: categorías y elementos.
- `data/reservations.json`: reservas y referencias; admite una lista vacía.
- `data/van.json`: información de la van y camping.

## Editar el viaje

Edita los JSON con un editor de texto, manteniendo su estructura y usando comillas dobles, sin comentarios ni comas finales. Puedes añadir o quitar días, reservas, categorías y elementos. Los identificadores `id` de categorías y elementos deben ser únicos; mantén los de los elementos para conservar sus marcas. `dates` y las fechas por día son texto libre para poder usar «Día 1» sin fijar un calendario.

El checklist se guarda bajo `selva.checklist.v1` en localStorage, por navegador y origen. No sincroniza dispositivos. Borrar datos del sitio elimina las marcas; el navegador también puede liberar almacenamiento. Si falla el guardado, la app muestra un aviso y mantiene los cambios en memoria durante la sesión. El botón «Desmarcar todo» solicita confirmación antes de reiniciar.

## Offline y actualizaciones

La primera visita requiere conexión y descarga todos los archivos listados en `ASSETS` de `sw.js`. Después utiliza esa copia coherente también con conexión. No hay fuentes, imágenes ni librerías externas.

**Cada vez que cambies código o JSON, cambia `CACHE` en `sw.js`**, por ejemplo de `selva-v2` a `selva-v3`. Si añades un archivo necesario offline, añádelo también a `ASSETS`. Sube todos los archivos juntos. La nueva versión se prepara en segundo plano; cierra todas las pestañas y ventanas de Selva y vuelve a abrir para activarla. Las marcas permanecen. En desarrollo puedes anular el registro del service worker y borrar Cache Storage desde las herramientas del navegador para ver cambios inmediatamente, sin borrar localStorage.

## Desplegar después

Sube **el contenido de esta carpeta** a cualquier alojamiento estático HTTPS. No requiere servidor de aplicación ni paso de build. Usa `index.html` como documento inicial. Las rutas relativas permiten desplegar en la raíz o en una subcarpeta. La navegación utiliza fragmentos (`#itinerario`), así que no necesita reglas de redirección. Sirve `.json` como `application/json` y `.js` como JavaScript; evita cachear `sw.js` a largo plazo (recomendado `Cache-Control: no-cache`).

Los JSON son públicos en el alojamiento: no incluyas contraseñas ni documentos sensibles. La app no se ha publicado automáticamente.

## Comprobación manual

1. Recorre las cinco secciones y expande varios días.
2. Marca elementos en distintas categorías, comprueba el progreso y recarga para verificar persistencia.
3. Cancela y después acepta «Desmarcar todo».
4. Espera el mensaje de disponibilidad offline, desconecta la red y recarga las cinco secciones.
5. En Safari de iPhone, instala y verifica navegación inferior, zonas seguras y uso sin conexión.
6. Publica una nueva versión de caché y comprueba que se activa al cerrar y volver a abrir la app, conservando los checks.
