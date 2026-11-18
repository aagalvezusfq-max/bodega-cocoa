# PRD — Bodega COCOA

- **Versión:** 1.0 · 18 de noviembre de 2026
- **Equipo:** Andrés Gálvez
- **Cliente:** Santiago, administrador de la Bodega COCOA. En la entrevista, su jefe Luis Daniel revisa el proyecto. En la visita del 11 de noviembre no se dijo que Luis Daniel apruebe cada reserva.
- **Fuentes:** resúmenes de la entrevista, recogidos en el documento de preguntas del avance 1, y la visita del cliente del 11 de noviembre de 2026 (`Notas Cliente.txt`). Si la visita contradice un resumen, manda la visita. Si nadie lo dijo, está en la sección 7 y no es un hecho.

## 1. Problema y objetivo

Santiago administra los préstamos de equipos de cine, periodismo y comunicación. El lugar que nombró en clase es la Bodega COCOA. Hoy la página no le sirve al estudiante ni a él. El estudiante arma el pedido como un carrito, el carrito se borra y no puede pedir más de un artículo. Le cuesta entrar, no recupera la clave con facilidad y no recibe ningún aviso. Termina buscándolo: Santiago atiende alrededor de diez personas por hora y completa la reserva a mano. Los correos personales no permiten saber si la persona sigue en la universidad.

**Objetivo:** que el estudiante arme solo una reserva con los objetos que necesita, vea en qué estado está y reciba un correo cuando se aprueba, cuando no retira a tiempo y cuando vence la entrega. El administrador aprueba o rechaza, anota quién se lleva el equipo y marca mantenimiento o daño, sin rehacer el pedido en el mostrador.

## 2. Usuarios

| Perfil | Quién es | Qué necesita hacer |
| --- | --- | --- |
| Estudiante | Persona con cuenta creada por un administrador. Solo puede reservar objetos de su carrera y su semestre; eso lo verifica el administrador. El cliente no dijo el dispositivo: se asume celular y computador (S12). | Ver el catálogo y las fechas, armar una reserva con varios objetos, explicar para qué los usa, seguir el estado, ver su historial, cancelar a tiempo y mostrar el comprobante al retirar y al devolver. |
| Administrador | Personal de la bodega. Tienen que ser mínimo dos, con los mismos permisos. Santiago es quien hoy presta los equipos. | Crear y editar el catálogo, aprobar o rechazar, escribir notas de la reserva y del estudiante, marcar mantenimiento y daño, confirmar el retiro y la devolución, y crear cuentas. |

No hay un tercer perfil. Luis Daniel no quedó confirmado como usuario del día a día (S20 habla de la baja de cuentas, no de un rol distinto).

## 3. Alcance del MVP

1. Iniciar sesión con correo institucional y contraseña, y cerrar la sesión al cumplirse una hora.
2. Crear cuentas de estudiante, con carrera y semestre, y cuentas de administrador.
3. Ver el catálogo de objetos y equipos, con foto, cantidad disponible y si está en mantenimiento.
4. Armar una reserva con varios objetos y sus cantidades, la fecha y hora de inicio, la fecha y hora de fin, y el uso que se les va a dar.
5. Enviar la reserva y seguirla en pendiente hasta que un administrador la apruebe o la rechace.
6. Ver el historial de las reservas propias y el estado de cada una.
7. Cancelar una reserva hasta una hora antes de la devolución prevista, si el equipo todavía no se retiró.
8. Ver el comprobante con los objetos, las cantidades y las fechas de inicio y fin.
9. Aprobar o rechazar la reserva completa, viendo carrera, semestre, uso declarado y las notas internas.
10. Crear y editar el catálogo, con foto, cantidad y valor, y marcar mantenimiento o daño.
11. Confirmar el retiro y la devolución.
12. Si pasan 30 minutos sin retirar, pasar la reserva a no retirada, liberar el objeto y avisar por correo.
13. Avisar por correo cuando la reserva se aprueba y cuando vence la fecha de entrega.
14. Leer una página de preguntas frecuentes sobre cómo reservar, retirar y devolver.
15. Actualizar solos el catálogo, las reservas y los avisos, sin recargar la página a mano.

