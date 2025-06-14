**Título:** `Hey dude! - Funcionalidades Principales (MVP)`

**Estado:** `Borrador`

**Autores:** `[Mario](mailto:mario1plaza@gmail.com)`

**Revisores:** `[Mario](mailto:mario1plaza@gmail.com)`

**Fecha de última actualización:** `2024-05-21`

---

## 1. Resumen (Abstract)

_"Hey dude!" es una aplicación móvil para grupos de amigos que asisten a eventos como festivales o viajes. La app resuelve tres problemas clave: el reparto de gastos, la localización de amigos en tiempo real dentro del evento y la comunicación rápida a través de notificaciones push._

## 2. Problema

_Cuando un grupo de amigos va a un festival, viaje o plan similar, se enfrenta a varios problemas de coordinación recurrentes:_
*   **Gestión de gastos:** Es complicado llevar la cuenta de quién ha pagado qué y cuánto debe cada persona. El proceso es manual, propenso a errores y a menudo se deja para el final, generando situaciones incómodas.
*   **Pérdida de amigos:** En lugares grandes y concurridos como un festival de música, es extremadamente fácil separarse del grupo y muy difícil reencontrarse. La comunicación tradicional (llamadas, mensajes de texto) no es eficiente por el ruido, la mala cobertura o la falta de referencias claras.
*   **Comunicación ineficiente:** Se necesita una forma de enviar mensajes cortos y urgentes a todo el grupo o a miembros específicos (ej. "¡El concierto empieza, venid al escenario principal!", "Estoy en la barra de la entrada") que no se pierda en un chat grupal ruidoso.

## 3. Objetivos y Metas

### 3.1. Objetivos (Goals)

*   **Facilitar el reparto de gastos:** Crear un sistema donde cualquier miembro del grupo pueda añadir un gasto y asignarlo a las personas correspondientes, llevando un balance claro y visible en tiempo real.
*   **Mejorar la localización:** Proveer un mapa del evento donde los miembros del grupo puedan ver la ubicación de sus amigos en tiempo real.
*   **Agilizar la comunicación:** Permitir el envío de notificaciones push predefinidas o personalizadas a todo el grupo o a miembros seleccionados.

### 3.2. No-Objetivos (Non-Goals)

*   **No será una app de chat completa:** La comunicación se centra en "pings" o notificaciones, no en conversaciones largas.
*   **No se integra con bancos (inicialmente):** Los pagos y deudas se saldan fuera de la app. La app es solo para el seguimiento.
*   **La localización es solo durante el evento:** La app no rastrea la ubicación de los usuarios de forma continua fuera del contexto de un "plan" o "evento" activo.

## 4. Solución Propuesta

_Se desarrollará una aplicación móvil para iOS y Android (usando Flutter) y un servicio de backend (usando Spring Boot). La app se estructurará en torno a "Planes" o "Eventos" (ej. "Festival PortAmérica 2024"). Un usuario crea un plan e invita a sus amigos. Dentro de un plan, los usuarios tendrán acceso a tres módulos principales:_

*   **Módulo de Gastos (Splitter):**
    *   Una lista de todos los gastos del grupo.
    *   Un botón para añadir un nuevo gasto (descripción, cantidad, quién pagó).
    *   Al añadir un gasto, se podrá seleccionar a quiénes se les imputa (por defecto, a todos).
    *   Una pantalla de "Balances" que muestre quién debe dinero a quién.

*   **Módulo de Localización (Map):**
    *   Un mapa (usando un proveedor como Google Maps o Mapbox) centrado en la zona del evento.
    *   Pines/avatares mostrando la última ubicación conocida de cada miembro del grupo.
    *   La ubicación se actualizará periódicamente (cada X minutos) cuando la app esté en segundo plano, o con más frecuencia si está en primer plano. Se debe notificar al usuario de este comportamiento.

