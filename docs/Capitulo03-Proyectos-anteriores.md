# Capítulo 3: Liberar un proyecto anterior

**Nunca es demasiado tarde**

![He cometido un gran error](https://media.opennews.org/fieldguides/open-sourcing/error.jpg)

En el [capítulo 2](Capitulo02-Empezar-proyecto-nuevo.md) vimos cómo comenzar un proyecto nuevo de código abierto. Obtuviste el visto bueno para liberarlo desde el principio y por el camino aprendiste la importancia de conocer al público de la herramienta, te aseguraste de que ya no hubiese una solución mejor en el mundo y te convenciste de los beneficios de trabajar en público.

O no.

Quizás tú o tu organización ya habían comenzado a trabajar en un proyecto de software *sin* hacerlo público desde el principio. No sería el primer caso. La mayoría de los proyectos comienzan con código cerrado.

Eso no quita que todavía haya quienes puedan beneficiarse de tu trabajo. Lo que es más importante, incluso así puedes aprovechar las ventajas de liberar el código de tu aplicación, o parte de tu base de código en forma de librería. Lo único que necesitarás es un poco de preparación y convencer a tu organización de que hacer esta transición es algo positivo.

## Qué esperar

En este capítulo examinaremos las decisiones a tomar para liberar el código de un proyecto que ya existe. Hablaremos de los potenciales beneficios para ti y los demás, discutiremos los pasos concretos que deberás seguir para higienizar o refactorizar tu aplicación, y finalmente, navegaremos por una serie de posibles objeciones y cómo responder a ellas.

## Qué han hecho los demás

La excelente guía de Karl Fogel, *Producción de software de código abierto* tiene toda una [sección](http://producingoss.com/en/opening-closed-projects.html) dedicada exclusivamente a la liberación de proyectos cerrados. El trabajo de Karl no es para medios de prensa específicamente, pero es útil en general para cualquier proyecto de código abierto.

# Consideraciones prácticas antes de comenzar

## ¿Necesitas liberar todo el proyecto? 

Muchos proyectos que comienzan con código cerrado incluyen partes que son tan específicas para el flujo de trabajo de tu organización que no serían útiles para nadie más. También puede que incluyan componentes propietarios que no quieres exponer en internet. Sin embargo, esto no debe ser una razón para renunciar a liberar tu código. Por ejemplo, puedes eliminar las partes que sean muy locales o estén protegidas por derechos de autor e incorporarlas como un módulo aparte que solo tus desarrolladores puedan ver. 

## ¿Está higienizado tu proyecto? 

![limpiar limpiar limpiar](https://media.opennews.org/fieldguides/open-sourcing/sanitary.png)

Aunque por lo general es buena práctica [separar configuración y código](https://12factor.net/config), es más fácil para los desarrolladores de programas de código cerrado romper esta regla. ¿Tu aplicación tiene claves o configuraciones en el repositorio que deberían ser exportadas al entorno o administradas de otra forma?

Aquí unos cuantos recursos: 

* Usa una herramienta como [*Git Secrets*](https://github.com/awslabs/git-secrets) de AWS para asegurarte de no estar publicando información confidencial por accidente. Y dado que tu historial de Git pudiera contener instancias antiguas de esa información en el repositorio, valora también borrarlo antes de hacer público el proyecto. 

* Limpia la información que pueda contener datos personales, incluyendo datos de muestra que estés enviando con el código. Usa [Poirot](https://github.com/emanuelfeld/poirot) para realizar búsquedas en el historial de revisiones de un repositorio y encontrar patrones textuales (ej. contraseñas, tókenes, datos de configuración, direcciones IP, números telefónicos y nombres).

Si estás liberando datos, querrás tener especial cuidado con esto también, particularmente con los datos de los usuarios. Incluso cuando los datos *parecen* haber sido anonimizados, con frecuencia pueden desanonimizarse (o sea, pueden analizarse a la inversa para vincularlos de nuevo al usuario original): 

> * En 2000, Latanya Sweeney [demostró](http://dataprivacylab.org/projects/identifiability/paper1.pdf) que el 87% de la población de EE.UU. puede ser identificada usando solamente su código postal, sexo y fecha de nacimiento. 

> * Incluso si la base de datos no incluye información de ubicación, edad o sexo, puede desanonimizarse usando factores aparentemente tan generales como favoritos y términos de búsqueda. Por ejemplo, en 2006, un conjunto de datos de las búsquedas de AOL permitió [identificar a una usuaria](http://www.nytimes.com/2006/08/09/technology/09aol.html) empleando simplemente los términos que había estado buscando en internet.

>  * En 2008, Narayanan y Shmatikov usaron técnicas de desanonimización para [identificar](https://www.cs.cornell.edu/~shmat/shmat_oak08netflix.pdf) a 500,000 suscriptores de Netflix, con un conjunto de datos que únicamente incluía fechas y valoraciones de películas.

## ¿Proyecto funcional o a medio desarrollar?

![](https://media.opennews.org/fieldguides/open-sourcing/makeitfit.gif)

Puede que el proyecto que quieres liberar ya tenga cierto camino recorrido pero no sea funcional todavía. ¿Tienes una hoja de ruta para las tareas que siguen? Publicar ese plan de desarrollo puede ayudar a los potenciales colaboradores a entender qué estás planeando construir, y decidir en qué otras áreas de la base de código pueden concentrarse. De esta forma podrás centrar tu atención únicamente en las funciones necesarias para llevar el proyecto a un estado funcional.

[TAREA: hipervincular a la sección de hojas de ruta]

## ¿Qué tipo de colaboración te interesa?

El tipo de colaboración que se necesita de la comunidad varía de un proyecto a otro. Quizás el tuyo es un proyecto maduro y lo único que estás buscando son informes de errores. Pero también podría ser algo tan nuevo que lo que estés buscando sea ayuda para refinar la interfaz de desarrollo. ¿Esperas recibir aportes en partes específicas? Deberías identificar en qué parte(s) del proyecto deseas que la gente ayude. ¿Estás buscando retroalimentación sobre los problemas centrales que el proyecto busca solucionar? Puedes aclararlo incluyendo una sección en el archivo README o creando una serie de tickets sobre esta preocupación. (Consulta el [capítulo 5](Capitulo05-Documentacion.md) sobre la documentación y el [capítulo 6](Capitulo06-Comunidad.md) sobre cómo trabajar en comunidad.)

## Manéjalo como si fuera un proyecto nuevo

Consulta el [capítulo 2](Capitulo02-Empezar-proyecto-nuevo.md) para ver las instrucciones sobre cómo nombrar el proyecto, elegir una licencia y evaluar a la competencia.

## Ejemplos

[TAREA: ¡añade tus ejemplos!]

## Últimos toques

Hablemos ahora de cómo preparar tu base de código y tu infraestructura para tener más probabilidades de éxito.

## Puntos a verificar

- [ ] Toma en cuenta a tu público y a tu competencia
- [ ] Prepara la argumentación de por qué tu organización se puede beneficiar de la liberación de este proyecto
- [ ] Identifica las partes del proyecto que *no deben* liberarse
- [ ] Higieniza tu código para asegurarte de no estar compartiendo secretos ni claves públicamente
- [ ] Comparte tu hoja de ruta, o al menos el estado en que se encuentra el proyecto, para informar a los posibles usuarios y colaboradores 