## 4. Reglas de negocio

1. Solo entra quien tiene cuenta. Las cuentas las crea un administrador. No hay registro abierto. *(entrevista, no contradicha; los datos de la cuenta están en S1)*
2. Operan como mínimo dos administradores y cualquiera de los dos puede hacer todo lo del perfil administrador. *(visita, 11 nov)*
3. El estudiante solo puede reservar objetos de su carrera y su semestre. Si el objeto no corresponde, lo ve en el catálogo con el texto «No corresponde a tu carrera» y no puede agregarlo. El administrador ve carrera y semestre al decidir. *(visita; la forma de marcarlo está en S17)*
4. Una reserva puede incluir varios objetos, hasta todos los de la bodega. Un objeto que se presta por cantidad —el ejemplo del cliente fue 30 trípodes— es un solo objeto con una cantidad, no treinta reservas. *(visita)*
5. El estudiante puede tener varias reservas a la vez. *(visita)*
6. Cada reserva lleva fecha y hora de inicio, fecha y hora de fin, y un texto de para qué se usa el equipo. Sin ese texto no se puede enviar. No hay anticipación mínima ni duración máxima: puede cubrir todo el semestre. *(visita; el formato de fecha y hora está en S23)*
7. La fecha y hora de fin no puede caer en sábado ni en domingo. No se devuelven objetos en días fuera de trabajo. *(visita; qué días son «fuera de trabajo» está en S16)*
8. La sesión del estudiante permanece abierta como máximo una hora, para que un objeto no se quede en espera. Si se cumple la hora y la reserva no se envió, los objetos elegidos dejan de estar apartados. *(visita)*
9. Una reserva enviada y todavía pendiente no descuenta la cantidad. El administrador elige a quién aprobar. Si en ese momento ya no hay cantidad, el sistema no deja aprobar y lo explica. *(S2: el cliente no dijo quién gana si dos lo piden a la vez)*
10. Al aprobar, la cantidad queda apartada. *(consecuencia de la regla 12, que el cliente sí dijo: si no se retira, el objeto vuelve a aparecer disponible)*
11. Estados de una reserva, y el único camino entre ellos:

| Desde | Hacia | Cuándo |
| --- | --- | --- |
| Sin enviar | Se descarta | Pasó la hora de la sesión (regla 8) |
| Sin enviar | Pendiente | El estudiante la envía |
| Pendiente | Aprobada | Un administrador la aprueba y hay cantidad |
| Pendiente | Rechazada | Un administrador la rechaza, con motivo (S3) |
| Pendiente | Cancelada | El estudiante cancela, hasta 1 hora antes del fin |
| Aprobada | En préstamo | El administrador confirma el retiro dentro de los 30 minutos |
| Aprobada | No retirada | Pasaron 30 minutos sin retiro |
| Aprobada | Cancelada | El estudiante cancela, hasta 1 hora antes del fin, y todavía no retiró |
| En préstamo | Devuelta | El administrador confirma la devolución |
| En préstamo | Vencida | Llegó la fecha de fin y no se ha devuelto |
| Vencida | Devuelta | El administrador confirma la devolución atrasada |

Rechazada, cancelada, no retirada y devuelta no cambian más. Los nombres en pantalla y sus colores están en `DESIGN.md`.