*   **Módulo de Mensajes Rápidos (Pings):**
    *   Una interfaz para enviar una notificación push.
    *   Se podrá seleccionar a quién enviar el "ping" (todo el grupo o seleccionar amigos).
    *   Habrá una lista de mensajes predefinidos ("Estoy aquí", "Veniros", "¿Dónde estáis?") y la opción de escribir uno corto.

## 5. Otras Soluciones Consideradas

_Descripción breve de otras alternativas que se exploraron y por qué se descartaron._

*   **Opción A:** _Descripción..._
    *   **Pros:** _Fácil de implementar._
    *   **Contras:** _No cumple completamente con el Objetivo 2._
*   **Opción B:** _Descripción..._
    *   **Pros:** _La mejor experiencia de usuario._
    *   **Contras:** _Requiere un gran esfuerzo técnico._

## 6. Preguntas Abiertas y Riesgos

_¿Qué dudas quedan por resolver? ¿Qué riesgos podrían afectar el proyecto?_


## 7. Discusión y Comentarios

_Este espacio puede usarse para registrar decisiones importantes que se tomen en reuniones o en los comentarios de este documento._

## 8. Flujo de Creación de Grupos e Invitación

_El siguiente flujo describe cómo un usuario se registra, crea un plan e invita a sus amigos._

1.  **Registro de Usuario:** El usuario se registra en la aplicación usando su email y una contraseña. Se podría añadir un registro con Google/Apple para simplificar.
2.  **Creación del Plan:** Una vez registrado, el usuario puede crear un "Plan" (ej: "Festival FIB 2024"). Al crearlo, se convierte en el administrador de ese plan.
3.  **Invitación por Email:**
    *   Dentro del plan, el administrador tiene una opción para "Invitar Amigos".
    *   Introduce las direcciones de email de los amigos que quiere invitar.
    *   El sistema envía un email a cada dirección con un enlace único de invitación.
4.  **Recepción de la Invitación (Flujo del Amigo):**
    *   El amigo recibe el email y hace clic en el enlace.
    *   **Si la app NO está instalada:** El enlace le redirige a la App Store (iOS) or Google Play Store (Android). Una vez instalada y abierta, la app detecta el enlace pendiente y le pregunta si quiere unirse al plan.
    *   **Si la app SÍ está instalada:** El enlace abre directamente "Hey dude!" y muestra una pantalla para confirmar y unirse al plan.
5.  **Unión al Plan:** Una vez que el amigo acepta, se añade al plan y ya puede ver los gastos, el mapa y los pings del grupo.

## 9. Modelo de Datos (Entidades Principales)

_A continuación se definen las estructuras de datos principales para el MVP._

### Entidad: `Usuario`

| Campo | Tipo | Descripción | Ejemplo |
| :--- | :--- | :--- | :--- |
| `id` | UUID | Identificador único del usuario. | `c3a5a3d4-3f9b-4b8c-8f9f-6e8d2e8b1e4c` |
| `nombre` | String | Nombre del usuario. | `Mario` |
| `email` | String | Email del usuario (usado para login). | `mario@email.com` |
| `password` | String | Contraseña hasheada. | `(hash)` |
| `telefono` | String | Teléfono móvil (opcional, para futuras features). | `+34600112233` |
| `url_foto_perfil` | String | URL a la imagen de perfil (opcional). | `https://.../foto.jpg` |
| `fecha_creacion` | Timestamp | Fecha y hora de creación del usuario. | `2024-05-21T10:00:00Z` |

### Entidad: `Plan`

