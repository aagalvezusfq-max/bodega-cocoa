# DESIGN.md — Bodega COCOA

Sistema de diseño y guía de estilo del frontend (`client/`). Léelo antes de crear o modificar cualquier pantalla o componente. Si una spec contradice este archivo, manda la spec y hay que actualizar este archivo en el mismo commit. Fuente visual: [docs/diseno/brand-board.html](docs/diseno/brand-board.html). Las reglas de estados, plazos y textos salen de [docs/prd/prd.md](docs/prd/prd.md). Si el PRD cambia un estado, cambian aquí el nombre, el color y el texto.

## Concepto

La ficha de préstamo de la bodega: eliges el equipo, ves si te lo prestaron y sabes cuándo devolverlo.

**Palabras clave:** claro · preciso · bodega.

**Usuarios y contexto:** el estudiante arma la reserva entre clases. El cliente no fijó el dispositivo (PRD, S12): se diseña primero para el celular y también para el computador. El administrador trabaja en la computadora de la bodega, con varias personas delante, y tiene que leer el estado sin detenerse. Hay como mínimo dos administradores.

**Dirección elegida.** Se probaron tres y se quedó una. El set oscuro de cine se descartó porque la bodega no es una sala y el administrador atiende seguido. El taller industrial se descartó porque parece una ferretería y no el comprobante que el estudiante ya se lleva. La ficha de préstamo usa papel, tinta cacao y el estado siempre escrito.

## Principios

1. **El estado de la reserva siempre a la vista,** con texto. El color no basta.
2. **Un solo botón primario por pantalla.**
3. **Cada pantalla tiene su mensaje** de carga, de lista vacía, de error y de éxito.
4. **Lo interno de la bodega no sale hacia el estudiante:** daño, notas, descripción del estudiante y valor en dólares.
5. **Se habla como en el mostrador:** objeto, reserva, retirar, devolver. Sin códigos ni palabras de sistema.

## Color

Usa solo estas variables. No escribas colores directamente en los componentes.

| Variable | Valor | Nombre | Uso |
| --- | --- | --- | --- |
| `--color-primario` | `#3D2914` | Cacao | Botón primario, encabezados, marca |
| `--color-acento` | `#1A4F4C` | Verde ficha | Enlaces y foco del teclado. Nunca en botones |
| `--color-texto` | `#1C1612` | Tinta | Texto principal |
| `--color-texto-secundario` | `#5C5148` | Cartón | Ayudas, fechas, etiquetas menores |
| `--color-fondo` | `#F3EBDD` | Papel | Fondo de página |
| `--color-superficie` | `#FFFFFF` | Superficie | Tarjetas y formularios |
| `--color-borde` | `#E4D8C8` | — | Bordes decorativos |
| `--color-borde-campo` | `#6B5E54` | — | Borde de los campos (6.2:1 sobre blanco, 5.2:1 sobre papel) |
| `--color-exito` | `#1E5C34` | Verde | Estado «Devuelta» y mensajes de éxito |
| `--color-exito-fondo` | `#E3F3E7` | — | Fondo de éxito |
| `--color-info` | `#1A4A78` | Azul ficha | Estado «Aprobada» |
| `--color-info-fondo` | `#E4EEF8` | — | Fondo de información |
| `--color-prestamo` | `#0E4F48` | Verde bodega | Estado «En préstamo» |
| `--color-prestamo-fondo` | `#E3F3F0` | — | Fondo de préstamo |
| `--color-aviso` | `#8A5300` | Ámbar | Estado «Pendiente» |
| `--color-aviso-fondo` | `#FBF1DF` | — | Fondo de aviso |
| `--color-error` | `#9B1C1C` | Error | Errores de formulario y estado «Rechazada» |
| `--color-error-fondo` | `#FBECEA` | — | Fondo de error |
| `--color-vencida` | `#7A2E0E` | Ladrillo | Estado «Vencida» |
| `--color-vencida-fondo` | `#F8E6D8` | — | Fondo de vencida |
| `--color-no-retirada` | `#243644` | Pizarra | Estado «No retirada» |
| `--color-no-retirada-fondo` | `#E7EEF2` | — | Fondo de no retirada |
| `--color-neutro` | `#4A4A4A` | Gris | Estado «Cancelada» |
| `--color-neutro-fondo` | `#EDEAE6` | — | Fondo neutro |
| `--color-mantenimiento` | `#5C3D00` | Ámbar oscuro | Objeto «En mantenimiento» |
| `--color-mantenimiento-fondo` | `#F8EFD4` | — | Fondo de mantenimiento |
| `--color-danado` | `#6B2A12` | Óxido | Objeto «Dañado». Solo lo ve el administrador |
| `--color-danado-fondo` | `#F8E6DC` | — | Fondo de dañado |