12. Desde la hora de inicio, el estudiante tiene 30 minutos para retirar. Si el administrador aprueba después de esa hora, los 30 minutos corren desde la aprobación. Si no retira, la reserva pasa a no retirada, la cantidad vuelve a estar disponible y se envía un correo. *(visita; desde cuándo corre el reloj está en S4)*
13. El administrador confirma el retiro cuando el estudiante ya revisó el equipo en persona. La reserva pasa a en préstamo. La firma del documento de responsabilidades sigue en papel. *(visita; que el clic lo haga el administrador está en S5)*
14. El administrador confirma la devolución cuando el estudiante vuelve con el comprobante. Si la reserva estaba vencida, al devolverla queda devuelta y se anota el retraso en la descripción del estudiante (regla 20). *(visita y S5)*
15. Si llega la fecha de fin y la reserva sigue en préstamo, pasa a vencida y se envía un correo al estudiante. *(visita)*
16. El estudiante puede cancelar solo si el equipo todavía no se retiró, y solo hasta una hora antes de la fecha y hora de fin. *(visita; el caso «ya lo retiró» está en S6)*
17. Una hora antes de la fecha de fin, la cantidad de una reserva en préstamo vuelve a poder reservarse, aunque el primer estudiante todavía no haya devuelto. *(visita: dijo una hora antes o media hora antes; se usa 60 minutos, S7)*
18. Si el valor registrado del objeto supera los 500 dólares, la reserva lo incluye y además lo anota como otro objeto extra, con el mismo nombre y las mismas fechas. El estudiante ve esa segunda línea y no ve el monto. No es un cobro. *(visita; S8)*
19. El administrador puede marcar un objeto en mantenimiento. Mientras lo esté, nadie lo reserva y el catálogo dice «En mantenimiento». *(visita)*
20. Hay que penalizar a quien devuelve tarde o devuelve el equipo dañado. En esta versión la penalización es una nota en la descripción del estudiante, visible solo para los administradores. El sistema no bloquea solo las reservas nuevas. Si el equipo está dañado, el administrador lo marca: ese estado solo lo ve él y el objeto deja de aparecer para los estudiantes. *(visita; en qué consiste la pena, S9)*
21. El administrador puede escribir notas en la reserva, para saber quién reserva y para qué, y una descripción del estudiante, por ejemplo si ya dañó algo. Ninguna de las dos la ve el estudiante. *(visita)*
22. El rechazo lleva un motivo escrito. El estudiante lo lee en la reserva y lo recibe por correo. *(S3: en clase quedó el correo de aprobación, no el de rechazo)*
23. Los correos del sistema son tres, además del de rechazo de la regla 22: al pasar a aprobada, al pasar a no retirada y al pasar a vencida. No se envía un correo al enviar la solicitud. El WhatsApp, si el equipo no vuelve, lo escribe el administrador por su cuenta y el sistema no lo manda. *(visita)*
24. El estudiante ve el historial de sus reservas y un comprobante con objetos, cantidades y fechas de inicio y fin. *(visita)*
25. El catálogo lo crea y lo edita el administrador. Cada objeto tiene nombre, cantidad, valor, carreras y semestres permitidos, y hasta dos fotos. *(visita; el tope de dos fotos está en S11)*
26. El daño, el mantenimiento, las notas y el valor no se muestran al estudiante, salvo el texto «En mantenimiento» cuando el objeto sigue visible pero no se puede reservar. El objeto dañado no se muestra. *(visita y S8)*

## 5. Fuera de alcance

| Lo que se mencionó | Por qué no entra |
| --- | --- |
| Chatbot que responda dudas | El cliente dijo que no es indispensable. Si era difícil, bastaba una sección de preguntas frecuentes. Esa sección sí entra (alcance 14). |
| Avisos por WhatsApp | El administrador los escribe por su cuenta cuando el equipo no se devuelve a tiempo. |
| Avisarle al guardia de seguridad quién está aprobado | Lo planteó para más adelante, junto con dejar los papeles. |
| Quitar la firma en papel | El estudiante sigue revisando el equipo y firmando en persona. El sistema muestra el comprobante; no reemplaza la firma. |
| Reporte en Excel | Lo pedían algunos resúmenes de la entrevista. En la visita no habló de reportes. El administrador ve las reservas en pantalla. |
| Cargar el inventario desde un Excel | En la visita el catálogo se crea y se edita en el sistema. No mencionó el archivo. |
| Espacios, incluido el estudio de televisión | En la visita no habló de espacios. Nombró la Bodega COCOA y su catálogo de objetos y equipos. Queda abierto en S13. |
| App nativa | No la pidió. La web cubre celular y computador (S12). |
| Cobro del préstamo | No dijo que el estudiante pague. Los 500 dólares no son una tarifa (S8). |
| Elegir una unidad física por número de serie | Dijo que 30 trípodes cuentan como un solo objeto. No dijo que la cámara se reserve por número (S10). |
| Aprobar solo una parte de la reserva | No dijo qué pasa si solo se puede prestar una parte. Se aprueba o se rechaza entera (S18). |

