
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
+ 
### CVE - 2024-26092
Adobe experience Manager versión 6.5.20 y anterior estan afectados por una vulnerabilidad Cross-Site Scripting que puede aprovechar un atacante para inyectar scripts maliciosos en campos de formularios vulnerables.


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

### Contramedidas

+ Eliminar las dependencias, funciones, archivos y documentación en desuso.
+ Comprobar continuamente las versiones de los componentes y sus dependencias en busca de partes desactualizadas.
+ Revisar de forma frecuente el Common Vulnerability and Exposures(CVE) para corregir lo antes posible nuevas vulnerabilidades en nuestros componentes.
+ Obtener solo de fuentes seguras los componentes que forman nuestro sistema.
