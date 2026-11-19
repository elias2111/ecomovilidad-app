# EcoMovilidad (app móvil)

App móvil de **EcoMovilidad Colombia S.A.S.** para el área metropolitana de Bucaramanga (Bucaramanga, Floridablanca, Girón y Piedecuesta): tienda, alquiler de flota, domicilios con domiciliario o dron y panel de operación, en una app que se instala en el iPhone como cualquier otra.

- **Abrir la app:** https://elias2111.github.io/ecomovilidad-app/
- **Repositorio de la web (portal Next.js + FastAPI):** https://github.com/santrolop1/ecomovilidad

La app implementa los mismos casos de uso que la web (CU-01 a CU-17) y se parece a ella, pero funciona sola en el teléfono: no necesita servidor. Los datos son de demostración, la pasarela de pagos y el GPS son simulados.

## Instalar en el iPhone

1. Abre https://elias2111.github.io/ecomovilidad-app/ en **Safari**.
2. Toca **Compartir** → **Agregar a pantalla de inicio** → **Agregar**.
3. Ábrela desde el ícono: se ve a pantalla completa, sin barra del navegador, y después de la primera visita funciona sin conexión.

En Android, ábrela en Chrome y, en el menú, toca **Instalar app** o **Agregar a la pantalla principal**.

## Cuentas de demostración

| Rol | Correo | Contraseña |
| --- | --- | --- |
| Cliente | cliente@ecomovilidad.co | Cliente123 |
| Cliente 2 | laura@ecomovilidad.co | Laura1234 |
| Administrador | admin@ecomovilidad.co | Admin123 |
| Domiciliario | domiciliario@ecomovilidad.co | Domi1234 |

También puedes crear una cuenta nueva de cliente. En **Cuenta → Casos de uso** está la lista de los 17 casos: tocar uno entra directo con el rol correcto.

## Tecnologías

| Área | Tecnologías |
| --- | --- |
| App | HTML, CSS y JavaScript sin frameworks, en un solo archivo (`index.html`) |
| Instalación | PWA: `manifest.webmanifest`, íconos y `sw.js` (funciona sin conexión) |
| Datos | `localStorage` del teléfono; cada teléfono tiene sus propios datos |
| Mapas | Mapa propio en SVG del área metropolitana, con geocercas y posiciones en vivo |
| GPS | Simulado: cada dispositivo se mueve y reporta su posición cada 3 segundos |
| Pagos | Pasarela de pruebas dentro de la app y pago manual (transferencia o efectivo) que confirma el administrador |
| Otros | Códigos QR con qrcode-generator y lectura con la cámara con jsQR (incluidas en la app, sin internet); tipografías Archivo e IBM Plex Mono; modo claro y oscuro |
| Publicación | GitHub Pages |

## Qué probar

