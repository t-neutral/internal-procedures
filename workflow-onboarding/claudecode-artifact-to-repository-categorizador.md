# Piloto · Descomposición del Categorizador RE-VISTE, paso a paso

Recorrido guiado de la primera descomposición real de la empresa, pensado para hacerse en equipo y para que quien lo siga aprenda a la vez el trabajo y las herramientas. Acompaña al *Procedimiento · De artefacto a activo* (documento `11`), que da el marco; este documento lo aplica a un caso concreto y lo convierte en experiencia. Da por leídas la *Guía de trabajo diario Claude/Git* y el *Anexo B*.

Todo lo que aparece medido o extraído en estas páginas se ha comprobado sobre el fichero real `Categorizador_REVISTE_v6.html`. No hay cifras de ejemplo ni pasos teóricos: es lo que ocurre al abrir este artefacto.

---

## Paso 0 · Replantear antes de descomponer

Este paso no estaba en la primera versión del procedimiento y lo añade el piloto, porque descomponer sin replantear solo reordena los problemas en lugar de resolverlos. Antes de mover un solo dato conviene decidir qué forma *deberían* tener los datos, no limitarse a copiar la que tienen. La diferencia es la que hay entre mudarse ordenando las cajas viejas y mudarse aprovechando para tirar lo que no sirve.

El paso 0 no cierra esa decisión. Su trabajo es plantear las preguntas correctas para que el equipo las responda durante el piloto, con el artefacto delante y criterio sobre la mesa. Cerrar la estructura antes de haberla tanteado sería el mismo error que se quiere evitar, cometido antes de empezar.

Hay un principio que gobierna todas las respuestas de este paso y conviene tenerlo escrito antes que las preguntas. La flexibilidad tiene un precio, y se paga en simplicidad. Un modelo que intenta anticipar cualquier evolución posible acaba tan genérico que solo un programador lo entiende, y eso convertiría un artefacto que una persona no técnica puede mantener en una arquitectura que nadie del equipo toca sin ayuda. La flexibilidad que conviene no es la máxima imaginable, es la máxima que el equipo pueda seguir manteniendo por sí mismo. Cada respuesta del paso 0 se mide contra esa vara.

### A. Qué se sabe ya del artefacto antes de preguntar nada

Conviene entrar a las preguntas con el diagnóstico que ya existe, para no partir de cero. El Categorizador guarda sus datos en seis bloques que, mirados de cerca, son una sola tabla de códigos vista desde seis ángulos. Todos comparten la misma clave, el código CN8, y cada bloque guarda una porción distinta de información sobre ese código: uno el peso estadístico, otro la descripción oficial y la categoría, otro la subfamilia comercial, otro el enriquecimiento comercial.

El código CN8 se repite hoy físicamente en tres de esos bloques. Esa repetición es el origen de un desajuste que ya se detectó: el universo tiene 460 códigos, pero la tabla de pesos solo 415. Cuando el mismo código vive en varias listas que se mantienen por separado, nada impide que aparezca en una y falte en otra. El problema del artefacto no es de velocidad ni de tamaño (las descripciones no tienen ni una duplicada y ocupan poco); es de integridad. Rediseñar aquí no busca aligerar, busca que sea imposible que un código exista a medias.

### B. Las preguntas que el piloto debe responder

Las preguntas se agrupan por el tipo de decisión que abren. Ninguna se responde en este documento; se responden haciendo.

Sobre la estructura de los datos, la pregunta central es si conviene una tabla maestra de códigos, donde cada código viva una sola vez, acompañada de tablas satélite que se actualicen por separado (los pesos por su lado, el mapa comercial por el suyo, el enriquecimiento por el suyo), todas unidas por la clave común. La pregunta que lo decide no es de principios sino de hechos: de todo lo que contiene el artefacto, ¿qué es lo que cambia con más frecuencia, y con qué ritmo distinto cambia cada cosa? Los pesos se rehacen cuando llegan datos de un año nuevo. El mapa comercial cambia cuando se reorganizan subfamilias. El enriquecimiento crece cuando se documentan más capítulos. Si cada uno cambia a su ritmo, cada uno merece poder actualizarse sin tocar los demás; y eso es lo que una estructura de maestra más satélites permite. La expectativa de "máxima flexibilidad y capacidad de evolución" se traduce en esta pregunta concreta, no en una consigna general.

