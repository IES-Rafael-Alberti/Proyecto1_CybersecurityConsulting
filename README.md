
# Proyecto1_CybersecurityConsulting
## Introducción
La empresa TrustShield Financial nos ha contratado para la realización de un análisisde su estructura y así identificar vulnerabilidades que puedan poner en peligro la confidencialidad, integridad y disponibilidad de sus datos.

Hemos decidido centrarnos en las vulnerabilidades de sus aplicaciones web ya que esta es la cara que da la empresa a internet, y por lo tanto, a gran parte de sus usuarios y a posibles atacantes.

Las categorías de vulnerabilidad han sido elegidas por su número de incidentes en los últimos años y como de graves serían para TrustShield Financial en caso de sufrirlas.
## Categorías de vulnerabilidades
****

## Broken Access Control
### <u>Descripción</u>
Esta vulnerabilidad lo que hace es que puedan actuar fuera de los permisos que se le había dado al usuario. Esto puede producir que el ciberdelincuente pueda compartir informacion la cual no está autorizado, modificar dato o incluso la destruccion de los mismos. Algunas de las vulnerabilidades más comunes de este tipo son:

+ Permitir ver o editar la cuenta de otra persona.

+ Acceder a APIs con controles de acceso inexistentes para los métodos POST, PUT, DELETE.

+ Forzar la navegación a páginas autenticadas siendo un usuario no autenticado o entrar a páginas las cuales un usuario regular no podría visitar.

+ Eludir las comprobaciones de control de acceso modificando la URL (alteración de parámetros o navegación forzada), el estado interno de la aplicación o la página HTML, o mediante el uso de una herramienta que modifique los pedidos a APIs.

+ Elevación de privilegios. Actuar como usuario sin haber iniciado sesión o actuar como administrador cuando se inició sesión como usuario regular.

+ Configuraciones incorrectas de CORS (uso compartido de recursos de origen cruzado) que permiten el acceso a APIs desde orígenes no autorizados o confiables.

###  Contramedidas 

+ Unas de las posibilidades que tenemos es que denegemos por defecto todo menos los recursos públicos.

+ Otras de las medidas es registrar las fallas de control de acceso y alertar a los administradores cuando por ejemplo estas fallas sean repetidas.

+ También podriamos limitar la tasas de acceso permitidos a las APIs y controladores de forma que podamos minimizar los daños.

+ Deshabilite el listado de directorios del servidor web y asegúrese de que los archivos de metadatos (por ejemplo una carpeta .git) y archivos de respaldo no puedan ser accedidos a partir de la raíz del sitio web.

+ Implemente mecanismos de control de acceso una única vez y reutilícelos en toda la aplicación, incluyendo la minimización del uso de CORS.

+ El control de acceso debe implementar su cumplimiento a nivel de dato y no permitir que el usuario pueda crear, leer, actulizar o borrar cualquier dato.

Aquí podemos encontrar varios casos reales de vulnerabilidades de este tipo:

### Identificación de CVEs

+ ####  CVE-2024-4263 
    + **Gravedad:** Media.
    + **Puntiación CVSS:** 5.4 (Base Score).
    + **Descripción:** Este es una de las vulnerabilidades que hemos encontrado la cuál los usuarios con pocos privilegios con solo permisos de edición (EDIT) pueden eliminar cualquier dato. Este problema está por la poca validación de las solicitudes DELEte que con tan sólo permisos EDIT puede hacer eliminaciones de datos no autorizados. Aunque en la documentación oficial sólo pone que los usuarios con permiso EDIT **solo** pueden leer y actualizar datos, **NO** eliminarlos.

    + **Contramedidas**:
        + Actualizar a la versión 2.10.1 o superior de MLflow, ya que esta versión corrige el fallo de control de acceso.
        + Revisar los permisos de los usuarios con acceso a MLflow, asegurándote de limitar los permisos de edición solo a aquellos que realmente lo necesiten.
        + Monitorear los registros y actividades de usuarios con permisos de edición para identificar cualquier actividad inusual o no autorizada.