- **Compra:** agrega al carrito (queda reservado 15 minutos), elige domicilio o **recogida en sucursal**, fecha y franja, y paga en la pasarela de pruebas. La factura queda en *Pedidos*.
- **Domicilio con domiciliario:** como administrador, en *Domicilios* asigna un domiciliario, avanza los estados y confirma la entrega con el código QR del cliente o con su firma. El cliente sigue el avance en el mapa.
- **Escanear el QR:** el cliente abre su pedido (por ejemplo EM-1002) y muestra el QR. El domiciliario, en *Entregas › Confirmar entrega*, toca *Escanear con la cámara*. Si el iPhone no da permiso de cámara, *Tomar foto del QR* abre la cámara del sistema; también se puede escribir el código de 6 caracteres. Los pedidos de ejemplo tienen el mismo código en todos los dispositivos, así que el QR de un teléfono sirve en otro.
- **Domicilio con dron:** en *Domicilios*, el pedido EM-1004 se puede asignar a un **dron**: elige cuál y toca el mapa para marcar el punto exacto de entrega. El dron vuela solo y suelta el paquete únicamente si su GPS está a 50 m o menos del punto. Entonces el cliente ve **"Recibí mi pedido"** o **"No lo encuentro"**; si en 30 minutos no confirma ni reclama, el panel cierra con la evidencia del dron. El pedido EM-1008 del cliente ya viene volando: en un minuto aparece el botón de confirmar.
- **Seguimiento de flota:** en *Operación* están el mapa en vivo y la lista de vehículos de alquiler, domiciliarios y **drones de domicilio**, cada uno con lo que está haciendo ("Llevando un domicilio…", "Alquilada hasta…", "En taller", "Disponible").
- **Alquiler y recogida en sucursal:** en *Alquiler* eliges vehículo, sucursal y fechas, y pagas. En el panel (*Gestión → Pedidos y alquileres*), la sucursal **registra la salida** del vehículo; desde ese momento aparece como **no disponible** y no se puede entregar a otro cliente. Al volver, **registra la entrada** con los km u horas de uso. El alquiler EM-1009 está listo para probarlo.
- **Mantenimiento:** en *Gestión → Flota de alquiler* cada unidad tiene dos límites: el uso (sale de la oferta al 90 % del umbral) y el **tiempo** (revisión cada 90 días; drones cada 60, editable). El panel muestra las próximas revisiones y saca sola la unidad cuando vence; vuelve al registrar el mantenimiento.
- **Pago manual:** al pagar elige *Pago manual*. Ves las instrucciones, la referencia y el plazo (24 horas). El administrador lo confirma o lo marca como no recibido en el detalle del pedido; el panel muestra cuántos hay por confirmar.
- **Contacto:** en *Cuenta → Contacto* (o al final del inicio) escribe un mensaje. El administrador lo ve en *Gestión → Mensajes de contacto* y lo marca como atendido.
- **Catálogo y tienda desde el panel:** en *Gestión* el administrador edita **productos** (precio, precio anterior, descripción, destacados, publicado), **categorías** (nombre, descripción, visible), **sucursales** (crear o editar, con ubicación tocando el mapa, servicios y cupo por franja) y **usuarios** (buscar, ver sus pedidos, activar o desactivar la cuenta).
- **Domiciliarios y dispositivos GPS:** en *Gestión* agrega domiciliarios (cada uno recibe su GPS) y registra dispositivos: drones de domicilio, GPS de domiciliario o de vehículo. El token se muestra una sola vez; desactivar un dispositivo lo saca del mapa.
- **Nosotros y servicios:** páginas con los compromisos legales y cómo avanza un domicilio.
- **Zonas y alertas:** en *Gestión → Zonas y alertas* crea una geocerca tocando el mapa y usa *Probar alerta*.
- **Reembolso, inventario y contenidos:** el cliente cancela o pide reembolso; el panel lo registra, ajusta existencias y edita banners, propuesta de valor y noticias.

Para volver a los datos iniciales: *Cuenta → Ajustes → Borrar datos de la app*.

## Estado por caso de uso

| Caso de uso | Estado | Cómo se hace en la app |
| --- | --- | --- |
| CU-01 Registro e inicio de sesión | Hecho | Correo y contraseña; bloqueo tras 5 intentos fallidos; el administrador puede desactivar cuentas |
| CU-02 Catálogo | Hecho | Filtros por categoría, marca y precio; productos y categorías editables en el panel |
| CU-03 Compra | Hecho | Reserva de 15 minutos al agregar al carrito |
| CU-04 Alquiler | Hecho | Sin cruces de horario; no ofrece unidades afuera, en taller o con revisión vencida |
| CU-05 Pago | Hecho | Pasarela de pruebas o pago manual confirmado por el panel; factura en PDF y XML de muestra |
| CU-06 Agendar entrega o recogida | Hecho | Cupo por sucursal y franja |
| CU-07 Seguimiento del domicilio | Hecho | Enlace público con la posición del domiciliario o del dron |
| CU-08 Validar entrega | Hecho | QR escaneado con la cámara (o con una foto, o el código escrito), firma o, con dron, GPS del punto de entrega más confirmación del cliente |
| CU-09 Contenidos | Hecho | Banners, propuesta de valor y noticias con vista previa |
| CU-10 Monitoreo de flota | Hecho | Vehículos, domiciliarios y drones con su actividad; GPS simulado |
| CU-11 Geofencing | Hecho | Zonas circulares; la alerta se abre al salir y se cierra al volver |
| CU-12 Mantenimiento | Hecho | Por uso y por tiempo, con bitácora que no se puede alterar |
| CU-13 Inventario | Hecho | Ajustes por sucursal y movimientos |
| CU-14 Gestionar domicilios | Hecho | Asignar domiciliario o dron, avanzar, marcar fallido y reprogramar |
| CU-15 Cancelación y reembolso | Hecho | El cliente lo pide y el panel lo registra |
| CU-16 Recibir pedido con dron | Hecho | Liberación a 50 m o menos y botón "Recibí mi pedido" |
| CU-17 Salida y entrada en sucursal | Hecho | Mientras el vehículo está afuera aparece como no disponible |

