# 3. Estrategia de autenticación y seguridad

*   **Fecha:** 2024-05-22
*   **Estado:** Aceptado

## Contexto

La API del proyecto necesita un mecanismo seguro para verificar la identidad de los usuarios (autenticación) y determinar si tienen permiso para realizar una acción (autorización). Este mecanismo debe ser eficiente, escalable y adecuado para una arquitectura de servicios consumida por una aplicación móvil (Flutter).

## Decisión

Se ha decidido utilizar **JSON Web Tokens (JWT)** como el estándar para la autenticación y autorización en la API.

El flujo de autenticación será el siguiente:

**1. Flujo de autenticación clásica (Email/Contraseña):**
1.  **Login:** El usuario envía sus credenciales al endpoint `/auth/login`.
2.  **Generación del Token:** El backend valida las credenciales y genera un token JWT.
3.  **Envío y Almacenamiento:** El token se envía al cliente de Flutter para que lo almacene y lo use en peticiones futuras.

**2. Flujo de autenticación social (Google/Facebook/Apple):**
1.  **SDK del Proveedor:** La aplicación de Flutter utiliza el SDK oficial de Google, Facebook o Apple para que el usuario inicie sesión.
2.  **Obtención del Token del Proveedor:** Tras un login exitoso, el SDK del proveedor le devuelve a la app de Flutter un `access_token` o `id_token` específico de ese proveedor.
3.  **Envío al Backend:** La app de Flutter envía este token del proveedor a nuestro backend, a través del endpoint `POST /auth/social-login`.
4.  **Validación en Backend:** Nuestro backend recibe ese token y lo valida contactando con el servidor del proveedor (ej. Google) para asegurarse de que es legítimo y obtener los datos del usuario (email, nombre, etc.).
5.  **Creación de Cuenta/Login:**
    *   Si el email del usuario no existe en nuestra base de datos, se crea una nueva cuenta de usuario asociada a ese proveedor.
    *   Si ya existe, simplemente se recupera el usuario.
6.  **Generación de Token JWT propio:** Finalmente, nuestro backend genera **su propio token JWT** (como en el flujo clásico) y se lo devuelve a la app de Flutter. A partir de aquí, el proceso es idéntico al de la autenticación clásica.

A partir del paso 6, para acceder a endpoints protegidos, la app cliente siempre usará el token JWT generado por nuestro backend, incluyéndolo en la cabecera `Authorization` de cada petición.

## Consecuencias

### Positivas:
*   **Stateless (Sin Estado):** El backend no necesita almacenar información de la sesión del usuario. La información está en el propio token, lo que simplifica la arquitectura y mejora la escalabilidad.
*   **Estándar y Seguro:** JWT es un estándar de la industria (RFC 7519) ampliamente adoptado y considerado seguro si se usa correctamente (con algoritmos de firma fuertes como RS256).
*   **Ideal para APIs y Móviles:** Es el enfoque predilecto para proteger APIs REST y es fácilmente manejable por clientes como una app de Flutter.
*   **Flexibilidad:** El "payload" (contenido) del token es personalizable, por lo que podemos incluir información útil como roles o permisos para gestionar la autorización de forma eficiente.
*   **Excelente integración con Spring Security:** Spring Boot, a través de Spring Security, ofrece un soporte robusto y completo para implementar la autenticación basada en JWT.

### Negativas:
*   **Gestión de Revocación:** Revocar un token JWT antes de que expire (por ejemplo, si un usuario cambia su contraseña o se le quiere forzar a cerrar sesión) es más complejo que con sesiones tradicionales. Se pueden implementar estrategias como listas negras de tokens (blacklist), pero añaden complejidad. Para el MVP, se asumirá que los tokens son válidos hasta su expiración.
*   **Tamaño del Token:** Si se incluye demasiada información en el token, puede aumentar el tamaño de las cabeceras de las peticiones. Esto es insignificante para nuestro caso de uso.

### Alternativas Consideradas:
*   **Sesiones basadas en Cookies:** Es el enfoque tradicional de las aplicaciones web. El servidor mantiene un registro de las sesiones activas. Se descartó por ser menos adecuado para una API REST consumida por un cliente no-navegador (la app móvil) y por ser más difícil de escalar horizontalmente.
*   **Tokens Opacos (OAuth2/OIDC):** Utilizar un flujo completo de OAuth2 con un servidor de autorización dedicado. Se considera una sobreingeniería para la fase inicial del proyecto, ya que introduce una gran complejidad. El uso de JWT como "bearer tokens" es una implementación más sencilla y directa que cumple con nuestros requisitos. 