+ ####  CVE-2024-22234   
    + **Gravedad:** Alto.
    + **Puntuación CVSS:**  7.4 (Base Score).
    + **Descripción:** Esta vulnerabilidad trata de que cuando utilizas el método *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)* directamente se le pasa un parámetro de autenticación que sea nulo y devuelve un retorno verdadero erróneo.

    + **Contramedidas**:
        + La aplicación no utiliza *AuthenticationTrustResolver.isFullyAuthenticated(Authentication)*
        directamente. 
        + La aplicación no pasa nula a *AuthenticationTrustResolver.isFullyAuthenticated*
        + La aplicación solo usa *isFullyAuthenticated*


****

## Cryptographic Failures

### <u>Descripción</u>

Esta vulnerabilidad de lo que consiste es poder mirar los datos  de contraseñas, números de tarjetas de créditos, registros médicos, información personal, etc. Ya que estas series de datos deben tener una protección adiccional, principalmente si están sujeto a  leyes de privacidad como pueden ser (Reglamento General de Protección de Datos de la UE) o regulaciones como (protección de datos financieros como el Estándar de Seguridad de Datos de PCI -PCI DSS-). Algunas de las preguntas que nos tenemos que hacer para estos datos son:

+ ¿Se utilizan algoritmos o protocolos criptográficos antiguos o débiles de forma predeterminada o en código antiguo?
+ ¿Se utilizan claves criptográficas predeterminadas, se generan o reutilizan claves criptográficas débiles, o es inexistente la gestión o rotación de claves adecuadas?
+ ¿Se incluyen las claves criptográficas en los repositorios de código fuente?
+ ¿No es forzado el cifrado, por ejemplo, faltan las directivas de seguridad de los encabezados HTTP (navegador) o los encabezados?
+ ¿El certificado de servidor recibido y la cadena de confianza se encuentran debidamente validados?
+ ¿Las contraseñas se utilizan como claves criptográficas en ausencia de una función de derivación de claves a partir de contraseñas?
+ ¿Se utilizan funciones hash en obsoletas, como MD5 o SHA1, o se utilizan funciones hash no criptográficas cuando se necesitan funciones hash criptográficas?

###  Contramedidas 

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


### Identificación de CVEs

+ ####  CVE-2024-45402
    + **Gravedad:** Alta.
    + **Puntuación CVSS:** 8.6 (Base Score)
    + **Descripción:** Picotls es una biblioteca de protocolos TLS que permite a los usuarios seleccionar diferentes backend criptográficos en función de su uso. Cuando analizas un mensaje TLS falsificado, los picolts pueden liberar la misma memoria dos veces. Este doble liberación de memoria ocurre durante la eliminación de múltiples objetos sin ninguna llamada intermedia a malloc. Típicamente, esto desencadena la implementación de malloc para detectar el error y abortar el proceso. Pero dependiendo de las partes internas de malloc y el backend criptográfico que se este utilizando, la falla prodría conducir a un escenario de uso despues de la liberación lo que permitiría la ejecución arbitaria de codigo.
    + **Contramedidas:** 
        + Actualizar Picotls.
   
+ ####  CVE-2024-6189
    + **Gravedad:** Alta
    + **Puntiación CVSS:** 9.0-8.7(Score Base) dependiendo de la versión tiene una nota puntuación distinta
    + **Descripción:** Esta vulnerabilidad afecta a la función *fromSetWirelessRepeat* del archivo */goform/WifiExtraSet*. La manipulación del argumento wpapsk_crypto conduce a un desbordamiento de búfer basado en pila. Es posible lanzar el ataque de forma remota.
    + **Contramedidas:**
    

****

## Security logging and monitoring failures
### <u>Descripción</u>
Si no se monitoriza y registra las actividades de una aplicación web o no se hace de manera correcta y efectiva, no seremos capaces de detectar, escalar y responder a ataques. Esto puede ocurrir debido a que:
+ Los eventos con autor, como los logins (ya sean exitosos o no) y transacciones de importancia (borrado de datos, creación...), no quedan registrados.
+ Los avisos y errores no generan mensajes de log o no se ven con claridad.
+ No se monitorizan los logs de aplicaciones y APIs en busca de actividad sospechosa.
+ Los logs solo se almacenan localmente y con una sola copia en lugar de en otro dispositivo y, preferiblemente, más de una copia.
+ No hay procesos para escalar la respuesta o no son efectivos.
+ Los pentesting y escaneos realizados por herramientas para pruebas dinámicas de seguridad de aplicaciones (DAST) no generan alertas.

