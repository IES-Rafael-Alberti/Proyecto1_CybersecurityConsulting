# **Proyecto1_CybersecurityConsulting**

## **Insecure Design**
### **Descripción**
El **diseño inseguro** se refiere a una falla en la etapa de diseño o implementación de un sistema o software, en la que no se pensaron o incluyeron controles de seguridad necesarios para defenderse de posibles ataques.
Esto se suele confundir mucho con una implementación insegura, aunque no se refieren a la misma definición.

Un ejemplo contidiano podriía ser el siguiente: una constructora realiza los planos de una casa, estructuración de cuartos, ventanas, puertas, etc. Si en la planificación, no preves el uso de puertas o ventanas con cerraduras, esto crea una vulnerabilidad que por muy bien que se construya posteriormente la casa siguiente cada paso de los planos, ladrones podrían entrar en ella debido a la falta de seguridad en la planificación. A esto se refiere con un diseño inseguro.  
Si por el contrario, en la planificación se han planificado estas medidas de seguridad y en su posterior planificación no se han puesto las cerraduras eso se identificaría con una implementación insegura.  

### **CVE**
#### **CVE-2022-44004**      	
Se descubrió un problema en BACKCLICK Professional 5.9.63. Debido a un diseño inseguro o a la falta de autenticación, los atacantes no autenticados pueden completar el proceso de restablecimiento de contraseña para cualquier cuenta y establecer una nueva contraseña.  

Es clasificada con una puntuación de 9.8 en CVSS, lo que la coloca en un nivel de seguridad ALTA.

#### CVE-2023-21367	
En Scudo, existe una forma posible de explotar ciertos problemas de lectura/escritura OOB en el montón debido a una implementación/diseño inseguro. Esto podría provocar la divulgación de información local sin necesidad de privilegios de ejecución adicionales. No se necesita la interacción del usuario para la explotación.

Es clasificada con una puntuación de 5.5 en CVSS, lo que la coloca en un nivel de seguridad MEDIA.

### **Contramedidas**
- Incorporar medidas de seguridad en todas las fases del desarrollo de software. Desde la simple planificación hasta el despliegue de la misma, incluyendo la colaboración con profesionales en el campo que pueden ir evaluando la seguridad de las diferentes etapas.

- Establecer y utilizar un catálogo de patrones de diseño seguros ("camino pavimnetado"), para que los equipos los utilicen en sus desarrollos sin tener que reinventar medidas de seguridad desde cero.

- Analizar los posibles ataques y vulnerabilidades en procesos clave (atenticación, control de acceso y lógica de negocio) para identificar y mitigar riesgos.

- Integre el lenguaje y los controles de seguridad en las historias de usuario.

- Implementar controles y validaciones de seguridad en todas las capas del sistema, desde el fronted (interfaz usuario) hasta backend (base de datos y servidores).

- Realizar pruebas para la comprobación de la resistencia a vulnerabilidades en los flujos críticos, y recopilar datos de buen y mal uso en cada capa de la aplicación.

- Separar las capas de sistema y red. Asegurando que cada parte tenga el nivel de seguridad adecuado según la función de la que se encargue. 

- Realizar un aislameinto de los tenants (usuarios o clientes) en todos los niveles del sistema, para que no puedan acceder a los datos o recursos de otros.

- Limitar el consumo de recursos por usuario o servicio.      
<br>

## Software and Data Integrity Failures

### **Descripción**

Los fallos de integridad en software y datos ocurren el código o la infraestructura no están correctamente protegidos contra modificaciones no autorizadas. Estan pueden provenir deaplicaciones que dependan de repositorios, plugins, bibliotecas... También puede suceder cuando una aplicación distribuye actualizaciones de software sin una previa verificación de las mismas, lo que puede facilitar a los atacantes dristribuir versiones maliciosas. 

### **CVE**
#### **CVE-2022-31609**

Esta era una vulnerabilidad crítica en el software NVIDIA vGPU, en la parte del Virtual GPU Manager. Esta falla permitia que una máquina invitada pudiese asignar recursos de los cuales no tenia autorización. Esto podía llevar a violaciones de integridad y confidencialidad de los datos, permitir accesos no autorizados o compremeter el sistema. 

Es clasificada con una puntuación de 7.8 en CVSS, lo que la coloca en un nivel de seguridad ALTA.

### **Contramedidas**
- Verificación de origen: Utiliza firmas digitales para confirmar que el software o los datos provienen de fuentes legítimas y no han sido modificados.

- Uso de repositorios confiables: Asegúrate de que las bibliotecas y dependencias se obtienen de repositorios confiables. Para perfiles de riesgo alto, considera alojarlas en un repositorio interno que haya sido analizado previamente.

- Análisis de vulnerabilidades: Implementa herramientas de análisis de componentes de terceros, como OWASP Dependency Check o OWASP CycloneDX, para detectar vulnerabilidades conocidas en tus dependencias.

- Revisión de cambios: Establece un proceso de revisión de cambios en el código y configuraciones para minimizar el riesgo de introducir código malicioso en tu pipeline.

- Controles en el pipeline CI/CD: Asegúrate de que tu pipeline de CI/CD tenga controles de acceso adecuados, segregación de funciones y configuraciones que protejan la integridad del código durante el proceso de construcción y despliegue.

- Seguridad de datos: No envíes datos sin cifrar o firmar a clientes no confiables sin alguna forma de verificación de integridad, como una firma electrónica, para detectar modificaciones o reutilización no autorizada de datos serializados.