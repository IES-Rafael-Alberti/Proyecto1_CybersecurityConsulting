
# Proyecto1_CybersecurityConsulting
## Security Misconfiguration
### Descripción

Los errores en la configuración son, a día de hoy, uno de los mayores problemas en la ciberseguridad. Se ha demostrado que el 90% de las aplicaciones tienen algún tipo de fallo de configuración, principalmente por el alto nivel de configuración de los programas actuales.
Entre los errores mas comunes, se encuentran los siguientes:
+ Falta de un bastionado de seguridad apropiado a lo largo de la aplicación unos permisos mal configurados en la nube.
+ Funciones habilitadas o instaladas innecesarias (puertos abiertos sin utilidad, privilegios...)
+ Cuentas por defecto con sus contraseñas activas y sin cambiar.
+ Manejo de errores inadecuado, como la exposición de mensajes de error detallados o que revelan información sensible.
+ Con sistemas actualizados, las ultimas funciones de seguridad están desactivadas o no configuradas de forma segura.
+ La configuración de seguridad del servidor de aplicaciones, frameworks, librerías, bases de datos... no tiene establecidas valores seguros.
+ El servidor no envía cabeceras seguras y/o directivas, o no están establecidas con valores seguros.
+ El software esta desactualizado o es vulnerable.

### CVE
#### CVE - 2024-26092
+ Gravedad: Alto
+ Puntuación CVSS: 6.1 (Base Score)
+ Adobe experience Manager versión 6.5.20 y anterior estan afectados por una vulnerabilidad Cross-Site Scripting que puede aprovechar un atacante para inyectar scripts maliciosos en campos de formularios vulnerables.

#### CVE-2024-35933
+ Gravedad: Alto
+ Puntuación CVSS: 7.8 (Base Score)
+ CVE-2024-35933 es una vulnerabilidad relacionada con el kernel de Linux, específicamente en la función Bluetooth de dispositivos Intel. El problema surge debido a una "dereferencia de puntero nulo" en la función btintel_read_version, que se usa para leer la versión de dispositivos Intel a través de Bluetooth.

### Contramedidas

+ Implementar un proceso de bastionado repetible?
+ Crear una plataforma con el contenido mínimo y necesario, evitando instalar características, componentes o documentación innecesaria.
+ Establecer una tarea que revise y actualice las configuraciones relacionadas con todas las notas de seguridad, actualizaciones y parches
+ Segmentar la arquitectura de la aplicación implementando contenedores o una lista de control de acceso en la nube (ACLs)
+ Enviar directivas de seguridad a los clientes.
+ Establecer un proceso que verifique la efectividad de la configuración de todos los entornos.

## Vulnerable and Outdated Components 
### Descripción

El problema de los compenentes vulnerables es uno de los mas dificiles de categorizar, pues no tienen CVEs asignados, teniendo por defecto una puntuacion de CWe de 5.0. 
Alguno de los errores que lo componen son:
+ No saber la versión de todos los componentes en uso. Esto incluye tambien las dependencias de los componentes.
+ Usar un software vulnerable, sin soporte o desactualizado. Incluyendo Sistema Operativo, servidor web, SGBD, APIs, librerias...
+ No escanear frecuentemente por vulnerabilidades y no suscribirse a boletines relacionados a los componentes que uses.
+ No asegurar las configuraciones de los componentes.
+ Los desarrolladores de software no comprueban las compatibilidades de su software con las librerias que han sido actualizadas o parcheadas. 

### CVE

#### CVE 2024-27395
+ Gravedad: Alto
+ Puntuación CVSS: 7.5 (Base Score)
+ CVE-2024-25103 es una vulnerabilidad que afecta al software AppSamvid, relacionado con el uso de componentes obsoletos y vulnerables. Un atacante que cuente con privilegios administrativos locales en el sistema objetivo podría explotar esta vulnerabilidad colocando archivos DLL maliciosos.

#### CVE-2022-24740
+ Gravedad: Alto
+ Puntuación CVSS: 6.5 (Base Score)
+ Entre las versiones 14.0.0-alpha.5 y 15.0.0-alpha.0 de Volto, es posible que un atacante, después de haber atraído a un usuario al sitio de ataque, reemplace su cookie de autenticación por la cookie de autenticación del atacante. Esto le daría al atacante control sobre la cuenta y los privilegios de ese usuario.

### Contramedidas

+ Eliminar las dependencias, funciones, archivos y documentación en desuso.
+ Comprobar continuamente las versiones de los componentes y sus dependencias en busca de partes desactualizadas.
+ Revisar de forma frecuente el Common Vulnerability and Exposures(CVE) para corregir lo antes posible nuevas vulnerabilidades en nuestros componentes.
+ Obtener solo de fuentes seguras los componentes que forman nuestro sistema.