Además, si los logs y alertas son visibles a todos y no solo a las personas responsables se puede filtrar información.

### <u>Contramedidas</u>

Aunque estas vulnerabilidades no provocarian un ataque por si sola, es muy importante el solventarlas ya que facilitaría la detección y respuesta a otros ataques y el análisis forense tras sufrir un ataque. Algunas maneras para cubrir este tipo de vulnerabilidad sería:

+ Todos los logins, control de accesos y fallos en la validación del input por parte del servidor se añadan a un log con información    suficiente sobre los usuarios para detectar cuentas sospechosas y mantener dichos logs el tiempo suficiente para realizar un análisis forense en caso de que ocurriera algo.
+ Asegurarse de que los logs se generan en un formato en el que un gestor de logs pueda comprender.
+ Asegurarse de que los datos de los logs están codificados correctamente para prevenir inyecciones o ataques a los sistemas de log o monitoreo y darnos una imagen distinta de la situación de la real.
+ Asegurarse de que transacciones de importancia (por ejemplo agregar información a una tabla de una base de datos) tengan un seguimiento de auditoría con controles de integridad para prevenir que se manipulen o eliminen.
+ Los equipos de DevSecOps deberían de monitorizar y alertar de manera efectiva para detectar actividad sospechosa y responder rápidamente.
+ Establecer o adoptar un plan de respuesta y recuperación a incidentes.
****
 
## Server-side request forgery (SSRF)
### <u>Descripción</u>
Los problemas de SSRF ocurren cuando una aplicación web realiza una consulta HTTP sin validar la URL suministrada por el usuario. Esto permite a un atacante forzar a la aplicación web a enviar una solicitud a la estructura interna de la red donde se aloja, incluso estando protegido por un firewall, VPN u otro tipo de lista de control de acceso a la red (ACL) y así obtener información, escalar privilegios o ejecutar código remotamente en un servidor.

Con las facilidades y conveniencias proporcionadas a los usuarios por las aplicaciones web actuales el número de incidencias de SSRF está en aumento.

Esta vulnerabilidad sería muy grave para TrustShield Financial, ya que un atacante podría acceder o incluso manipular información confidencial simplemente cambiando una URL si tiene algo de conocimento sobre la red de la empresa.

### Identificación de CVEs
+ ####  CVE-2021-21973 : Este CVE registra una vulnerabilidad de SSRF encontrada en el cliente de vSphere debido a que no se valida correctamente las URLs en un plugin de vCenter Server. Esta vulnerabilidad puede permitir a un atacante con acceso al puerto 443 obtener información sensible enviando una solicitud POST. Esta vulnerabilidad afecta a VMware vCenter Server (7.x antes de 7.0 U1c, 6.7 antes de 6.7 U3l y 6.5 antes de 6.5 U3n) y a VMware Cloud Foundation (4.x antes de 4.2 y 3.x antes de 3.10.1.2).
Tiene un CVSS de 5'3.

### <u>Contramedidas</u>
+ ####  CVE-2021-21973 
    
    A día de hoy esta vulnerabilidad ya está parcheada, por lo que la mejor solución sería actualizar a una de las versiones más actuales no afectadas. En el caso de que no fuera así podríamos probar varias cosas desde la capa de red y desde la e aplicación:

    Desde la capa de red podríamos:
    + Separar los sistemas que se encargan de las solicitudes externas del resto de la red, reduciendo el impacto de un SSRF.
    + Limitar el tráfico de nuestra intranet configurando nuestro firewall para que deniegue por defecto salvo para el tráfico esencial.

    Desde la capa de aplicación podríamos:
    + Validar todo lo que introduzca un usuario, forzandolos a usar un esquema de URL, puerto y destino con una whitelist. De esta manera el ususario solo podrá acceder a las direcciones de la whitelist.
    + Deshabilitar redirecciones HTTP.
    + No devolver información sin validar al cliente.