## Novedades (noviembre de 2026)

1. **Domicilios con dron y prueba de entrega:** el GPS del dron registra dónde soltó el paquete y el cliente lo confirma.
2. **Seguimiento del administrador:** vehículos, domiciliarios y drones de domicilio en el mapa y en la lista.
3. **Recogida en sucursal con registro de salida y entrada:** un vehículo afuera no aparece disponible.
4. **Mantenimiento cada cierto tiempo** en el panel, además del mantenimiento por uso.
5. **Igual que la web (`main`):** pago manual, formulario de contacto con bandeja en el panel, páginas Nosotros y Servicios, inicio con área de cobertura y accesos por categoría, y gestión de productos, categorías, sucursales, usuarios, domiciliarios y dispositivos GPS.

Los mismos cambios están en la rama `main` de la web: https://github.com/santrolop1/ecomovilidad. Los diagramas actualizados (casos de uso, secuencia, clases con interfaz/control/entidad, paquetes, componentes y nodos) se entregan aparte en *Diagramas-EcoMovilidad.pdf*; no están en este repositorio.

## App y web

| | App (este repositorio) | Web (santrolop1/ecomovilidad) |
| --- | --- | --- |
| Dónde corre | En el teléfono, sin servidor | Next.js + FastAPI + PostgreSQL/PostGIS |
| Datos | De demostración, guardados en el teléfono | Base de datos compartida |
| GPS | Simulado | Dispositivos reales o simulador (`scripts/simulate_gps.py`) |
| Pagos | Pasarela de pruebas o pago manual | Pasarela de pruebas, pago manual o Wompi |
| Para qué sirve | Mostrar y probar todo desde el iPhone | El sistema completo, listo para desplegar |

## Archivos

```
index.html              La app completa (pantallas, reglas y datos de demostración)
manifest.webmanifest    Nombre, colores e íconos para instalarla
sw.js                   Guarda la app para usarla sin conexión
icon-*.png              Íconos del iPhone y de Android
```

## Actualizar la app

1. Sube el nuevo `index.html` (y `sw.js` si cambió) a la rama `main`.
2. GitHub Pages publica en 1 o 2 minutos.
3. En el iPhone, cierra la app y ábrela otra vez; si sigue igual, ciérrala y ábrela una vez más.

Si cambian los datos de demostración, la app vuelve a cargarlos sola y se pierden los pedidos de prueba guardados en ese teléfono.

## Límites

- Los datos no se comparten entre teléfonos: cada uno tiene su propia copia.
- El GPS, los pagos, los correos y los SMS son simulados (los avisos aparecen dentro de la app).
- La factura es de muestra; no es factura electrónica DIAN.

Las sucursales, productos y datos de contacto son **datos de demostración**. Las fotos de producto provienen de Wikimedia Commons.

Proyecto de José Elías Cruz y Santiago Cabeza Méndez, Universidad Autónoma de Bucaramanga.
