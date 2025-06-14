# Plantilla de Documento de Diseño (Design Doc)

> Copia este archivo y renómbralo (p. ej., `DD-2024-05-21-Nueva-Pagina-de-Perfil.md`) para cada nuevo diseño.

---

**Título:** `[Nombre del Proyecto/Funcionalidad]`

**Estado:** `Borrador | En Revisión | Aprobado | Completo`

**Autores:** `@[TuNombre], @[OtroAutor]`

**Revisores:** `@[ProductManager], @[LíderTécnico]`

**Fecha de última actualización:** `AAAA-MM-DD`

---

## 1. Resumen (Abstract)

_Describe en 2 o 3 frases el problema que estás resolviendo y la solución que propones. Es el "elevator pitch" de tu diseño._

## 2. Problema

_Describe en detalle el problema que se aborda. ¿Qué dolor de usuario estamos aliviando? ¿Qué oportunidad de negocio estamos persiguiendo? Usa datos si los tienes (ej. "El 30% de los usuarios abandonan el flujo de pago en el paso X")._

## 3. Objetivos y Metas

### 3.1. Objetivos (Goals)

_¿Qué queremos lograr con esta solución? Sé específico._
*   _Ej: Reducir el tiempo para completar la Tarea Y en un 50%._
*   _Ej: Incrementar la tasa de conversión de la página Z en un 5%._
*   _Ej: Permitir a los usuarios hacer X cosa que antes no podían._

### 3.2. No-Objetivos (Non-Goals)

_Es igual de importante definir qué **NO** se busca con este proyecto para evitar que el alcance crezca indefinidamente (scope creep)._
*   _Ej: Este proyecto no modificará el sistema de autenticación._
*   _Ej: La integración con la plataforma B se hará en una fase posterior._

## 4. Solución Propuesta

_Esta es la parte central del documento. Describe tu solución en detalle. Puedes apoyarte en diagramas, flujos de usuario y enlaces a prototipos._

*   **Flujos de Usuario (User Flows):** _Describe los pasos que un usuario seguirá._
*   **Prototipos y Mockups:** _[Enlace a Figma, Sketch, etc.](http://figma.com/...)_
*   **Consideraciones Técnicas (opcional):** _¿Impacta a la API? ¿Necesita cambios en la base de datos?_
*   **Casos de borde (Edge Cases):** _¿Qué pasa si el usuario no tiene internet? ¿Qué ve un usuario nuevo vs uno antiguo?_

## 5. Otras Soluciones Consideradas

_Describe brevemente otras alternativas que exploraste y por qué las descartaste. Esto demuestra que has hecho un análisis completo._

*   **Opción A:** _Descripción..._
    *   **Pros:** _Fácil de implementar._
    *   **Contras:** _No cumple completamente con el Objetivo 2._
*   **Opción B:** _Descripción..._
    *   **Pros:** _La mejor experiencia de usuario._
    *   **Contras:** _Requiere un gran esfuerzo técnico._

## 6. Preguntas Abiertas y Riesgos

_¿Qué dudas quedan por resolver? ¿Qué riesgos podrían afectar el proyecto?_

*   **Pregunta:** _¿Cómo se comportará esta pantalla en dispositivos muy pequeños?_
*   **Riesgo:** _La API externa de la que dependemos tiene un límite de peticiones._

## 7. Discusión y Comentarios

_Este espacio puede usarse para registrar decisiones importantes que se tomen en reuniones o en los comentarios de este documento._ 