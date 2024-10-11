# Proyecto1_CybersecurityConsulting

## Broken Access Control

**Descripción**

Esta vulnerabilidad lo que hace es que puedan actuar fuera de los permisos que se le había dado al usuario. Esto puede producir que el ciberdelincuente pueda compartir informacion la cual no está autorizado, modificar dato o incluso la destruccion de los mismos. Algunas de las vulnerabilidades más comunes de este tipo son:

- Permitir ver o editar la cuenta de otra persona.

- Acceder a APIs con controles de acceso inexistentes para los métodos POST, PUT, DELETE.

- Forzar la navegación a páginas autenticadas siendo un usuario no autenticado o entrar a páginas las cuales un usuario regular no podría visitar.

- Eludir las comprobaciones de control de acceso modificando la URL (alteración de parámetros o navegación forzada), el estado interno de la aplicación o la página HTML, o mediante el uso de una herramienta que modifique los pedidos a APIs.

- Elevación de privilegios. Actuar como usuario sin haber iniciado sesión o actuar como administrador cuando se inició sesión como usuario regular.

- Configuraciones incorrectas de CORS (uso compartido de recursos de origen cruzado) que permiten el acceso a APIs desde orígenes no autorizados o confiables.

**Contramedidas**

- Unas de las posibilidades que tenemos es que denegemos por defecto todo menos los recursos públicos.

- Otras de las medidas es reistrar las fallas de control de acceso y alertar a los aministradores cuando por ejemplo estas fallas sean repetidas.

- También podriamos limitar la tasas de acceso permitidos a las APIs y controladores de forma que podamos minimizar los daños.

- Deshabilite el listado de directorios del servidor web y asegúrese de que los archivos de metadatos (por ejemplo una carpeta .git) y archivos de respaldo no puedan ser accedidos a partir de la raíz del sitio web.

- Implemente mecanismos de control de acceso una única vez y reutilícelos en toda la aplicación, incluyendo la minimización del uso de CORS.

- El control de acceso debe implementar su cumplimiento a nivel de dato y no permitir que el usuario pueda crear, leer, actulizar o borrar cualquier dato.

Aquí podemos encontrar varios casos reales de vulnerabilidades de este tipo:

### CVE-2024-4263

Este es una de las vulnerabilidades que hemos encontrado la cuál los usuarios con pocos privilegios con solo permisos de edición (EDIT) pueden eliminar cualquier dato. Este problema está por la poca validación de las solicitudes DELEte que con tan sólo permisos EDIT puede hacer eliminaciones de datos no autorizados.

Aunque en la documentación oficial sólo pone que los usuarios con permiso EDIT **solo** pueden leer y actualizar datos, **NO** eliminarlos

Según CVSS nos encontramos contra una vulnerabilidad **MEDIA** con una nota de **5.4**

### CVE-2024-22234
Esta vulnerabilidad trata de que cuando utilizas el método *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)* directamente se le pasa un parámetro de autenticación que sea nulo y devuelve un retorno verdadero erróneo.

La forma en la que no es vulnerable si cualquiera de los siguientes es cierto:  
- La aplicación no utiliza *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)*
 directamente. 
- La aplicación no pasa nula a *AuthenticationTrustResolver.isFullyAuthenticated*
- La aplicación solo usa *isFullyAuthenticated*

Según CVSS nos encontramos con una vulnerabilidad **ALTA** con una nota de **7.4**

****

## Cryptographic Failures

**Descripción**

Esta vulnerabilidad de lo que consiste es poder mirar los datos  de contraseñas, números dde tarjetas de crédditom registros médicos, información personal, etc. Ya que estas series de datos deben tener una protección adiccional, principalmente si están sujeto a  leyes de privacidad como pueden ser (Reglamento General de Protección de Datos de la UE) o regulaciones como (protección de datos financieros como el Estándar de Seguridad de Datos de PCI -PCI DSS-). Algunas de las preguntas que nos tenemos que hacer para estos datos son:

- ¿Se utilizan algoritmos o protocolos criptográficos antiguos o débiles de forma predeterminada o en código antiguo?
- ¿Se utilizan claves criptográficas predeterminadas, se generan o reutilizan claves criptográficas débiles, o es inexistente la gestión o rotación de claves adecuadas?
- ¿Se incluyen las claves criptográficas en los repositorios de código fuente?
- ¿No es forzado el cifrado, por ejemplo, faltan las directivas de seguridad de los encabezados HTTP (navegador) o los encabezados?
- ¿El certificado de servidor recibido y la cadena de confianza se encuentran debidamente validados?
- ¿Las contraseñas se utilizan como claves criptográficas en ausencia de una función de derivación de claves a partir de contraseñas?
- ¿Se utilizan funciones hash en obsoletas, como MD5 o SHA1, o se utilizan funciones hash no criptográficas cuando se necesitan funciones hash criptográficas?


**Contramedidas**

Estas son algunas de las cosas que tenemos que verificar para saber como prevenir estos ataques.

- Clasifique los datos procesados, almacenados o transmitidos por una aplicación. Identifique qué datos son confidenciales de acuerdo con las leyes de privacidad, los requisitos reglamentarios o las necesidades comerciales.

- No almacene datos sensibles innecesariamente. Descártelos lo antes posible o utilice una utilización de tokens compatible con PCI DSS o incluso el truncamiento. Los datos que no se conservan no se pueden robar.

- Asegúrese de cifrar todos los datos sensibles en reposo (almacenamiento).

- Garantice la implementación de algoritmos, protocolos y claves que utilicen estándares sólidos y actualizados; utilice una gestión de claves adecuada.

- Deshabilite el almacenamiento en caché para respuestas que contengan datos sensibles.

- Aplique los controles de seguridad requeridos según la clasificación de los datos.

- No utilice protocolos antiguos como FTP y SMTP para transportar datos sensibles.

- Las claves deben generarse criptográficamente al azar y almacenarse en la memoria como arrays de bytes. Si se utiliza una contraseña, debe convertirse en una clave mediante una función adecuada de derivación de claves basada en contraseña.

- Evite las funciones criptográficas y los esquemas de relleno(padding) en desuso, como MD5, SHA1, PKCS número 1 v1.5.

Aquí podemos encontrar varios casos reales de vulnerabilidades de este tipo:


### CVE-2024-45402

**Título: Picotls Double Free**

**Descripción**

Picotls es una biblioteca de protocolos TLS que permite a los usuarios seleccionar diferentes backend criptográficos en función de su uso. Cuando analizas un mensaje TLS falsificado, los picolts pueden liberar la misma memoria dos veces. Este doble liberación de memoria ocurre durante la eliminación de múltiples objetos sin ninguna llamada intermedia a malloc. Típicamente, esto desencadena la implementación de malloc para detectar el error y abortar el proceso. Pero dependiendo de las partes internas de malloc y el backend criptográfico que se este utilizando, la falla prodría conducir a un escenario de uso despues de la liberación lo que permitiría la ejecución arbitaria de codigo.

Según CVSS estamos ante una vulnerabilidad de gravedad **ALTA** con una puntuación de **8.6**

### CVE-2024-6189

**Título: Tenda A301 WifiExtraSet fromSetWirelessRepeat stack-based overflow**

**Descripción**

Esta vulnerabilidad afecta a la función *fromSetWirelessRepeat* del archivo */goform/WifiExtraSet*. La manipulación del argumento wpapsk_crypto conduce a un desbordamiento de búfer basado en pila. Es posible lanzar el ataque de forma remota.

Esta vulnerabiliddad desde la versión 2.0 siguiendo la versión 3.0, 3.1, 4.0 son todas vulnerabilidades de gravedad **ALTA** con estas respectivas notas **9.0, 8.8, 8.8, 8.7**