## 6. Decisiones del cliente

Todas son de la visita del 11 de noviembre de 2026. La visita pesa más que los resúmenes de la entrevista.

| # | Decisión | Cambió o confirmó |
| --- | --- | --- |
| D1 | No hay límite de uso. Hay quien se queda un equipo todo el semestre. El estudiante explica para qué lo va a usar. | Corrige la entrevista, que hablaba de franjas como 8:30 a 17:20 o «hasta la madrugada», sin cerrar la duración. |
| D2 | No hay tiempo de anticipación para reservar. | Cierra un vacío de la entrevista. |
| D3 | Una reserva puede incluir todos los objetos de la bodega. El estudiante también puede reservar varias veces. El administrador le consulta cuántos necesita, para no abrir varias reservas. | Corrige el fallo del carrito, que no dejaba más de un artículo. |
| D4 | El administrador aprueba o rechaza. Tienen que ser mínimo dos administradores. | Corrige la idea de un solo administrador. No nombró a Luis Daniel como uno de ellos. |
| D5 | El estudiante solo reserva objetos de su semestre y su carrera. Lo verifica el administrador. | Precisa quién puede reservar. No habló de profesores ni de monitores. |
| D6 | Hay 30 minutos para retirar. Si el estudiante tarda, el objeto vuelve a aparecer disponible y se le avisa por correo. | Nuevo: no estaba en la entrevista. |
| D7 | Correo al estudiante cuando se aprueba la reserva, cuando retira tarde y cuando vence la fecha de entrega. Si no devuelve, el WhatsApp lo manda el administrador por su cuenta. | Precisa los avisos. No pidió un correo de «recibimos tu reserva». |
| D8 | El tiempo máximo para cancelar la reserva es una hora antes de la devolución. Ese día, una hora antes o media hora antes, el objeto ya podría reservarse otra vez. | Nuevo. La elección entre una hora y media hora queda en S7. |
| D9 | No se pueden devolver objetos en días fuera de trabajo. | Nuevo. No dijo si se puede reservar un sábado para usarlo, ni enumeró los festivos. |
| D10 | Hay objetos por cantidad. Treinta trípodes cuentan como un solo objeto. | No cerró si una cámara repetida se elige por número (S10). |
| D11 | Si el objeto de la reserva pasa de 500 dólares, se anota como otro objeto extra reservado. | No dijo si el préstamo se cobra ni si el estudiante ve el valor (S8). |
| D12 | Se penaliza devolver tarde o devolver el equipo dañado. El daño lo marca el administrador, solo él lo ve, y el objeto sale del catálogo de los estudiantes. | No definió un bloqueo automático (S9). |
| D13 | El administrador marca si un objeto está en mantenimiento, crea y edita el catálogo, escribe notas de quien reserva y una descripción del estudiante. | Confirma que el catálogo vive en el sistema. |
| D14 | El estudiante mira el catálogo, luego las fechas disponibles, y espera la aprobación. Puede ver su historial. Se lleva un comprobante con lo retirado y las fechas. Antes de la entrega revisa el equipo y firma en persona. | Confirma el recorrido. Dejar el papel y avisar al guardia lo dejó para más adelante. |
| D15 | La sesión solo puede quedar abierta una hora, para que un objeto no se quede en espera. | Nuevo. |
| D16 | Hay que poner fotos de Google de los equipos. Objetos, equipos y notificaciones se recargan solos. Lo mencionó como un sistema con React. | Nuevo como condición de la interfaz. No dijo celular o computador (S12). |
| D17 | Un chatbot de dudas no es indispensable. Si no se puede, deja una sección de preguntas frecuentes. | Saca el chatbot de esta versión y deja las preguntas frecuentes. |
| D18 | El lugar se llama Bodega COCOA. | No habló del estudio de televisión ni de Miguel de Santiago (S13). |

## 7. Supuestos y preguntas abiertas

