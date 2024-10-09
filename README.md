## Proyecto1_CybersecurityConsulting

### Broken Access Control

Hemos seleccionado esta vulnerabilidad ya que tiene una incidencia promedio de un 3.81%

Esta vulnerabilidad lo que hace es que puedan actuar fuera de los permisos que se le había dado al usuario. Esto puede producir que el ciberdelincuente pueda compartir informacion la cual no está autorizado, modificar dato o incluso la destruccion de los mismos. Algunas de las vulnerabilidades más comunes de este tipo son:

- Permitir ver o editar la cuenta de otra persona.
- Acceder a APIs con controles de acceso inexistentes para los métodos POST, PUT, DELETE.
- Forzar la navegación a páginas autenticadas siendo un usuario no autenticado o entrar a páginas las cuales un usuario regular no podría visitar.

*¿Cómo podemos prevenirlo?*

Unas de las posibilidades que tenemos es que denegemos por defecto todo menos los recursos públicos.

Otras de las medidas es reistrar las fallas de control de acceso y alertar a los aministradores cuando por ejemplo estas fallas sean repetidas.

También podriamos limitar la tasas de acceso permitidos a las APIs y controladores de forma que podamos minimizar los daños.

****

Aquí podemos encontrar varios casos reales de vulnerabilidades de este tipo.

#### CVE-2024-4263

Este es una de las vulnerabilidades que hemos encontrado la cuál los usuarios con pocos privilegios con solo permisos de edición (EDIT) pueden eliminar cualquier dato. Este problema está por la poca validación de las solicitudes DELEte que con tan sólo permisos EDIT puede hacer eliminaciones de datos no autorizados.

Aunque en la documentación oficial sólo pone que los usuarios con permiso EDIT **solo** pueden leer y actualizar datos, **NO** eliminarlos

Según CVSS nos encontramos contra una vulnerabilidad **MEDIA** con una nota de **5.4**

#### CVE-2024-22234
Esta vulnerabilidad trata de que cuando utilizas el método *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)* directamente se le pasa un parámetro de autenticación que sea nulo y devuelve un retorno verdadero erróneo.

La forma en la que no es vulnerable si cualquiera de los siguientes es cierto:  
- La aplicación no utiliza *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)*
 directamente. 
- La aplicación no pasa nula a *AuthenticationTrustResolver.isFullyAuthenticated*
- La aplicación solo usa *isFullyAuthenticated*

Según CVSS nos encontramos con una vulnerabilidad **ALTA** con una nota de **7.4**