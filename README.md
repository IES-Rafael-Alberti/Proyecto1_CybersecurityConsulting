# Proyecto1_CybersecurityConsulting
## Security logging and monitoring failures
### Descripción
Si no se monitoriza y registra las actividades de una aplicación web o no se hace de manera correcta y efectiva, no seremos capaces de detectar, escalar y responder a ataques. Esto puede ocurrir debido a que:
+ Los eventos que dejan constancia de quién los realiza, como los logins (ya sean exitosos o no) y transacciones de importancia (borrado de datos, modificación...), no quedan registrados.
+ Los avisos y errores no generan mensajes de log o no lo hacen de manera clara o adecuada.
+ No se monitorizan los logs de aplicaciones y APIs en busca de actividad sospechosa.
+ Los logs solo se almacenan localmente y con una sola copia.
+ No hay procesos de escalación de respuesta y umbrales de aviso o no son efectivos.
+ Los pentesting y escaneos de herramientas para pruebas dinámicas de seguridad de aplicaciones (DAST) no generan alertas.
+ La aplicación web no puede detectar, escalar o alertar de ataques en tiempo real o casi real.
Además, si los logs y alertas son visibles a los usuarios se puede filtrar información.
### Contramedidas
+ Todos los logins, control de accesos y fallos en la validación del input por parte del servidor se añadan a un log con el suficiente contexto sobre los usuarios para detectar cuentas sospechosas o maliciosas y se mantengan el tiempo suficiente para realizar un análisis forense tardío.
+ Asegurarse de que los logs se generan en un formato en el que un gestor de logs pueda comprender.
+ Asegurarse de que los datos de los logs están codificados correctamente para prevenir inyecciones o ataques a los sistemas de log o monitoreo.
+ Asegurarse de que transacciones de importancia tengan un seguimiento de auditoría con controles de integridad para prevenir que se manipulen o eliminen. Un ejemplo serían las tablas de bases de datos en las que solo se puede agregar.
+ Los equipos de DevSecOps deberían de monitorizar y alertar de manera efectiva para detectar actividad sospechosa y responder rápidamente.
+ Establecer o adoptar un plan de respuesta y recuperación a incidentes.
## Server-side request forgery (SSRF)
### Descripción
Los problemas de SSRF ocurren cuando una aplicación web realiza una consulta HTTP sin validar la URL suministrada por el usuario. Esto permite a un atacante forzar a la aplicación web a enviar una solicitud a la estructura interna de la red donde se aloja, incluso estando protegido por un firewall, VPN u otro tipo de lista de control de acceso a la red (ACL) y así extraer información sensible, escalar privilegios o ejecutar código remotamente en un servidor.

Con las facilidades y conveniencias proporcionadas a los usuarios por las aplicaciones web actuales el número de incidencias de SSRF está en aumento.
### CVE
Un ejemplo de vulnerabilidad por SSRF sería el registrado en CVE-2021-21973. Este CVE registra una vulnerabilidad encontrada en el cliente de vSphere debido a que no se valida correctamente las URLs en un plugin de vCenter Server. Esta vulnerabilidad puede ermitir a un atacante con acceso al puerto 443 obtener información sensible enviando una solicitud POST. Esta vulnerabilidad afecta a VMware vCenter Server (7.x antes de 7.0 U1c, 6.7 antes de 6.7 U3l y 6.5 antes de 6.5 U3n) y a VMware Cloud Foundation (4.x antes de 4.2 y 3.x antes de 3.10.1.2).
### Contramedidas
Desde la capa de red podríamos:
+ Separar los sistemas que se encargan de las solicitudes externas del resto de la red, reduciendo así el impacto de un SSRF.
+ Limitar el tráfico de nuestra intranet configurando nuestro firewall para que deniegue por defecto salvo para el tráfico esencial.

Desde la capa de aplicación podríamos:
+ Validar todo lo que introduzca un usuario, forzandolos a usar un esquema de URL, puerto y destino con una whitelist.
+ Deshabilitar redirecciones HTTP.
+ No devolver información sin validar al cliente.
