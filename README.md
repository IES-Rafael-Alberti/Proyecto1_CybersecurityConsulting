##  Insecure Design 
###  Descripción 
El **diseño inseguro** se refiere a una falla en la etapa de diseño o implementación de un sistema o software, en la que no se pensaron o incluyeron controles de seguridad necesarios para defenderse de posibles ataques.
Esto se suele confundir mucho con una implementación insegura, aunque no se refieren a la misma definición.

**Ejemplo**:  
Un ejemplo cotidiano podría ser el siguiente: una constructora realiza los planos de una casa, estructuración de cuartos, ventanas, puertas, etc. Si en la planificación, no preves el uso de puertas o ventanas con cerraduras, esto crea una vulnerabilidad que por muy bien que se construya posteriormente la casa siguiente cada paso de los planos, ladrones podrían entrar en ella debido a la falta de seguridad en la planificación. A esto se refiere con un diseño inseguro.  
Si por el contrario, en la planificación se han planificado estas medidas de seguridad y en su posterior planificación no se han puesto las cerraduras eso se identificaría con una implementación insegura.  

### Identificación de CVEs
+ ####  [CVE-2022-44004](https://www.cve.org/CVERecord?id=CVE-2022-44004) 
    + **Gravedad**: ALTA  
    + **Puntuación CVSS**: 9.8 (Base Score)  
    + **Descripción**: Se descubrió un problema en BACKCLICK Professional 5.9.63. Debido a un diseño inseguro o a la falta de autenticación, los atacantes no autenticados pueden completar el proceso de restablecimiento de contraseña para cualquier cuenta y establecer una nueva contraseña. 
    + **Contramedidas**: Tras una investigación hemos visto que no hay información relacionada con medidas para prevenir este CVE. Aunque viendo la fuente del problema habría algunas medidas interesantes.
        + Utilizar autenticación de multifactor.
        + Fortalecer los procesos de restablecimiento de contraseña.
        + Hemos encontrado un error similar que ocurrió en CISCO, en el cuál como en la mayoría de CVE nos aconseja actualizar el software a versiones donde se hayan parcheado dichos problemas. [Referencia](https://ostec.blog/es/generico/cve-2024-20419-vulnerabilidad-critica-en-cisco-smart-software-manager/#:~:text=Mitigaci%C3%B3n%20y%20correcci%C3%B3n)



+ #### [CVE-2023-21367](https://www.cve.org/CVERecord?id=CVE-2023-21367)	
    + **Gravedad**: MEDIA  
    + **Puntuación CVSS**: 5.5 (Base Score)  
    + **Descripción**: En Scudo, existe una forma posible de explotar ciertos problemas de lectura/escritura OOB en el montón debido a una implementación/diseño inseguro. Esto podría provocar la divulgación de información local sin necesidad de privilegios de ejecución adicionales. No se necesita la interacción del usuario para la explotación.
    + **Contramedida**:
        + La única contramedida que nos brindan es la de actualizar al siguiente parche para solucionar las fallas del sistema. [Referencia](https://source.android.com/docs/security/bulletin/android-14?hl=es)

###  Contramedidas 
- Incorporar medidas de seguridad en todas las fases del desarrollo de software. Desde la simple planificación hasta el despliegue de la misma, incluyendo la colaboración con profesionales en el campo que pueden ir evaluando la seguridad de las diferentes etapas.

- Establecer y utilizar un catálogo de patrones de diseño seguros ("camino pavimentado"), para que los equipos los utilicen en sus desarrollos sin tener que reinventar medidas de seguridad desde cero.

- Analizar los posibles ataques y vulnerabilidades en procesos clave (autenticación, control de acceso y lógica de negocio) para identificar y mitigar riesgos.

- Integre el lenguaje y los controles de seguridad en las historias de usuario.

- Implementar controles y validaciones de seguridad en todas las capas del sistema, desde el frontend (interfaz usuario) hasta backend (base de datos y servidores).

- Realizar pruebas para la comprobación de la resistencia a vulnerabilidades en los flujos críticos, y recopilar datos de buen y mal uso en cada capa de la aplicación.

- Separar las capas de sistema y red. Asegurando que cada parte tenga el nivel de seguridad adecuado según la función de la que se encargue. 

- Realizar un aislamiento de los tenants (usuarios o clientes) en todos los niveles del sistema, para que no puedan acceder a los datos o recursos de otros.

- Limitar el consumo de recursos por usuario o servicio.      

****

### Software and Data Integrity Failures

###  Descripción 

Los fallos de integridad en software y datos ocurren cuando el código o la infraestructura no están correctamente protegidos contra modificaciones no autorizadas. Estas pueden provenir de aplicaciones que dependan de repositorios, plugins, bibliotecas... También puede suceder cuando una aplicación distribuye actualizaciones de software sin una previa verificación de las mismas, lo que puede facilitar a los atacantes distribuir versiones maliciosas.   

**Ejemplo**:  
Tú utilizas una aplicación y dicha actualización recibe actualizaciones de la compañía de la cuál ha sido creada y tu al recibir las notificaciones instalas dichas actualizaciones. Un día un atacante decide escribir código malicioso en una actualización y te la envía a tu teléfono. Tú como siempre, le das a actualizar la aplicación y el móvil ya ha sido infectado. Esto ha sido problema de que la aplicación no verificó de donde venía la actualización por lo que hay un fallo en el diseño y los datos del software. 

### Identificación de CVEs
+ #### [CVE-2022-31609](https://www.cve.org/CVERecord?id=CVE-2022-31609)
    + **Gravedad**: ALTA   
    + **Puntuación CVSS**: 7.8 (Base Score)  
    + **Descripción**: Esta era una vulnerabilidad crítica en el software NVIDIA vGPU, en la parte del Virtual GPU Manager. Esta falla permitía que una máquina invitada pudiese asignar recursos de los cuales no tenía autorización. Esto podría llevar a violaciones de integridad y confidencialidad de los datos, permitir accesos no autorizados o comprometer el sistema.
    + **Contramedida**: 
     + Como en la mayoría de CVEs las contramedidas propuestas son la actualización del software a uno más reciente y estar atentos a futuros parches. [Referencia](https://nvidia.custhelp.com/app/answers/detail/a_id/5383)

###  Contramedidas 
- Verificación del origen de los software o datos. Tendremos que comprobar que estos provienen de fuentes legítimas y no se han alterado.

- Tendremos que asegurarnos que las bibliotecas y dependencias que utilizamos provienen de repositorios confiables. Comentar que para cargos de alto riesgo es mejor utilizarlos en repositorios locales previamente analizados.

- Verifica la ausencia de vulnerabilidades conocidas con el uso de herramientas como OWASP Dependency Check u OWASP CycloneDX.

- Revisión de cambios en el código y las configuraciones para disminuir el riesgo de introducir código malicioso. 

- Asegúrese que su pipeline CI/CD posee adecuados controles de acceso, segregación y configuraciones que permitan asegurar la integridad del código a través del proceso de build y despliegue.

- Asegúrate de no enviar datos sin proteger (sin cifrado o firma) a clientes no confiables. Siempre utiliza algún método para verificar la integridad de los datos, como una firma electrónica, para detectar posibles modificaciones o reutilización de datos que hayan sido manipulados o serializados anteriormente.

****

## Conclusión

Durante la duración de este proyecto hemos estado analizando las vulnerabilidades más comunes que pueden afectar a las aplicaciones web de una empresa. Para entenderlo mejor, estas vulnerabilidades son como si hubiera un agujero en la seguridad de la empresa. Este agujero lo podrían usar los ciberdelincuentes para acceder a datos sensibles o causar algún problema en el sistema de la empresa.  

Hemos identificado numerosas vulnerabilidades, como los fallos criptográficos que permiten que datos importantes como contraseñas o información bancaria no tenga una protección ajustada a su importancia; o el control de acceso roto , donde usuarios sin autorización pueden acceder y modificar información. También hemos podido ver problemas en la configuración de seguridad , donde los sistemas utilizan componentes desactualizados o están mal configurados con lo que hacen que estos no sean seguros. 

Hemos añadido a cada explicación de las vulnerabilidades, casos concretos o ejemplos llamados CVE. Estos son fallos que han sido registrados y que se han descubierto en algún sistema. Cada uno tendrá una gravedad diferente y dependiendo de lo críticas que sean causará más o menos problemas.

A parte de definir y poner ejemplo de las vulnerabilidades, también hemos realizado contramedidas que pueden ayudar a minimizar los riesgos de estas. Algunas de las recomendaciones pasan por una correcta configuración de los permisos de acceso, actualización continua de todos los componentes y sistemas, el uso de cifrado para datos sensibles o el monitoreo de las actividades de los sistemas para la detección de posibles ataques o fallos. Lo que queremos conseguir con estas medidas es anticiparnos a los posibles problemas que ocurran y responder en el menor tiempo posible si sucede algo.

En resumen, proteger las aplicaciones web es una parte muy importante porque son las que hacen de puente o punto de contacto entre el mundo exterior (clientes, usuarios...) con la empresa, por lo que cualquier vulnerabilidad podría tener graves consecuencias.