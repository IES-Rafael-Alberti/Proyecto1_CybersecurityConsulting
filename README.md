# Proyecto1_CybersecurityConsulting
## Introducción
La empresa TrustShield Financial nos ha contratado para la realización de un análisisde su estructura y así identificar vulnerabilidades que puedan poner en peligro la confidencialidad, integridad y disponibilidad de sus datos.

Hemos decidido centrarnos en las vulnerabilidades de sus aplicaciones web ya que esta es la cara que da la empresa a internet, y por lo tanto, a gran parte de sus usuarios y a posibles atacantes.

Las categorías de vulnerabilidad han sido elegidas por su número de incidentes en los últimos años y como de graves serían para TrustShield Financial en caso de sufrirlas.
## Categorías de vulnerabilidades

### Broken Access Control
#### Descripción
Esta vulnerabilidad lo que hace es que puedan actuar fuera de los permisos que se le había dado al usuario. Esto puede producir que el ciberdelincuente pueda compartir informacion la cual no está autorizado, modificar dato o incluso la destruccion de los mismos. Algunas de las vulnerabilidades más comunes de este tipo son:

+ Permitir ver o editar la cuenta de otra persona.

+ Acceder a APIs con controles de acceso inexistentes para los métodos POST, PUT, DELETE.

+ Forzar la navegación a páginas autenticadas siendo un usuario no autenticado o entrar a páginas las cuales un usuario regular no podría visitar.

+ Eludir las comprobaciones de control de acceso modificando la URL (alteración de parámetros o navegación forzada), el estado interno de la aplicación o la página HTML, o mediante el uso de una herramienta que modifique los pedidos a APIs.

+ Elevación de privilegios. Actuar como usuario sin haber iniciado sesión o actuar como administrador cuando se inició sesión como usuario regular.

+ Configuraciones incorrectas de CORS (uso compartido de recursos de origen cruzado) que permiten el acceso a APIs desde orígenes no autorizados o confiables.

**Contramedidas**

+ Unas de las posibilidades que tenemos es que denegemos por defecto todo menos los recursos públicos.

+ Otras de las medidas es reistrar las fallas de control de acceso y alertar a los aministradores cuando por ejemplo estas fallas sean repetidas.

+ También podriamos limitar la tasas de acceso permitidos a las APIs y controladores de forma que podamos minimizar los daños.

+ Deshabilite el listado de directorios del servidor web y asegúrese de que los archivos de metadatos (por ejemplo una carpeta .git) y archivos de respaldo no puedan ser accedidos a partir de la raíz del sitio web.

+ Implemente mecanismos de control de acceso una única vez y reutilícelos en toda la aplicación, incluyendo la minimización del uso de CORS.

+ El control de acceso debe implementar su cumplimiento a nivel de dato y no permitir que el usuario pueda crear, leer, actulizar o borrar cualquier dato.

Aquí podemos encontrar varios casos reales de vulnerabilidades de este tipo:

## Identificación de CVEs

+ **CVE-2024-4263**

    Este es una de las vulnerabilidades que hemos encontrado la cuál los usuarios con pocos privilegios con solo permisos de edición (EDIT) pueden eliminar cualquier dato. Este problema está por la poca validación de las solicitudes DELEte que con tan sólo permisos EDIT puede hacer eliminaciones de datos no autorizados.

    Aunque en la documentación oficial sólo pone que los usuarios con permiso EDIT **solo** pueden leer y actualizar datos, **NO** eliminarlos

    Según CVSS nos encontramos contra una vulnerabilidad **MEDIA** con una nota de **5.4**

+ **CVE-2024-22234**
    Esta vulnerabilidad trata de que cuando utilizas el método *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)* directamente se le pasa un parámetro de autenticación que sea nulo y devuelve un retorno verdadero erróneo.

    La forma en la que no es vulnerable si cualquiera de los siguientes es cierto:  
    + La aplicación no utiliza *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)*
    directamente. 
    + La aplicación no pasa nula a *AuthenticationTrustResolver.isFullyAuthenticated*
    + La aplicación solo usa *isFullyAuthenticated*

    Según CVSS nos encontramos con una vulnerabilidad **ALTA** con una nota de **7.4**

****

### Cryptographic Failures

#### Descripción

