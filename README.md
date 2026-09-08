# Selva Negra 2026

App de viaje para el roadtrip del 19 al 27 de septiembre de 2026: Barcelona, Selva Negra, Alsacia y Suiza. Coche propio, 9 días y 8 noches.

Se conserva la estructura estática original: HTML, CSS y JavaScript vanilla, sin frameworks, dependencias, backend, cuentas ni base de datos externa. `vercel.json` conserva la configuración de publicación en Vercel.

## Actualizar la app ya publicada

Sigue [ACTUALIZAR.md](ACTUALIZAR.md). Para una primera publicación, consulta [PUBLICAR.md](PUBLICAR.md).

## Uso

- **Inicio:** día actual o próxima etapa, cuenta atrás antes de salir, preparación real, reservas no confirmadas y tres pendientes importantes. La fecha usa Europe/Madrid, compartida en septiembre con los destinos del viaje. Al volver a la app o cambiar el día se actualiza la selección. Después del viaje muestra el regreso.
- **Itinerario:** nueve tarjetas cerradas por defecto, con el día actual destacado. Estado manual (Pendiente, Listo, Completado), origen, destino, alojamiento vinculado a Reservas, plan, notas editables y checklist diaria independiente.
- **Checklist:** 198 elementos iniciales en 13 categorías plegables. Buscar, marcar, editar/eliminar desde el botón de tres puntos y añadir elementos. Desmarcar por categoría o toda la preparación con confirmación. El porcentaje se calcula sobre los elementos generales existentes, incluidos los añadidos y excluidos los eliminados.
- **Reservas:** cinco alojamientos con los estados comunicados, sin confirmaciones inventadas. Edita nombre, dirección, entrada/salida, precio total en euros, estado, referencia, notas, enlace, parking y horarios. La home cuenta como pendientes todas las que no estén en Confirmado.
- **Van/Camping:** listas de llegada y desmontaje independientes de los días y de la preparación general.
- **Compras:** acceso desde Inicio y Checklist; lista inicialmente vacía. Nombre, categoría, cantidad, precio estimado total, precio real total y comprado. Los precios son opcionales, en euros y por compra completa, no por unidad. Los totales solo se muestran cuando hay importes registrados; si faltan importes se indica que son parciales.
- **Documentos:** acceso desde Inicio y Reservas. Siete categorías con marca de preparado y notas/referencias; sin subida de documentos.

Confirmar una reserva no marca automáticamente su tarea en preparación: el estado del alojamiento y la lista general son controles distintos. Los estados de los días también se eligen manualmente.

## Persistencia

Las ediciones y marcas se guardan en `localStorage` bajo `selva.roadtrip.2026.v1`. Preparación, tareas diarias, camping, reservas, compras y documentos usan campos independientes. Los datos JSON originales no se modifican al editar desde la interfaz.

El registro anterior `selva.checklist.v1` se conserva sin borrar. Una migración inicial importa algunas marcas compatibles de documentación, ropa y descanso; no reutiliza indiscriminadamente los identificadores de la lista anterior para el nuevo viaje. Las nuevas personalizaciones se aplican por identificador: conserva los IDs al cambiar los JSON. Las ediciones locales tienen prioridad sobre el dato base correspondiente.

El guardado pertenece al navegador y dominio. No se sincroniza entre Mac e iPhone ni entre localhost y Vercel. Si el dispositivo impide guardar, se muestra un aviso permanente; si los datos almacenados no se pueden leer, no se sobrescriben. Borrar los datos del sitio o la liberación de almacenamiento del sistema puede eliminar la información local.

## Datos editables

- `data/trip.json`: datos generales.
- `data/itinerary.json`: nueve etapas, planes y tareas por día.
- `data/checklist.json`: categorías y elementos de preparación.
- `data/reservations.json`: alojamientos y estados iniciales.
- `data/van.json`: llegada y desmontaje.
- `data/documents.json`: categorías de referencias.
- `data/shopping.json`: lista inicial vacía; las compras se crean en la app y se guardan localmente.

Las reservas enviadas o planteadas no se consideran confirmadas. Los precios objetivo y los 8–10 km de senderismo son los indicados en el plan del viaje, no cotizaciones ni una ruta comprobada. Horarios, rutas, aparcamientos y alojamientos que aún no se han cerrado permanecen pendientes.

## Offline y PWA

`manifest.json` mantiene `id`, `start_url`, `scope`, iconos y modo standalone. `index.html` conserva los metadatos iOS y las zonas seguras. La barra inferior conserva las cinco pestañas originales.

`sw.js` usa la caché `selva-v3`. Precarga la app, los iconos y todos los JSON. Tras la primera carga completa por HTTPS, permite consultar y editar todos los datos locales sin conexión. Las páginas externas enlazadas y los mapas de otras apps no se descargan automáticamente.

Al actualizar código o datos base, cambia la versión de caché (por ejemplo de `selva-v3` a `selva-v4`) y sube todos los archivos modificados. La actualización se descarga con conexión y se activa después de cerrar todas las ventanas de Selva y volver a abrir. No se fuerza una recarga durante una edición. `vercel.json` evita caché HTTP prolongada y el registro del service worker no reutiliza una copia HTTP antigua.

En iPhone abre el dominio HTTPS de producción en Safari, pulsa Compartir → Añadir a pantalla de inicio y activa Abrir como app web si aparece. Abre también el icono instalado con conexión hasta ver «Disponible sin conexión». Luego prueba modo avión. No hace falta reinstalar para recibir esta actualización ni borrar el almacenamiento.

## Ejecutar localmente, opcional

Desde esta carpeta:

```sh
python3 -m http.server 8080 --bind 127.0.0.1
```

Abre http://localhost:8080. No abras el HTML con doble clic: los JSON y el service worker necesitan HTTP local o HTTPS. Para usarla en viaje basta la dirección publicada; no necesitas mantener el ordenador encendido.

## Verificación realizada

- Sintaxis JavaScript, JSON, IDs únicos, vínculos día/alojamiento y recursos de precarga completos.
- Selección de la home antes, durante y después del viaje; nueve días, cinco reservas y 198 elementos generales.
- Navegación por las cinco pestañas y acceso a Compras/Documentos.
- Búsqueda, edición y guardado de checks; alta de elementos; estado diario; camping; edición de reservas; cálculos de pendientes y compras; notas de documentos.
- Recarga con servidor local detenido: itinerario, referencias y reservas conservados; alta de un elemento y edición de reserva sin servidor, persistentes al recargar.
- Anchuras móviles de 390 y 320 px sin desbordamiento horizontal y revisión visual de la home.

Pruebas realizadas en un origen local separado, sin alterar las marcas del dominio publicado. Queda por verificar la nueva versión instalada en Safari de un iPhone físico después de subirla a GitHub/Vercel.