****

## Security Misconfiguration
### <u>Descripción</u>

Los errores en la configuración son, a día de hoy, uno de los mayores problemas en la ciberseguridad. Se ha demostrado que el 90% de las aplicaciones tienen algún tipo de fallo de configuración, principalmente por el alto nivel de configuración de los programas actuales.
Entre los errores más comunes, se encuentran los siguientes:
+ Falta de un bastionado de seguridad apropiado a lo largo de la aplicación unos permisos mal configurados en la nube.
+ Funciones habilitadas o instaladas innecesarias (puertos abiertos sin utilidad, privilegios...)
+ Cuentas por defecto con sus contraseñas activas y sin cambiar.
+ Manejo de errores inadecuado, como la exposición de mensajes de error detallados o que revelan información sensible.
+ Con sistemas actualizados, las ultimas funciones de seguridad están desactivadas o no configuradas de forma segura.
+ La configuración de seguridad del servidor de aplicaciones, frameworks, librerías, bases de datos... no tiene establecidas valores seguros.
+ El servidor no envía cabeceras seguras y/o directivas, o no están establecidas con valores seguros.
+ El software esta desactualizado o es vulnerable.

### Identificación de CVEs

+ ####  CVE - 2024-26092 
    + Gravedad: Medio
    + Puntuación CVSS: 5.4 (Base Score)
    + Adobe experience Manager versión 6.5.20 y anterior estan afectados por una vulnerabilidad Cross-Site Scripting que puede aprovechar un atacante para inyectar scripts maliciosos en
  campos de formularios vulnerables.

+ #### CVE-2024-35933
    + Gravedad: Medio
    + Puntuación CVSS: 5.5 (Base Score)
    + CVE-2024-35933 es una vulnerabilidad relacionada con el kernel de Linux, específicamente en la función Bluetooth de dispositivos Intel. El problema surge debido a una "dereferencia de puntero nulo" en la función btintel_read_version, que se usa para leer la versión de dispositivos Intel a través de Bluetooth.

### <u>Contramedidas</u>

+ Crear una plataforma con el contenido mínimo y necesario, evitando instalar características, componentes o documentación innecesaria.
+ Establecer una tarea que revise y actualice las configuraciones relacionadas con todas las notas de seguridad, actualizaciones y parches
+ Segmentar la arquitectura de la aplicación implementando contenedores o una lista de control de acceso en la nube (ACLs)
+ Enviar directivas de seguridad a los clientes.
+ Establecer un proceso que verifique la efectividad de la configuración de todos los entornos.

****

## Vulnerable and Outdated Components 
### <u>Descripción</u>

Esta vulnerabilidad se refiere al uso de bibliotecas, frameworks, módulos o cualquier componente de software que no está actualizado o que contiene vulnerabilidades conocidas. Esto puede ocurrir cuando los desarrolladores no actualizan los componentes a sus versiones más recientes o usan componentes que ya no  tienen soporte. Los atacantes pueden aprovechar estas debilidades para comprometer la seguridad del sistema.
Alguno de los errores que lo componen son:
+ No saber la versión de todos los componentes en uso. Esto incluye también las dependencias de los componentes.
+ Usar un software vulnerable, sin soporte o desactualizado. Incluyendo Sistema Operativo, servidor web, SGBD, APIs, librerias...
+ No escanear frecuentemente por vulnerabilidades y no suscribirse a boletines relacionados a los componentes que uses.
+ No asegurar las configuraciones de los componentes.
+ Los desarrolladores de software no comprueban las compatibilidades de su software con las librerías que han sido actualizadas o parcheadas. 

### Identificación de CVEs

+ ####  CVE 2024-27395 
    + Gravedad: Medio
    + Puntuación CVSS: 5.5 (Base Score)
    + CVE-2024-25103 es una vulnerabilidad que afecta al software AppSamvid, relacionado con el uso de componentes obsoletos y vulnerables. Un atacante que cuente con privilegios administrativos locales en el sistema objetivo podría explotar esta vulnerabilidad colocando archivos DLL maliciosos.