| Campo | Tipo | Descripción | Ejemplo |
| :--- | :--- | :--- | :--- |
| `id` | UUID | Identificador único del plan. | `a1b2c3d4-e5f6-7890-1234-567890abcdef` |
| `nombre` | String | Nombre del plan. | `Festival MadCool 2024` |
| `descripcion` | String | Descripción opcional del plan. | `Viaje a Madrid para el festival.` |
| `fecha_inicio` | Date | Fecha de inicio del plan. | `2024-07-10` |
| `fecha_fin` | Date | Fecha de fin del plan. | `2024-07-13` |
| `admin_id` | UUID | ID del usuario que creó/administra el plan. | `c3a5a3d4-...` |
| `ubicacion_lat`| Double | Latitud del punto central del mapa. | `40.416775` |
| `ubicacion_lon`| Double | Longitud del punto central del mapa. | `-3.703790` |
| `fecha_creacion` | Timestamp | Fecha y hora de creación del plan. | `2024-05-21T10:05:00Z` |

### Relación: `Plan_Usuarios`
*Existirá una tabla intermedia que relacione qué usuarios pertenecen a qué planes.*

### Entidad: `Gasto`

| Campo | Tipo | Descripción | Ejemplo |
| :--- | :--- | :--- | :--- |
| `id` | UUID | Identificador único del gasto. | `f1g2h3i4-j5k6-7890-1234-567890lmnpq` |
| `plan_id` | UUID | ID del plan al que pertenece el gasto. | `a1b2c3d4-...` |
| `payer_id` | UUID | ID del usuario que pagó. | `c3a5a3d4-...` |
| `descripcion` | String | Descripción del gasto. | `Cena en la pizzería` |
| `importe` | Decimal | Cantidad total del gasto. | `85.50` |
| `fecha` | Date | Fecha en que se realizó el gasto. | `2024-07-11` |
| `url_foto_ticket`| String | URL a la foto del ticket (opcional). | `https://.../ticket.jpg` |
| `fecha_creacion` | Timestamp | Fecha y hora de creación del registro. | `2024-07-11T22:00:00Z` |

### Relación: `Gasto_Participantes`
*Tabla intermedia que define qué usuarios participan en un gasto para su división.*
* **Lógica de negocio:** Al crear un gasto, el `payer_id` se añade por defecto a esta tabla.

| gasto_id | usuario_id | status |
| :--- | :--- | :--- |
| `f1g2h3i4-...` | `c3a5a3d4-...` | `CONFIRMED` |
| `f1g2h3i4-...` | `d5e6f7g8-...` | `PAID_UNCONFIRMED` |
| `f1g2h3i4-...` | `h9i0j1k2-...` | `PENDING` |

*   **Status:** `PENDING` (no ha pagado), `PAID_UNCONFIRMED` (el deudor dice que ha pagado), `CONFIRMED` (el que pagó confirma que ha recibido el dinero).

### Entidad: `Ping`

| Campo | Tipo | Descripción | Ejemplo |
| :--- | :--- | :--- | :--- |
| `id` | UUID | Identificador único del ping. | `p1q2r3s4-t5u6-7890-1234-567890vwxyz` |
| `plan_id` | UUID | ID del plan donde se envió el ping. | `a1b2c3d4-...` |
| `sender_id` | UUID | ID del usuario que envió el ping. | `c3a5a3d4-...` |
| `mensaje` | String | Contenido del mensaje. | `¡El concierto empieza!` |
| `fecha_envio` | Timestamp | Fecha y hora de envío del ping. | `2024-07-11T23:30:00Z` |

### Relación: `Ping_Destinatarios`
*Tabla intermedia que define qué usuarios recibieron un ping concreto. Si está vacía, se asume que era para todo el grupo.*

## 10. Discusión y Comentarios

_Este espacio puede usarse para registrar decisiones importantes que se tomen en reuniones o en los comentarios de este documento._

## 11. API Endpoints (Contrato Preliminar)

_A continuación se definen los endpoints de la API REST que el backend expondrá. Esto sirve como contrato entre el frontend y el backend._

### Autenticación y Usuario
| Método | Endpoint | Descripción |
| :--- | :--- | :--- |
| `POST` | `/auth/register` | Registra un nuevo usuario. |
| `POST` | `/auth/login` | Inicia sesión y devuelve un token de autenticación. |
| `GET` | `/users/me` | Obtiene el perfil del usuario actualmente logueado. |

