# 1. Elección de la base de datos

*   **Fecha:** 2024-05-22
*   **Estado:** Aceptado

## Contexto

El backend del proyecto necesita una base de datos para persistir los datos de la aplicación, como usuarios, planes, gastos y sus relaciones. El modelo de datos, tal como se define en el documento de diseño principal, es inherentemente relacional:
*   Un `Plan` tiene múltiples `Usuarios`.
*   Un `Gasto` pertenece a un `Plan` y tiene un `Usuario` que paga.
*   Un `Gasto` se reparte entre múltiples `Usuarios` (participantes).

Se necesita una base de datos que pueda gestionar estas relaciones de forma eficiente y segura, garantizando la integridad de los datos (por ejemplo, que no se pueda borrar un usuario si tiene gastos asociados sin gestionar).

## Decisión

Se ha decidido utilizar **PostgreSQL** como el sistema de gestión de bases de datos para este proyecto.

## Consecuencias

### Positivas:
*   **Modelo Relacional Fuerte:** PostgreSQL es ideal para nuestro modelo de datos, permitiendo el uso de `foreign keys` para mantener la integridad referencial.
*   **Transacciones ACID:** Garantiza que las operaciones complejas (como añadir un gasto y sus participantes) sean atómicas: o se hacen todas bien, o no se hace ninguna. Esto es crucial para la fiabilidad de los datos económicos.
*   **Ecosistema Maduro:** Se integra perfectamente con Spring Boot a través de `Spring Data JPA` y `Hibernate`, lo que facilita enormemente el desarrollo.
*   **Escalabilidad y Fiabilidad:** Es una tecnología probada, robusta y capaz de escalar si el proyecto crece.
*   **Código Abierto:** No tiene costes de licencia.

### Negativas:
*   **Menos flexibilidad de esquema:** A diferencia de una base de datos NoSQL como MongoDB, los cambios en la estructura de las tablas (el esquema) son más rígidos y requieren migraciones formales. Para nuestro caso, esto se considera una ventaja, ya que fuerza un diseño más disciplinado.

### Alternativas Consideradas:
*   **MySQL:** Otra excelente base de datos relacional. Se eligió PostgreSQL por su manejo históricamente superior de transacciones complejas y tipos de datos avanzados, aunque ambas hubieran sido opciones viables.
*   **MongoDB:** Una base de datos NoSQL. Se descartó debido a la complejidad de gestionar las relaciones de nuestros datos. Implementar la lógica de reparto de gastos y balances de forma segura habría sido significativamente más complejo y propenso a errores sin las garantías que ofrece un sistema relacional. 