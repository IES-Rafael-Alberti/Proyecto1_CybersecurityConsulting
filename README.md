# Proyecto1_CybersecurityConsulting
## Introducción
La empresa TrustShield Financial nos ha contratado para la realización de un análisisde su estructura y así identificar vulnerabilidades que puedan poner en peligro la confidencialidad, integridad y disponibilidad de sus datos.

Hemos decidido centrarnos en las vulnerabilidades de sus aplicaciones web ya que esta es la cara que da la empresa a internet, y por lo tanto, a gran parte de sus usuarios y a posibles atacantes.

Las categorías de vulnerabilidad han sido elegidas por su número de incidentes en los últimos años y como de graves serían para TrustShield Financial en caso de sufrirlas.
## Categorías de vulnerabilidades
### Security logging and monitoring failures
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