| # | Pregunta abierta | Supuesto mientras tanto |
| --- | --- | --- |
| S1 | Al crear la cuenta, ¿qué datos se anotan y cómo llega la primera clave? Tampoco describió la falla actual al entrar. | Nombre, correo institucional, código, carrera y semestre. El administrador pone una clave temporal y el estudiante la cambia al entrar. Puede pedir otra clave por correo, sin escribirle a Santiago. No se copia el fallo de la página vieja. |
| S2 | Si dos estudiantes piden el mismo objeto antes de que haya una respuesta, ¿de quién es? | La reserva pendiente no descuenta la cantidad. Al aprobar, si ya no hay, el sistema no deja aprobar. El administrador elige el orden. |
| S3 | Si rechaza, ¿el estudiante lee el motivo? ¿Le llega un correo? | El motivo es obligatorio y visible. También se envía por correo. En clase solo quedó confirmado el correo de aprobación. |
| S4 | Los 30 minutos para retirar, ¿desde la aprobación o desde la hora de inicio? | Desde la hora de inicio. Si la aprobación es posterior, desde la aprobación. |
| S5 | ¿El sistema registra el retiro y la devolución, y si el equipo volvió completo? | El administrador confirma los dos momentos. No hay un formulario de «volvió completo»: si volvió dañado, usa la marca de daño. La revisión y la firma siguen en papel. |
| S6 | Cancelar y devolver quedaron en la misma frase. ¿Se puede cancelar un equipo que ya salió? | Solo se cancela si todavía no se retiró. Si ya está en préstamo, el cierre es la devolución. |
| S7 | Para volver a reservar un objeto cerca de la devolución, ¿una hora antes o media hora antes? | 60 minutos antes de la fecha de fin. |
| S8 | ¿El estudiante paga? ¿Ve el valor del equipo? ¿Qué significa «otro objeto extra»? | El préstamo no se cobra. El valor lo carga el administrador y el estudiante no lo ve. Si pasa de 500 dólares, la reserva lleva una segunda línea del mismo objeto, sin el monto. |
| S9 | ¿En qué consiste la penalización? ¿Impide nuevas reservas? | Una nota en la descripción del estudiante, solo para administradores. No bloquea reservas. El objeto dañado, además, se oculta. |
| S10 | Si hay varias cámaras iguales, ¿se reserva una unidad o cualquiera que esté libre? | Se reserva el tipo y una cantidad. No hay número de serie. El administrador puede anotar en la reserva qué unidad entregó. |
| S11 | ¿Cuántas fotos, y de dónde salen? | Hasta dos URL de Google por objeto, pegadas por el administrador. El sistema no guarda el archivo. |
| S12 | ¿Reservan desde el celular, desde el computador o desde los dos? | Desde los dos. El estudiante, sobre todo en el celular; el administrador, en la computadora de la bodega. |
| S13 | ¿El estudio de televisión, u otro espacio, entra en esta versión? | No. El MVP reserva objetos y equipos de la Bodega COCOA. |
| S14 | En diciembre, ¿lo usan estudiantes reales o es un prototipo para revisar? | Prototipo para que Santiago lo recorra el 2 de diciembre. No es la salida con toda la universidad. |
| S15 | ¿Alguna cifra de la entrevista (unos 150 dólares al mes, unos 1,50, o unos 3.000 al año la página actual) es un tope? | Ninguna. No las reconoció. El despliegue es gratuito o de bajo costo. |
| S16 | ¿Qué es un día fuera de trabajo? ¿Se reserva en festivo? ¿En qué huso? | Sábado y domingo son días fuera de trabajo: no pueden ser fecha de fin. Los festivos no están cargados. Hora de Ecuador, America/Guayaquil. |
| S17 | ¿El sistema impide pedir un objeto de otra carrera, o solo lo mira el administrador? | El administrador marca carreras y semestres en el objeto. Si no marca ninguno, cualquiera puede pedirlo y él verifica a mano. Si marca, el estudiante lo ve y no puede agregarlo cuando no coincide. |
| S18 | Si solo se puede prestar una parte del pedido, ¿qué pasa con el resto? | Se aprueba o se rechaza la reserva entera. El motivo explica qué sí se puede prestar y el estudiante envía otra. |
| S19 | ¿Hay un horario del área y otro por equipo? | No en esta versión. Un objeto deja de ofrecerse si está en mantenimiento, dañado u oculto, o si la cantidad ya está en reservas aprobadas o en préstamo. La regla 17 devuelve esa cantidad a la cuenta una hora antes del fin. |
| S20 | Si se da de baja a un estudiante que todavía tiene un equipo, ¿qué pasa con el préstamo? | Deja de poder entrar. La reserva sigue visible para los administradores hasta la devolución. |
| S21 | ¿El reporte en Excel entra, y con qué columnas? | No entra. Las reservas se ven en pantalla. |
| S22 | ¿Profesores o monitores también reservan? | No. Solo estudiantes con cuenta. El cliente no los nombró. |
| S23 | ¿La reserva es por horas, por días, de un día para otro o de noche? | Fecha y hora de inicio y de fin. Puede cruzar la noche y varios días. Sin tope de duración. |