+ ####  CVE-2022-24740 
    + Gravedad: Alto
    + Puntuación CVSS: 7.5 (Base Score)
    + Entre las versiones 14.0.0-alpha.5 y 15.0.0-alpha.0 de Volto, es posible que un atacante, después de haber atraído a un usuario al sitio de ataque, reemplace su cookie de autenticación por la cookie de autenticación del atacante. Esto le daría al atacante control sobre la cuenta y los privilegios de ese usuario.

### <u>Contramedidas</u>

+ Eliminar las dependencias, funciones, archivos y documentación en desuso.
+ Comprobar continuamente las versiones de los componentes y sus dependencias en busca de partes desactualizadas.
+ Revisar de forma frecuente el Common Vulnerability and Exposures(CVE) para corregir lo antes posible nuevas vulnerabilidades en nuestros componentes.
+ Obtener solo de fuentes seguras los componentes que forman nuestro sistema.

****

##  Insecure Design 
###  Descripción 
El **diseño inseguro** se refiere a una falla en la etapa de diseño o implementación de un sistema o software, en la que no se pensaron o incluyeron controles de seguridad necesarios para defenderse de posibles ataques.
Esto se suele confundir mucho con una implementación insegura, aunque no se refieren a la misma definición.

Un ejemplo contidiano podriía ser el siguiente: una constructora realiza los planos de una casa, estructuración de cuartos, ventanas, puertas, etc. Si en la planificación, no preves el uso de puertas o ventanas con cerraduras, esto crea una vulnerabilidad que por muy bien que se construya posteriormente la casa siguiente cada paso de los planos, ladrones podrían entrar en ella debido a la falta de seguridad en la planificación. A esto se refiere con un diseño inseguro.  
Si por el contrario, en la planificación se han planificado estas medidas de seguridad y en su posterior planificación no se han puesto las cerraduras eso se identificaría con una implementación insegura.  

### Identificación de CVEs
+ ####  CVE-2022-44004       	
Se descubrió un problema en BACKCLICK Professional 5.9.63. Debido a un diseño inseguro o a la falta de autenticación, los atacantes no autenticados pueden completar el proceso de restablecimiento de contraseña para cualquier cuenta y establecer una nueva contraseña.  

Es clasificada con una puntuación de 9.8 en CVSS, lo que la coloca en un nivel de seguridad ALTA.

+ #### CVE-2023-21367	
En Scudo, existe una forma posible de explotar ciertos problemas de lectura/escritura OOB en el montón debido a una implementación/diseño inseguro. Esto podría provocar la divulgación de información local sin necesidad de privilegios de ejecución adicionales. No se necesita la interacción del usuario para la explotación.

Es clasificada con una puntuación de 5.5 en CVSS, lo que la coloca en un nivel de seguridad MEDIA.

###  Contramedidas 
- Incorporar medidas de seguridad en todas las fases del desarrollo de software. Desde la simple planificación hasta el despliegue de la misma, incluyendo la colaboración con profesionales en el campo que pueden ir evaluando la seguridad de las diferentes etapas.

- Establecer y utilizar un catálogo de patrones de diseño seguros ("camino pavimnetado"), para que los equipos los utilicen en sus desarrollos sin tener que reinventar medidas de seguridad desde cero.

- Analizar los posibles ataques y vulnerabilidades en procesos clave (atenticación, control de acceso y lógica de negocio) para identificar y mitigar riesgos.

- Integre el lenguaje y los controles de seguridad en las historias de usuario.

- Implementar controles y validaciones de seguridad en todas las capas del sistema, desde el fronted (interfaz usuario) hasta backend (base de datos y servidores).

- Realizar pruebas para la comprobación de la resistencia a vulnerabilidades en los flujos críticos, y recopilar datos de buen y mal uso en cada capa de la aplicación.

- Separar las capas de sistema y red. Asegurando que cada parte tenga el nivel de seguridad adecuado según la función de la que se encargue. 

- Realizar un aislameinto de los tenants (usuarios o clientes) en todos los niveles del sistema, para que no puedan acceder a los datos o recursos de otros.