Sobre qué guardar en el repositorio y qué dejar fuera, la pregunta la resuelve la frontera del *Anexo B* aplicada dato a dato. Cinco de los seis bloques son texto que evoluciona y que gana estando versionado. El sexto insumo, el fichero maestro de códigos arancelarios oficiales, es una hoja de cálculo de casi tres megas que nadie edita a mano: se consulta, no se mantiene. La pregunta para cada dato es si es algo que la empresa edita línea a línea o algo que recibe de fuera y solo consulta; lo primero va al repositorio, lo segundo se referencia pero vive donde corresponde a un fichero de ese tipo.

Sobre guardar y retomar el trabajo, hay dos necesidades distintas que hoy el artefacto atiende con un solo mecanismo, y conviene separarlas. Una es la foto fija: congelar un mapa concreto para archivarlo o compartirlo, que es lo que hoy hace la exportación a un fichero y que encaja como entregable versionable. Otra es la memoria de sesión: que el trabajo a medias sobreviva al cierre para poder retomar donde se dejó, incluso semanas después y desde otro equipo. La decisión de dónde vive esa memoria ya se tomó, y está razonada en la guía de creación de artefactos: para un artefacto de una sola persona que se retoma en el tiempo, el nivel adecuado es un fichero de estado, el mismo mecanismo que la exportación ya usa, sin base de datos ni infraestructura. El navegador se quedaría corto (no viaja de un equipo a otro) y una base de datos sería excesiva (haría falta solo si varias personas editaran la misma sesión a la vez, y entonces el artefacto ya sería cosa del equipo dev). El piloto solo tiene que confirmar que ese fichero de estado cubre el caso en la práctica.

Sobre el límite de la ambición, la última pregunta es transversal y se hace a cada respuesta de las anteriores: lo que se está proponiendo, ¿lo va a poder mantener una persona del equipo sin formación técnica, como se mantuvo el artefacto original? Si la respuesta es no, la propuesta es demasiado ambiciosa aunque sea elegante, y conviene una versión más simple. Esta pregunta es la que impide que el paso 0 se convierta en una excusa para sobre-diseñar.

El paso 0 se cierra cuando estas preguntas tienen respuesta anotada en el repositorio, con el porqué de cada decisión. Esa nota es el documento fundacional que la guía diaria espera encontrar al empezar en un proyecto. A partir de ahí, la descomposición de los pasos siguientes ya no reordena lo que había: construye hacia la estructura decidida.

## Paso 1 · Radiografía (ejecutada)

Con la estructura destino decidida en el paso 0, se pide a Claude Code que lea el artefacto y confirme qué hay dentro. Esto ya se ha ejecutado sobre el fichero real, y este es el resultado, que sirve de referencia de lo que se debe encontrar.

El fichero tiene unos 426.000 caracteres. Repartidos así: el 41% son datos, el resto es la lógica de cálculo y la interfaz en JavaScript, y una porción menor es el aspecto visual. Los seis bloques de datos, de mayor a menor, son la librería de enriquecimiento comercial (17,4%), el universo de códigos con sus descripciones (10,5%), los pesos estadísticos (8,7%), el mapa comercial (2,6%), el árbol de familias (1,4%) y los umbrales de las alertas (una fracción mínima). Las dos funciones de cálculo que son el corazón de la herramienta, la que pondera las estadísticas de una subfamilia y la que dispara sus alertas, están claramente delimitadas y no dependen de la interfaz.

La instrucción a Claude Code en este paso es de lectura, no de cambio: *"Lee este artefacto y dime qué bloques de datos contiene, dónde empieza y termina cada uno, y qué funciones de cálculo hay separadas de la interfaz. No cambies nada todavía."* El resultado se guarda como primer documento del proyecto y se cierra con un commit.

## Paso 2 · Sacar los datos a tablas (con una extracción ya probada)

Este paso construye la estructura decidida en el paso 0, un bloque cada vez, con su commit. Dos extracciones ya se han probado sobre el fichero real y enseñan dos aprendizajes que conviene anticipar.