Esta vulnerabilidad de lo que consiste es poder mirar los datos  de contraseñas, números dde tarjetas de crédditom registros médicos, información personal, etc. Ya que estas series de datos deben tener una protección adiccional, principalmente si están sujeto a  leyes de privacidad como pueden ser (Reglamento General de Protección de Datos de la UE) o regulaciones como (protección de datos financieros como el Estándar de Seguridad de Datos de PCI -PCI DSS-). Algunas de las preguntas que nos tenemos que hacer para estos datos son:

+ ¿Se utilizan algoritmos o protocolos criptográficos antiguos o débiles de forma predeterminada o en código antiguo?
+ ¿Se utilizan claves criptográficas predeterminadas, se generan o reutilizan claves criptográficas débiles, o es inexistente la gestión o rotación de claves adecuadas?
+ ¿Se incluyen las claves criptográficas en los repositorios de código fuente?
+ ¿No es forzado el cifrado, por ejemplo, faltan las directivas de seguridad de los encabezados HTTP (navegador) o los encabezados?
+ ¿El certificado de servidor recibido y la cadena de confianza se encuentran debidamente validados?
+ ¿Las contraseñas se utilizan como claves criptográficas en ausencia de una función de derivación de claves a partir de contraseñas?
+ ¿Se utilizan funciones hash en obsoletas, como MD5 o SHA1, o se utilizan funciones hash no criptográficas cuando se necesitan funciones hash criptográficas?


**Contramedidas**

Estas son algunas de las cosas que tenemos que verificar para saber como prevenir estos ataques.

+ Clasifique los datos procesados, almacenados o transmitidos por una aplicación. Identifique qué datos son confidenciales de acuerdo con las leyes de privacidad, los requisitos reglamentarios o las necesidades comerciales.

+ No almacene datos sensibles innecesariamente. Descártelos lo antes posible o utilice una utilización de tokens compatible con PCI DSS o incluso el truncamiento. Los datos que no se conservan no se pueden robar.

+ Asegúrese de cifrar todos los datos sensibles en reposo (almacenamiento).

+ Garantice la implementación de algoritmos, protocolos y claves que utilicen estándares sólidos y actualizados; utilice una gestión de claves adecuada.

+ Deshabilite el almacenamiento en caché para respuestas que contengan datos sensibles.

+ Aplique los controles de seguridad requeridos según la clasificación de los datos.

+ No utilice protocolos antiguos como FTP y SMTP para transportar datos sensibles.

+ Las claves deben generarse criptográficamente al azar y almacenarse en la memoria como arrays de bytes. Si se utiliza una contraseña, debe convertirse en una clave mediante una función adecuada de derivación de claves basada en contraseña.

+ Evite las funciones criptográficas y los esquemas de relleno(padding) en desuso, como MD5, SHA1, PKCS número 1 v1.5.

Aquí podemos encontrar varios casos reales de vulnerabilidades de este tipo:

## Identificación de CVEs

+ **CVE-2024-45402**

    Picotls es una biblioteca de protocolos TLS que permite a los usuarios seleccionar diferentes backend criptográficos en función de su uso. Cuando analizas un mensaje TLS falsificado, los picolts pueden liberar la misma memoria dos veces. Este doble liberación de memoria ocurre durante la eliminación de múltiples objetos sin ninguna llamada intermedia a malloc. Típicamente, esto desencadena la implementación de malloc para detectar el error y abortar el proceso. Pero dependiendo de las partes internas de malloc y el backend criptográfico que se este utilizando, la falla prodría conducir a un escenario de uso despues de la liberación lo que permitiría la ejecución arbitaria de codigo.

    Según CVSS estamos ante una vulnerabilidad de gravedad **ALTA** con una puntuación de **8.6**

+ **CVE-2024-6189**

    Esta vulnerabilidad afecta a la función *fromSetWirelessRepeat* del archivo */goform/WifiExtraSet*. La manipulación del argumento wpapsk_crypto conduce a un desbordamiento de búfer basado en pila. Es posible lanzar el ataque de forma remota.

    Esta vulnerabiliddad desde la versión 2.0 siguiendo la versión 3.0, 3.1, 4.0 son todas vulnerabilidades de gravedad **ALTA** con estas respectivas notas **9.0, 8.8, 8.8, 8.7**

