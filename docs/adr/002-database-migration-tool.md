# 2. Herramienta de migración de base de datos

*   **Fecha:** 2024-05-22
*   **Estado:** Aceptado

## Contexto

El esquema de la base de datos de la aplicación (las tablas, columnas, etc.) evolucionará a medida que se añadan nuevas funcionalidades. Es necesario gestionar estos cambios de forma sistemática y controlada, especialmente cuando se trabaja en equipo o se despliega en diferentes entornos (desarrollo, producción).

Un sistema de migración de base de datos automatiza la aplicación de estos cambios y los mantiene bajo control de versiones, evitando problemas de inconsistencia y facilitando las actualizaciones.

## Decisión

Se ha decidido utilizar **Liquibase** para gestionar las migraciones del esquema de la base de datos.

Liquibase funcionará de la siguiente manera:
1.  Los cambios en el esquema se definirán en archivos de `changeset`, que pueden ser en formato SQL, XML, YAML o JSON. Para mayor claridad y control, se optará por el formato **SQL**.
2.  Estos archivos de `changeset` se almacenarán en el control de versiones (Git) junto al código del backend.
3.  Al arrancar la aplicación de Spring Boot, Liquibase comprobará si hay nuevos `changesets` que no se hayan aplicado en la base de datos y los ejecutará automáticamente.

## Consecuencias

### Positivas:
*   **Control de versiones del esquema:** El historial de cambios de la base de datos queda registrado en Git, lo que proporciona una trazabilidad completa.
*   **Automatización:** Las actualizaciones del esquema se aplican automáticamente al iniciar la aplicación, simplificando los despliegues.
*   **Independencia de la base de datos:** Aunque escribamos los `changesets` en SQL, Liquibase tiene una capa de abstracción que puede facilitar una eventual migración a otra base de datos relacional.
*   **Soporte para Rollbacks:** Liquibase tiene mecanismos para deshacer cambios si una migración falla, lo que aumenta la seguridad.
*   **Excelente integración con Spring Boot:** `spring-boot-starter-data-jpa` y `spring-boot-starter-jdbc` funcionan perfectamente con Liquibase.

### Negativas:
*   **Curva de aprendizaje:** Introduce una nueva herramienta y un nuevo concepto (`changesets`, `changelogs`) que el equipo debe conocer.
*   **Pequeña sobrecarga:** Añade un paso más al proceso de desarrollo al tener que crear un archivo de migración para cada cambio en el esquema. Este coste es mínimo en comparación con los beneficios en fiabilidad.

### Alternativas Consideradas:
*   **Flyway:** Es la otra gran alternativa en el ecosistema de Spring Boot. Es un poco más simple que Liquibase, pero también menos potente (por ejemplo, su sistema de `rollbacks` es menos avanzado). Se ha elegido Liquibase por su mayor flexibilidad y potencia, que pueden ser útiles a largo plazo.
*   **Gestión manual de DDL con Hibernate (`ddl-auto`):** Se podría configurar Hibernate para que genere o actualice el esquema automáticamente. Se descarta esta opción por ser peligrosa y no apta para entornos de producción, ya que se pierde el control y la trazabilidad de los cambios. 