- Limitar el consumo de recursos por usuario o servicio.      

****

### Software and Data Integrity Failures

###  Descripción 

Los fallos de integridad en software y datos ocurren el código o la infraestructura no están correctamente protegidos contra modificaciones no autorizadas. Estan pueden provenir deaplicaciones que dependan de repositorios, plugins, bibliotecas... También puede suceder cuando una aplicación distribuye actualizaciones de software sin una previa verificación de las mismas, lo que puede facilitar a los atacantes dristribuir versiones maliciosas. 

### Identificación de CVEs
+ #### CVE-2022-31609

Esta era una vulnerabilidad crítica en el software NVIDIA vGPU, en la parte del Virtual GPU Manager. Esta falla permitia que una máquina invitada pudiese asignar recursos de los cuales no tenia autorización. Esto podía llevar a violaciones de integridad y confidencialidad de los datos, permitir accesos no autorizados o compremeter el sistema. 

Es clasificada con una puntuación de 7.8 en CVSS, lo que la coloca en un nivel de seguridad ALTA.

###  Contramedidas 
- Verificación del origen de los software o datos. Tendremos que comprobar que estos provienen de fuentes legitimas y no se han alterado.

- Tendremos que asegurarnos que las bibliotecas y dependencias que utilizamos provienen de repositorios confiables. Comentar que para cargos de alto riesgo es mejor utilizarlos en repositorios locales previamente analizados.

- Verifica la ausencia de vulnerabilidades conocidas con el uso de herramientas como OWASP Dependency Check u OWASP CycloneDX.

- Revisión de cambios en el código y las configuraciones para disminuir el riesgo de introducir código malicioso. 

- Asegúrese que su pipeline CI/CD posee adecuados controles de acceso, segregación y configuraciones que permitan asegurar la integridad del código a través del proceso de build y despliegue.

- Asegúrate de no enviar datos sin proteger (sin cifrado o firma) a clientes no confiables. Siempre utiliza algún método para verificar la integridad de los datos, como una firma electrónica, para detectar posibles modificaciones o reutilización de datos que hayan sido manipulados o serializados anteriormente.

****

## Conclusión

Durante la duración de este proyecto hemos estado analizando las vulnerabilidades más comunes que pueden afectar a las aplicaciones web de una empresa. Para entenderlo mejor, estas vulnerabilidades son como si hubiese un agujero en la seguridad de la empresa. Este agujero lo podrían usar los ciberdelincuentes para acceder a datos sensibles o causar algún problema en el sistema de la empresa.  

Hemos identificado numerosas vulnerabilidades, como los fallos criptográficos que permiten que datos importantes como contraseñas o información bancaria no tenga uan protección ajustada a su importancia; o el control de acceso roto , donde usuarios sin autorización pueden acceder y modificar información. También hemos podido ver problemas en la configuración de seguridad , donde los sistemas utilizan componentes desactualizados o estan mal configurados con lo que hacen que estos no sean seguros. 

Hemos añadido a cada explicación de las vulnerabilidades, casos concretos o ejemplos llamados CVE. Estos son fallos que han sido resgitrados y que se han ido descrubrierto en algún sistema. Cada uno tendrá una gravedad diferente y dependiendo de lo críticas que sean causará más o menos problemas.

A parte de definir y poner ejemplo de las vulnerabilidades, también hemos realizado contramedidas que pueden ayudar a minimizar los riesgos de estas. Algunas de las recomendaciones pasan por una correcta configuración de los permisos de acceso, actualización continua de todos los compenentes y sistemas, el uso de cifrado para datos sencibles o el monitoreo de las actividades de los sistemas para la detección de posibles ataques o fallos. Lo que queremos conseguir con estas medidas es anticiparnos a los posibles problemas que ocurran y responder en el menor tiempo posible si sucede algo.

En resumen, proteger las aplicaciones web es una parte muy importante porque son las que hacen de puente o punto de contacto entre el mundo exterior (clientes, usuarios...) con la empresa, por lo que cualquier vulnerabilidad podría tener graves consecuencias.