Todos los textos de esta tabla cumplen contraste 4.5:1 o más sobre su fondo. El blanco sobre cacao da 13.7:1. El cartón `#5C5148` sobre papel da 6.5:1.

## Tipografía

Fuentes de Google Fonts:

- `--fuente-titulos`: **Newsreader** 600.
- `--fuente-texto`: **Source Sans 3** 400 y 700.

| Uso | Tamaño | Fuente |
| --- | --- | --- |
| Título de pantalla | 32 px | títulos 600 |
| Título de sección | 24 px | títulos 600 |
| Destacado y botones | 18 px | texto 700 |
| Texto general y campos | 16 px | texto 400 |
| Ayudas, fechas y etiquetas de estado (mínimo) | 14 px | texto 400 o 700 |

Interlineado 1.5. Ningún texto por debajo de 14 px.

## Espacio y forma

| Variable | Valor | Uso típico |
| --- | --- | --- |
| `--espacio-1` | 4 px | Entre icono y texto |
| `--espacio-2` | 8 px | Entre etiqueta y campo |
| `--espacio-3` | 12 px | Relleno de botones y etiquetas |
| `--espacio-4` | 16 px | Entre campos de un formulario |
| `--espacio-5` | 24 px | Relleno de tarjetas |
| `--espacio-6` | 32 px | Entre secciones |
| `--espacio-7` | 48 px | Margen de página en escritorio |

- **Radios:** `--radio-control` 10 px (botones y campos); `--radio-tarjeta` 16 px (tarjetas); `--radio-etiqueta` 999 px (etiquetas de estado).
- **Sombra única:** `--sombra-tarjeta` solo en la tarjeta de equipo que sí se puede reservar. En mantenimiento, agotada o dañada, la tarjeta va sin sombra.

## Tokens en CSS

Estas variables van en `client/src/styles/tokens.css` y se importan una sola vez en la entrada de la app:

```css
:root {
  --color-primario: #3d2914;
  --color-acento: #1a4f4c;
  --color-texto: #1c1612;
  --color-texto-secundario: #5c5148;
  --color-fondo: #f3ebdd;
  --color-superficie: #ffffff;
  --color-borde: #e4d8c8;
  --color-borde-campo: #6b5e54;
  --color-exito: #1e5c34;
  --color-exito-fondo: #e3f3e7;
  --color-info: #1a4a78;
  --color-info-fondo: #e4eef8;
  --color-prestamo: #0e4f48;
  --color-prestamo-fondo: #e3f3f0;
  --color-aviso: #8a5300;
  --color-aviso-fondo: #fbf1df;
  --color-error: #9b1c1c;
  --color-error-fondo: #fbecea;
  --color-vencida: #7a2e0e;
  --color-vencida-fondo: #f8e6d8;
  --color-no-retirada: #243644;
  --color-no-retirada-fondo: #e7eef2;
  --color-neutro: #4a4a4a;
  --color-neutro-fondo: #edeae6;
  --color-mantenimiento: #5c3d00;
  --color-mantenimiento-fondo: #f8efd4;
  --color-danado: #6b2a12;
  --color-danado-fondo: #f8e6dc;

  --fuente-titulos: "Newsreader", Georgia, serif;
  --fuente-texto: "Source Sans 3", system-ui, sans-serif;

  --espacio-1: 4px;
  --espacio-2: 8px;
  --espacio-3: 12px;
  --espacio-4: 16px;
  --espacio-5: 24px;
  --espacio-6: 32px;
  --espacio-7: 48px;

  --radio-control: 10px;
  --radio-tarjeta: 16px;
  --radio-etiqueta: 999px;

  --sombra-tarjeta: 0 1px 2px rgb(61 41 20 / 0.08), 0 4px 12px rgb(61 41 20 / 0.06);
}
```

## Componentes

