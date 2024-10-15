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