### Security logging and monitoring failures
#### Descripción
Si no se monitoriza y registra las actividades de una aplicación web o no se hace de manera correcta y efectiva, no seremos capaces de detectar, escalar y responder a ataques. Esto puede ocurrir debido a que:
+ Los eventos con autor, como los logins (ya sean exitosos o no) y transacciones de importancia (borrado de datos, creación...), no quedan registrados.
+ Los avisos y errores no generan mensajes de log o no se ven con claridad.
+ No se monitorizan los logs de aplicaciones y APIs en busca de actividad sospechosa.
+ Los logs solo se almacenan localmente y con una sola copia en lugar de en otro dispositivo y, preferiblemente, más de una copia.
+ No hay procesos para escalar la respuesta o no son efectivos.
+ Los pentesting y escaneos realizados por herramientas para pruebas dinámicas de seguridad de aplicaciones (DAST) no generan alertas.

Además, si los logs y alertas son visibles a todos y no solo a las personas responsables se puede filtrar información.

Aunque estas vulnerabilidades no provocarian un ataque por si sola, es muy importante el solventarlas ya que facilitaría la detección y respuesta a otros ataques y el análisis forense tras sufrir un ataque. Algunas maneras para cubrir este tipo de vulnerabilidad sería:

+ Todos los logins, control de accesos y fallos en la validación del input por parte del servidor se añadan a un log con información    suficiente sobre los usuarios para detectar cuentas sospechosas y mantener dichos logs el tiempo suficiente para realizar un análisis forense en caso de que ocurriera algo.
+ Asegurarse de que los logs se generan en un formato en el que un gestor de logs pueda comprender.
+ Asegurarse de que los datos de los logs están codificados correctamente para prevenir inyecciones o ataques a los sistemas de log o monitoreo y darnos una imagen distinta de la situación de la real.
+ Asegurarse de que transacciones de importancia (por ejemplo agregar información a una tabla de una base de datos) tengan un seguimiento de auditoría con controles de integridad para prevenir que se manipulen o eliminen.
+ Los equipos de DevSecOps deberían de monitorizar y alertar de manera efectiva para detectar actividad sospechosa y responder rápidamente.
+ Establecer o adoptar un plan de respuesta y recuperación a incidentes.

### Server-side request forgery (SSRF)
#### Descripción
Los problemas de SSRF ocurren cuando una aplicación web realiza una consulta HTTP sin validar la URL suministrada por el usuario. Esto permite a un atacante forzar a la aplicación web a enviar una solicitud a la estructura interna de la red donde se aloja, incluso estando protegido por un firewall, VPN u otro tipo de lista de control de acceso a la red (ACL) y así obtener información, escalar privilegios o ejecutar código remotamente en un servidor.

Con las facilidades y conveniencias proporcionadas a los usuarios por las aplicaciones web actuales el número de incidencias de SSRF está en aumento.

Esta vulnerabilidad sería muy grave para TrustShield Financial, ya que un atacante podría acceder o incluso manipular información confidencial simplemente cambiando una URL si tiene algo de conocimento sobre la red de la empresa.

## Identificación de CVEs
+ **CVE-2021-21973**: Este CVE registra una vulnerabilidad de SSRF encontrada en el cliente de vSphere debido a que no se valida correctamente las URLs en un plugin de vCenter Server. Esta vulnerabilidad puede permitir a un atacante con acceso al puerto 443 obtener información sensible enviando una solicitud POST. Esta vulnerabilidad afecta a VMware vCenter Server (7.x antes de 7.0 U1c, 6.7 antes de 6.7 U3l y 6.5 antes de 6.5 U3n) y a VMware Cloud Foundation (4.x antes de 4.2 y 3.x antes de 3.10.1.2).
Tiene un CVSS de 5'3.

## Contramedidas propuestas
+ **CVE-2021-21973**
    
    A día de hoy esta vulnerabilidad ya está parcheada, por lo que la mejor solución sería actualizar a una de las versiones más actuales no afectadas. En el caso de que no fuera así podríamos probar varias cosas desde la capa de red y desde la e aplicación:

    Desde la capa de red podríamos:
    + Separar los sistemas que se encargan de las solicitudes externas del resto de la red, reduciendo el impacto de un SSRF.
    + Limitar el tráfico de nuestra intranet configurando nuestro firewall para que deniegue por defecto salvo para el tráfico esencial.

    Desde la capa de aplicación podríamos:
    + Validar todo lo que introduzca un usuario, forzandolos a usar un esquema de URL, puerto y destino con una whitelist. De esta manera el ususario solo podrá acceder a las direcciones de la whitelist.
    + Deshabilitar redirecciones HTTP.
    + No devolver información sin validar al cliente.

## Conclusiones