| Componente | Cómo se ve | Reglas |
| --- | --- | --- |
| **Botón primario** | Fondo `--color-primario`, texto blanco 700 | Altura mínima 44 px. Uno por pantalla. La acción de esa pantalla: enviar, aprobar o confirmar la devolución |
| **Botón secundario** | Borde de 2 px `--color-primario`, fondo blanco, texto primario | Altura mínima 44 px. Cancelar, rechazar o volver al catálogo |
| **Campo** | Etiqueta visible arriba, borde `--color-borde-campo` | Ayuda debajo. Con error: borde de 2 px `--color-error` y mensaje debajo con icono |
| **Tarjeta de equipo** | Foto arriba, superficie blanca, radio de tarjeta, sombra de tarjeta | Nombre, una línea de qué es, y la cantidad. Si se puede reservar, lleva sombra. En mantenimiento, agotada o «no corresponde»: sin sombra |
| **Etiqueta de estado** | Píldora con texto de 14 px en negrita sobre el fondo de su color | Siempre con texto, nunca solo color. Estados de reserva y de objeto, en las tablas de abajo |
| **Rango de fechas** | Dos campos, inicio y fin, no una grilla de turnos | La reserva es un rango que puede durar el semestre. Los 30 minutos no se eligen aquí: son el plazo para retirar después de la aprobación |
| **Comprobante** | Tarjeta con objetos, cantidades y las dos fechas | Es lo que hoy se imprime. No pide firma: la firma sigue en papel |
| **Nota interna** | Borde izquierdo de 4 px en `--color-primario`, etiqueta «Nota interna» | Solo en pantallas de administrador. No se renderiza en la vista del estudiante |
| **Fila de reserva (administrador)** | Estudiante, equipo, devolución y estado | En el celular, cada fila se convierte en una tarjeta. La nota interna va debajo del nombre |
| **Mensaje de carga** | Solo texto, por ejemplo «Cargando el catálogo…» | Sin spinners. El catálogo y los avisos se actualizan solos; este texto cubre la primera carga y un fallo de red que ya se reintentó |
| **Mensaje de éxito / error** | Fondo de su color, icono y texto | Nombra lo que pasó y, si es un error, qué hacer |
| **Lista vacía** | Borde discontinuo y una acción | Siempre ofrece el siguiente paso |

## Datos y textos

### Estados de una reserva

Coinciden con la regla 11 del PRD. El valor de API no se muestra en pantalla.

| Estado (API) | Texto en pantalla | Color de texto | Fondo |
| --- | --- | --- | --- |
| `pendiente` | Pendiente | `--color-aviso` | `--color-aviso-fondo` |
| `aprobada` | Aprobada | `--color-info` | `--color-info-fondo` |
| `en_prestamo` | En préstamo | `--color-prestamo` | `--color-prestamo-fondo` |
| `devuelta` | Devuelta | `--color-exito` | `--color-exito-fondo` |
| `rechazada` | Rechazada | `--color-error` | `--color-error-fondo` |
| `cancelada` | Cancelada | `--color-neutro` | `--color-neutro-fondo` |
| `no_retirada` | No retirada | `--color-no-retirada` | `--color-no-retirada-fondo` |
| `vencida` | Vencida | `--color-vencida` | `--color-vencida-fondo` |

Texto que acompaña al estado, cuando hace falta una frase y no solo la píldora:

| Estado | Texto de apoyo |
| --- | --- |
| Pendiente | «Enviada. Falta que un administrador la apruebe.» |
| Aprobada | «Tienes 30 minutos para retirar {objetos}. Si no llegas, vuelven a quedar disponibles.» Si el reloj todavía no empieza: «Aprobada. Retírala el {inicio}. Tienes 30 minutos a partir de esa hora.» |
| En préstamo | «Devuélvelo el {fin} en la bodega.» |
| Devuelta | «Devuelta el {fecha}.» |
| Rechazada | El motivo escrito por el administrador. Si no hubiera motivo, no se puede rechazar (PRD, S3). |
| Cancelada | «Cancelaste esta reserva.» |
| No retirada | «Pasaron 30 minutos y no se retiró. El equipo volvió a quedar disponible.» |
| Vencida | «La fecha de entrega ya pasó. Devuelve el equipo en la bodega el próximo día de trabajo.» |

### Estados de un objeto

No son estados de la reserva. El daño no se muestra al estudiante.

| Estado | Quién lo ve | Texto | Color de texto | Fondo |
| --- | --- | --- | --- | --- |
| Disponible | Estudiante y administrador | «Quedan {n} de {total}» | `--color-texto` | ninguno; la tarjeta lleva sombra |
| Sin unidades | Estudiante y administrador | «No quedan» | `--color-texto-secundario` | tarjeta sin sombra |
| En mantenimiento | Estudiante y administrador | «En mantenimiento» | `--color-mantenimiento` | `--color-mantenimiento-fondo` |
| No corresponde | Estudiante | «No corresponde a tu carrera» | `--color-texto-secundario` | tarjeta sin sombra, no se puede agregar |
| Dañado | Solo administrador | «Dañado» | `--color-danado` | `--color-danado-fondo` |