### Planes
| Método | Endpoint | Descripción | Notas/Reglas de Negocio |
| :--- | :--- | :--- | :--- |
| `GET` | `/plans` | Obtiene una lista de todos los planes en los que participa el usuario. | |
| `POST` | `/plans` | Crea un nuevo plan. | El usuario que lo crea se convierte en admin. |
| `GET` | `/plans/{planId}` | Obtiene los detalles de un plan específico. | |
| `PUT` | `/plans/{planId}` | Actualiza los datos de un plan (nombre, descripción, fechas...). | Solo el admin del plan puede hacerlo. |
| `DELETE` | `/plans/{planId}` | Borra un plan completo. | Solo el admin del plan puede. Se borra toda la info asociada. |

### Miembros y Participantes (dentro de un Plan)
| Método | Endpoint | Descripción | Notas/Reglas de Negocio |
| :--- | :--- | :--- | :--- |
| `GET` | `/plans/{planId}/members` | Obtiene la lista de usuarios que participan en un plan. | |
| `DELETE` | `/plans/{planId}/members/me` | El usuario actual abandona el plan. | Si es el último miembro, el plan se borra. |
| `DELETE` | `/plans/{planId}/members/{userId}` | Un admin expulsa a un miembro del plan. | Solo el admin puede. El admin no puede expulsarse a sí mismo. |

### Invitaciones (dentro de un Plan)
| Método | Endpoint | Descripción | Notas/Reglas de Negocio |
| :--- | :--- | :--- | :--- |
| `POST` | `/plans/{planId}/invitations` | Envía una invitación por email a un nuevo miembro. | El body contiene `{ "email": "amigo@email.com" }`. |
| `DELETE` | `/plans/{planId}/invitations/{invitationId}` | Cancela una invitación que aún no ha sido aceptada. | Solo el admin puede. |

### Gastos (dentro de un Plan)
| Método | Endpoint | Descripción | Notas/Reglas de Negocio |
| :--- | :--- | :--- | :--- |
| `GET` | `/plans/{planId}/expenses` | Obtiene la lista de gastos. | Se puede filtrar por estado (e.g., `?status=pending`). |
| `POST` | `/plans/{planId}/expenses` | Añade un nuevo gasto. | El `payer` es el usuario logueado. |
| `PUT` | `/plans/{planId}/expenses/{expenseId}` | Modifica un gasto. | Solo el creador del gasto puede. |
| `DELETE`| `/plans/{planId}/expenses/{expenseId}` | Elimina un gasto. | Solo el creador del gasto puede. |

### Pagos y Balances (dentro de un Plan)
| Método | Endpoint | Descripción | Notas/Reglas de Negocio |
| :--- | :--- | :--- | :--- |
| `GET` | `/plans/{planId}/balance` | Obtiene el balance final del plan (quién debe a quién). | |
| `POST`| `/plans/{planId}/expenses/{expenseId}/pay` | El usuario logueado marca su parte de este gasto como pagada. | Cambia el estado a `PAID_UNCONFIRMED`. |
| `POST`| `/plans/{planId}/expenses/{expenseId}/confirm/{userId}` | El creador del gasto confirma que ha recibido el pago de un usuario. | Cambia el estado a `CONFIRMED`. |

### Pings (dentro de un Plan)
| Método | Endpoint | Descripción | Notas/Reglas de Negocio |
| :--- | :--- | :--- | :--- |
| `GET` | `/plans/{planId}/pings` | Obtiene los últimos pings del plan. | |
| `POST` | `/plans/{planId}/pings` | Envía un nuevo ping. | El body puede incluir a quién se dirige. |

## 12. Discusión y Comentarios

_Este espacio puede usarse para registrar decisiones importantes que se tomen en reuniones o en los comentarios de este documento._ 