El primero es una fricción técnica que aparece nada más empezar. Los datos embebidos en el HTML están escritos como objetos de JavaScript, no como el formato de intercambio que usan los ficheros de datos. La diferencia práctica es pequeña pero real: en el HTML, las etiquetas de cada campo van sin comillas, y al sacarlas a un fichero hay que ponérselas para que sea un fichero de datos válido. Los umbrales por defecto, por ejemplo, viven en el HTML como `{cv_max:0.60, ...}` y salen al fichero como `{"cv_max":0.60, ...}`. Claude Code hace esa conversión sin que haya que pedirla, pero conviene saber que ocurre, porque es el tipo de detalle que confunde si aparece sin aviso.

El segundo aprendizaje es el que justifica todo el ejercicio. La librería de enriquecimiento comercial vive hoy en dos sitios a la vez: dentro del HTML y en un fichero suelto que se trabajó aparte. Se ha comprobado que las dos copias tienen hoy exactamente las mismas 76 entradas, todavía idénticas. Ese "todavía" es la clave: están iguales hoy porque nadie las ha tocado por separado aún, pero nada garantiza que sigan iguales mañana. El momento de unificarlas es justo este, antes de que diverjan. Al sacar la librería a un único fichero y hacer que el artefacto lo lea de ahí, las dos copias se convierten en una, y el riesgo desaparece. Un dato, un sitio.

La instrucción por bloque es del tipo *"Saca la librería de enriquecimiento a su propio fichero de datos y haz que el artefacto lo lea desde fuera en lugar de tenerlo dentro. Confírmame que el artefacto sigue funcionando igual antes de pasar al siguiente bloque."* La decisión de qué bloque va al repositorio y cuál se queda fuera, la toma la persona con la frontera del *Anexo B*, no la herramienta.

## Paso 3 · Separar la lógica de la interfaz

Extraídos los datos, quedan las dos funciones de cálculo. Se piden a un fichero aparte, dejando la interfaz llamándolas desde fuera. El criterio para distinguir cálculo de interfaz es una pregunta que cualquiera puede aplicar sin ser técnica: ¿esta función seguiría teniendo sentido si la herramienta se viera completamente distinta? La que pondera medias y la que calcula alertas seguirían valiendo con cualquier pantalla; son lógica. Lo que solo tiene sentido con esta pantalla concreta es interfaz y se queda donde está.

Este es el paso de mayor riesgo, porque mover una regla de cálculo sin querer cambiarla estropearía los resultados sin que se note a simple vista. Por eso el paso siguiente es obligatorio.

## Paso 4 · Comprobar que nada ha cambiado (la comprobación exhaustiva)

Separar no es reescribir. Al terminar, la herramienta debe comportarse exactamente igual que antes. Abrir el HTML y ver que arranca es necesario, pero solo caza los fallos visibles; el fallo peligroso de una descomposición es el que no se ve, un cálculo que empieza a dar un número distinto con la pantalla idéntica. Como la salida de este artefacto alimenta el motor de la Tarifa Simplificada, un número que baila sin avisar es una tarifa mal calculada, no un detalle. Por eso la comprobación de este paso es obligatoria y tiene cuatro frentes, no uno.

La comprobación se hace en Python, que es el lenguaje de verificación del taller. No exige programar: se le pide a Claude Code que ejecute cada frente y muestre las diferencias, si las hay. Mientras quede una sola diferencia sin explicar, la tarea no está cerrada.

### A. Los cuatro frentes

El primer frente es el visual, y es el más rápido: abrir el HTML tras cada evolución y confirmar que arranca, que las pantallas se ven, que se puede arrastrar un código y cambiar de modo sin que salte un error. Detecta lo que se rompe de forma evidente. No basta por sí solo, pero se hace siempre y el primero, porque si esto falla no tiene sentido comprobar lo demás.

El segundo frente es el de los números, el que de verdad protege lo que la herramienta hace. Antes de tocar nada se anotan los resultados que el artefacto original da en varios casos conocidos; después de cada cambio, se recalculan esos mismos casos sobre la versión nueva y se comparan. Los valores de referencia ya están calculados sobre el artefacto original y son estos tres, que sirven de patrón de lo que la versión descompuesta debe reproducir al dígito:

| Caso | n.º códigos | con peso | media ponderada | CV | concentración |
|---|---|---|---|---|---|
| COM-01 | 26 | 26 | 0,7057 | 0,2633 | 30,06% |
| COM-12 | 27 | 27 | 0,0920 | 0,5690 | 22,64% |
| COM-18 | 25 | 23 | 0,6300 | 0,2395 | 43,72% |

El detalle de COM-18, veinticinco códigos de los que solo veintitrés tienen peso, es justo el tipo de cosa que un cálculo mal reconstruido estropea (contando veinticinco en el denominador en vez de veintitrés) y que en pantalla no se vería. Si la versión nueva da 0,6300 de media en COM-18, la ponderación sigue bien; si da otra cosa, algo se ha movido.

El tercer frente es la integridad de los datos, que cobra sentido con la estructura de tabla maestra y satélites. Se comprueba que toda clave de una tabla satélite existe en la maestra (ningún peso ni asignación comercial huérfana, colgando de un código que no está en el universo) y que ningún código aparece duplicado dentro de su familia. Esta comprobación se ha ejecutado ya sobre el diseño destino: cero huérfanos y cero duplicados. Además, la estructura hace visible por fin el desajuste que antes se escondía, los cuarenta y cinco códigos del universo sin dato de peso, que pasan de problema latente a consulta de una línea.

El cuarto frente es la recuperación de sesión: que el trabajo guardado se recupere idéntico. Se toma un estado guardado, se carga y se vuelve a guardar, y se comprueba que el resultado es igual al de partida y que conserva los invariantes de la sesión (el número de subfamilias por familia, el contador de subfamilias manuales, el modo activo, y la ausencia de códigos duplicados). Este ciclo se ha probado sobre el estado real y se conserva idéntico. Importa porque una descomposición puede alterar sin querer la forma en que el estado se serializa, y eso solo se detecta haciendo el viaje de ida y vuelta completo.

### B. El ritmo: comprobar en cada commit, no solo al final

Los cuatro frentes no se dejan para el final. Se corren después de cada bloque de datos extraído y después de separar la lógica, es decir, en cada commit importante. Esta es la ventaja de descomponer poco a poco: si los números cuadran tras extraer cinco bloques y dejan de cuadrar tras el sexto, se sabe exactamente qué cambio lo rompió. Comprobar solo al final dice que algo se rompió, pero no dónde, y obliga a buscar en todo lo hecho.

Este paso 4, tal como queda descrito, es el patrón de comprobación del taller. Cuando se haya aplicado en este piloto y en el segundo o tercer artefacto, tendrá la forma estable que hoy todavía no se puede dar por definitiva, y ese será el momento de destilarlo en un skill que nazca ya probado. Fijarlo antes sería cerrar en piedra algo que el piloto existe para tantear. El método (anotar antes, recalcular después, comparar, ninguna diferencia sin explicar) es común a cualquier artefacto; los valores concretos son propios de cada uno, y por eso el skill podrá estandarizar el rigor pero no el contenido.

## Paso 5 · Documentar y dejarlo listo para el siguiente

El cierre convierte el resultado en algo que otra persona pueda retomar sin preguntar: el README que la guía diaria espera, con qué es la herramienta, dónde está cada tabla, dónde la lógica y cómo se comprueba que funciona. Se conserva el artefacto original como referencia, no se borra. A partir de aquí, actualizar un peso o afinar una regla es una tarea corriente sobre una base ordenada.

## Qué debería salir de este piloto

Más allá del Categorizador descompuesto, el piloto deja tres cosas para la empresa. Una estructura de datos decidida con criterio y no por defecto, que sirve de patrón para el siguiente artefacto. Una primera experiencia real del equipo con Claude Code y GitHub sobre un trabajo que importa. Y una versión corregida del procedimiento `11` y de este mismo documento, con los tropiezos reales ya incorporados, que es como debe madurar un procedimiento. La reflexión sobre cómo exportar todo esto al resto de la empresa se hace mejor después de haberlo recorrido una vez, no antes.

---

*T_NEUTRAL · Fuente en control de versiones: `12_piloto_categorizador_paso-a-paso.md`. La versión viva y editable reside en el repositorio de procedimientos; cualquier copia en otro formato es para consulta.*