La segunda línea de un objeto de más de 500 dólares se llama «{nombre} · objeto extra». El estudiante no ve el monto. El administrador sí ve el valor, en la ficha del objeto, como «Valor: 500 USD» solo cuando supera ese umbral, y el número real que cargó.

### Formatos

- **Fechas:** día de la semana abreviado, día y mes en español: «vie 21 nov». Con hora: «vie 21 nov · 10:00».
- **Rango de una reserva:** «vie 21 nov · 10:00 – vie 5 dic · 16:00».
- **Horas:** 24 horas. Zona America/Guayaquil (PRD, S16).
- **Cantidades:** «Quedan 18 de 30». Con cero, «No quedan». En la reserva, «2 trípodes».
- **Plazos fijos,** siempre con la cifra del PRD: 30 minutos para retirar, 1 hora de sesión, 1 hora antes de la devolución para cancelar, 60 minutos antes del fin para que la cantidad vuelva a ofrecerse.
- **Carrera y semestre:** «Cine · 6.º semestre».
- **Errores de validación de la API:** junto al campo al que corresponden. Si no se pueden asociar a un campo, arriba del formulario.

### Mensajes de pantalla

| Situación | Texto |
| --- | --- |
| Cargando el catálogo | «Cargando el catálogo…» |
| Cargando las reservas | «Cargando tus reservas…» |
| Catálogo vacío | «Todavía no hay equipos en el catálogo.» El administrador ve, además, el botón «Agregar un objeto». |
| Historial vacío | «Todavía no tienes reservas.» Botón secundario: «Ver el catálogo». |
| Reserva enviada | «Reserva enviada. Te avisamos por correo cuando un administrador la apruebe.» |
| Sesión a punto de cerrarse | «Esta reserva sin enviar se borra a las {hora}. El equipo deja de quedar apartado.» |
| Sin conexión al actualizar | «No se pudo actualizar. Revisa la conexión. Lo intentamos de nuevo.» |
| Aprobación sin cantidad | «Ya no quedan unidades. No se puede aprobar.» Solo lo ve el administrador. |

## Tono de voz

Español, tuteo con el estudiante, frases cortas y concretas. Con el administrador, el mismo español y la misma claridad: la pantalla le habla de tú. Sin tecnicismos, sin códigos de error y sin regaños. La penalización no se escribe como castigo en la interfaz del estudiante: se dice qué pasó y qué hacer.

| Así sí | Así no |
| --- | --- |
| «Tu reserva está aprobada. Tienes 30 minutos para retirar 2 trípodes.» | «Su solicitud ha sido procesada exitosamente.» |
| «La fecha de entrega ya pasó. Devuelve el equipo en la bodega el próximo día de trabajo.» | «Error: préstamo vencido.» |
| «Este trípode está en mantenimiento. Elige otro del catálogo.» | «Item no disponible (MNT).» |

## Accesibilidad

- Contraste de texto de 4.5:1 o más.
- Un `<label>` real en cada campo.
- Los estados y errores llevan texto, nunca solo color.
- Zonas táctiles de 44 px como mínimo.
- Foco visible al navegar con teclado: contorno de 3 px en `--color-acento`.
- Botones con `<button>` y enlaces con `<a href>`, nunca un `div` con `onClick`.
- La nota interna, el daño y el valor no están en el HTML de la vista del estudiante. No basta con ocultarlos con CSS.

## No hacemos

- Librerías de UI o de CSS (Tailwind, Bootstrap, MUI…).
- Animaciones, degradados o sombras fuera de la tarjeta de equipo.
- Modo oscuro en el MVP.
- Emojis e iconos de librerías: solo SVG en línea, los mínimos.
- Mostrar al estudiante el daño, las notas, la descripción que el administrador escribió sobre él, o el valor en dólares.
- Un selector de turnos de media hora. Los 30 minutos son el plazo para retirar, no una franja que se elige.
- WhatsApp, chatbot ni aviso al guardia dentro de la interfaz.
- Fotos de personas. La foto del objeto es la URL de Google que pegó el administrador, hasta dos por objeto.
- Spinners y recarga manual como forma de ver datos nuevos.