## 8. Épicas del MVP

| Épica | Qué cubre | Alcance |
| --- | --- | --- |
| E1 · Cuentas y acceso | Entrar, cerrar la sesión a la hora, crear estudiantes y administradores, preguntas frecuentes | §3.1, §3.2, §3.14 |
| E2 · Catálogo de la bodega | Crear y editar objetos, fotos, cantidad, valor, mantenimiento y daño | §3.3, §3.10 |
| E3 · Reservas del estudiante | Armar la reserva, enviarla, historial, cancelar y comprobante | §3.4 a §3.8 |
| E4 · Aprobación, préstamo y avisos | Aprobar o rechazar, notas, retiro, devolución, 30 minutos, correos y actualización sola | §3.9, §3.11, §3.12, §3.13, §3.15 |

Las historias de usuario llegan en el avance 3.

## 9. Criterios de éxito y restricciones

**Criterios de éxito:**

- Un estudiante arma una reserva con más de un objeto, sin que se borre, y la deja pendiente sin hablar con Santiago.
- Un administrador ve carrera, semestre, el uso declarado y sus notas, y aprueba o rechaza desde esa pantalla.
- Si nadie retira en 30 minutos, el objeto figura otra vez como disponible y el estudiante tiene un correo.
- El estudiante reconoce el estado en su historial por el texto, no solo por el color.
- El catálogo, las reservas y los avisos cambian sin recargar la página a mano.

**Restricciones:**

- El cliente lo prueba en el avance del 2 de diciembre de 2026. La presentación final del curso es el 16 o 17 de diciembre.
- Es un prototipo para recorrerlo, no la salida con todos los estudiantes (S14).
- Interfaz en React, como pidió el cliente. Catálogo, reservas y avisos se actualizan solos.
- Despliegue gratuito o de bajo costo. Las cifras de la entrevista no son un tope (S15).
- No hay un archivo de inventario confirmado: el administrador carga el catálogo en el sistema.
- Hora de Ecuador (S16).

## Uso de IA

Se usó el asistente de Cursor (Grok) para leer `Notas Cliente.txt` y el documento de preguntas del avance 1, contrastarlos con el PRD de ejemplo y redactar este documento, el brand board y el `DESIGN.md`. Se le pidió que no completara lo que Santiago no dijo.

Al cuestionar las reglas aparecieron tres choques, y quedaron como supuesto en vez de como hecho: la sesión de una hora frente a una reserva ya enviada (S2), desde cuándo corren los 30 minutos si la aprobación es anterior al inicio (S4), y qué quiere decir «otro objeto extra» cuando el valor pasa de 500 dólares (S8). El mismo pase dejó abiertos el motivo del rechazo (S3), la penalización (S9) y la reserva partida (S18).

Para la identidad se exploraron tres direcciones y se descartaron dos. Un set oscuro de cine se lee mal en la bodega, con gente esperando. Un taller industrial con etiquetas de estarcido parece ferretería y no el comprobante que el estudiante ya se lleva. La dirección elegida es la ficha de préstamo: papel, tinta cacao y el estado siempre escrito. Está en el brand board y en `DESIGN.md`.

Las decisiones de alcance siguen lo que el cliente dijo en clase el 11 de noviembre de 2026. Si una frase no es lo que se oyó, se corrige aquí antes del avance 3.
