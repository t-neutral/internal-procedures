# Procedimiento · De artefacto a activo: descomponer un artefacto en código y datos

Guía operativa para convertir un artefacto ya creado (un HTML autónomo, con sus datos y su lógica dentro de un solo fichero) en un proyecto versionado, con el código y los datos separados y documentados. Aplica a cualquier artefacto del taller de prototipado, sea cual sea su contenido. Es una guía de un tipo de trabajo concreto, no un documento de fondo: da por leídos el documento troncal *Entornos de trabajo*, el *Anexo B (Git y GitHub)* y la *Guía de trabajo diario Claude/Git*, y solo desarrolla lo que esas guías no cubren.

Este procedimiento cubre la exportación de algo que ya existe. La decisión de arquitectura de un artefacto que aún no se ha construido (qué stack, qué forma de datos, cómo se guarda el trabajo) es un trabajo distinto, previo, y vive en la guía de creación de artefactos desde cero. Si el artefacto que se va a descomponer se construyó sin ese criterio de partida, conviene revisar su arquitectura antes de exportarlo; las preguntas para hacerlo están en esa guía de creación, y no se repiten aquí.

## 1. Qué problema resuelve este procedimiento y cuál no

Un artefacto recién salido de Claude es un logro y una trampa a la vez. Es un logro porque una persona sin formación técnica ha construido una herramienta que calcula, agrupa y decide. Es una trampa porque todo lo que hace vive dentro de un único fichero HTML: la lógica de cálculo, los datos sobre los que calcula y la interfaz que lo muestra están mezclados en el mismo sitio. Mientras eso siga así, el artefacto es una funcionalidad que funciona hoy, no un activo del que la empresa pueda fiarse mañana.

La diferencia se ve en cuanto el dato cambia. Imagínese un artefacto que consulta una tabla de tarifas y que, por la forma en que se construyó, guarda esa tabla en dos lugares a la vez: una copia dentro del propio HTML y otra en un fichero aparte que en algún momento se trabajó por separado. Son la misma tabla, pero nada garantiza que las dos copias se mantengan iguales con el tiempo. El día que una se actualice y la otra no, habrá dos verdades y ninguna forma automática de saber cuál vale. Ese es el problema que la descomposición resuelve, y se resume en una regla: un dato, un sitio.

Conviene decir con claridad qué **no** es este procedimiento, porque la petición habitual esconde dos trabajos distintos bajo una sola frase. Subir el artefacto tal cual a un repositorio y empezar a versionarlo es sencillo, lo cubre la *Guía de trabajo diario Claude/Git* y no necesita esta guía. Descomponer el artefacto en piezas separadas es el trabajo de fondo, el que lo convierte en activo, y es el único que se documenta aquí. La honestidad sobre esa distinción evita la frustración de esperar que el segundo trabajo sea tan automático como el primero. No lo es. Pero tampoco exige programar: exige dirigir a Claude Code con criterio, que es una capacidad distinta y alcanzable.

## 2. La idea de fondo: tres cosas que hoy están juntas

Antes de tocar nada conviene entender por qué un artefacto se puede separar en piezas, porque esa comprensión es la que permite dirigir el trabajo en lugar de seguirlo a ciegas.

Todo artefacto de este tipo contiene tres materiales de naturaleza distinta, aunque a primera vista formen un bloque. Están **los datos**, que son las tablas sobre las que la herramienta opera: catálogos, parámetros, cualquier información que la herramienta consulta o produce. Está **la lógica**, que son las reglas de cálculo y decisión: cómo se pondera un resultado, qué dispara una alerta, cómo se clasifica un elemento. Y está **la presentación**, que es todo lo que se ve y se toca: los colores, las tarjetas, los botones, el arrastrar y soltar.

La proporción sorprende cuando se mide. En un artefacto típico de cálculo, buena parte del fichero son datos embebidos, otra buena parte es lógica, y el resto es la interfaz. Con frecuencia, cerca de la mitad del artefacto son datos y reglas que no tienen por qué vivir dentro de una página web, y que ganan mucho viviendo fuera de ella. Merece la pena medirlo en cada caso antes de decidir el plan, porque las proporciones orientan por dónde empezar.

La razón por la que esto encaja con el marco de la empresa está en el *Anexo B*: Git sabe comparar texto línea a línea y detectar quién cambió qué. Un dato en su propio fichero de texto se beneficia de eso por completo. El mismo dato enterrado en medio de miles de líneas de código de interfaz, no. Separar es lo que permite que el control de versiones haga su trabajo sobre lo que de verdad importa.

## 3. Antes de empezar: lo que esta guía añade a las que ya existen

La preparación del entorno (instalar, clonar un repositorio, entender qué es una rama o un commit) está resuelta en el *Anexo B* y en la *Guía de trabajo diario Claude/Git*. No se repite aquí. Quien no las haya leído, las lee antes de seguir; esta guía no tiene sentido sin ellas.

Lo que sí conviene añadir es una condición de partida propia de este trabajo. La descomposición no se hace sobre el artefacto en producción ni sobre la única copia que existe. Se hace sobre una copia dentro de un repositorio ya creado, en una rama propia, con el artefacto original guardado y a salvo. El principio es sencillo: mientras se descompone, la versión que funciona sigue intacta. Si algo sale mal a mitad de camino, no se ha perdido nada, porque el punto de partida sigue ahí, versionado y recuperable. Este es el mismo mecanismo de rama que describe la guía diaria, aplicado a un trabajo que dura varios días en lugar de unas horas.

Una segunda condición es tener a mano la documentación del artefacto, si existe. Cuando el artefacto viene con una guía técnica que describe cada dato y cada función, la descomposición se convierte en una tarea de horas en lugar de días, porque no hay que adivinar qué es cada cosa. Cuando esa documentación no existe, el primer trabajo es reconstruirla leyendo el artefacto con Claude, y conviene contarlo en la ficha de la tarea para que el tiempo estimado lo refleje.

## 4. El recorrido, paso a paso

La descomposición sigue cinco pasos en orden. Cada uno termina en un commit, de modo que el avance queda registrado a diario tal como pide la guía diaria, y en cualquier momento se puede ver hasta dónde se ha llegado. Ninguno de los cinco exige escribir código: en todos, el trabajo de la persona es decidir y revisar, y el de Claude Code es proponer, editar y ejecutar. La instrucción se le da en lenguaje natural.

### A. Radiografía del artefacto

El primer paso es entender qué hay dentro antes de mover nada. Se le pide a Claude Code que lea el artefacto y produzca un inventario: qué datos contiene, dónde empieza y termina cada uno, qué funciones de cálculo existen y qué parte es interfaz. El resultado es una lista, no un cambio; el fichero todavía no se toca.

Esa radiografía es la que revela las proporciones del apartado 2 y, sobre todo, la que identifica las costuras por donde separar: los bloques de datos bien delimitados, las funciones de cálculo independientes de la interfaz, y la parte de presentación que no contiene ninguna regla de negocio. Saber esto de antemano es lo que permite planear los pasos siguientes en lugar de improvisarlos.

Este paso cierra con un documento breve, guardado en el repositorio, que describe lo encontrado. Es la base del README que el proyecto tendrá al final.

### B. Sacar los datos a ficheros propios

Con el inventario delante, se extrae cada bloque de datos a su propio fichero. Los datos que son texto estructurado salen a ficheros que Git compara bien y que cualquiera puede abrir y leer sin abrir el artefacto entero. A Claude Code se le pide que extraiga un bloque, lo guarde en su fichero y ajuste el artefacto para que lo lea desde fuera en lugar de tenerlo dentro. Se hace un bloque cada vez, con su commit, de forma que si algo deja de funcionar se sabe exactamente qué cambio lo causó.

Aquí aparece la primera decisión que la persona debe tomar, no Claude. No todos los datos son iguales. La mayoría suelen ser texto que evoluciona y que gana estando en el repositorio. Pero a veces hay un fichero maestro que es una hoja de cálculo pesada que nadie edita a mano: una fuente externa que se consulta, no un texto que la empresa mantenga línea a línea. Ese no va al repositorio como los demás. La frontera del *Anexo B* lo resuelve: lo que evoluciona línea a línea y se revisa, a Git; lo que es un binario pesado y estable, se referencia desde el proyecto pero vive donde corresponde a un fichero de Office, con las reglas del *Anexo A*. Confundir los dos casos es el error más común de este paso, y por eso la decisión la toma una persona con criterio sobre el dato, no la herramienta.

El caso del dato duplicado, el que se mencionó al principio, se resuelve precisamente aquí: al sacar la tabla a un único fichero y hacer que el artefacto lo lea de ahí, las dos copias se convierten en una. Un dato, un sitio.

### C. Separar la lógica de la presentación

Extraídos los datos, queda separar las reglas de cálculo de la interfaz que las muestra. Las funciones que calculan, ponderan, clasifican o deciden son el corazón de la herramienta y no dependen de ningún color ni de ningún botón; pueden vivir en su propio fichero, y deben, porque son el activo técnico que la empresa quiere proteger y reutilizar. La interfaz, por su parte, se queda con lo suyo: mostrar y recoger lo que el usuario hace.

A Claude Code se le pide que mueva las funciones de cálculo a un fichero aparte y deje la interfaz llamándolas desde fuera. El criterio para saber qué es cálculo y qué es interfaz lo da una pregunta simple que la persona puede aplicar sin ser técnica: ¿esta función seguiría teniendo sentido si la herramienta se viera completamente distinta? Si la respuesta es sí, es lógica y va al fichero de cálculo. Si solo tiene sentido con esta pantalla concreta, es presentación.

Este paso es el que más se beneficia de la validación que describe la sección 5, porque mover una regla de cálculo sin querer cambiarla es el riesgo mayor de toda la descomposición.

### D. Comprobar que nada ha cambiado de comportamiento

Separar no es reescribir. Al terminar los pasos B y C, la herramienta debe producir exactamente los mismos resultados que producía el artefacto original; si un cálculo da un número distinto, la descomposición ha introducido un error y hay que encontrarlo antes de seguir. Esta comprobación es obligatoria y es la que distingue un trabajo serio de uno que solo parece terminado.

La forma de hacerla no requiere programar. Se toman unos cuantos casos del artefacto original con su resultado conocido y se comprueba que la versión descompuesta da los mismos. Cuando el artefacto trae casos de prueba documentados con sus valores esperados, el trabajo está medio hecho; cuando no los trae, se generan antes de empezar a descomponer, anotando qué da el original en varias situaciones, para tener contra qué comparar después. A Claude Code se le pide que ejecute esa comprobación y muestre las diferencias, si las hay. Mientras haya una sola diferencia sin explicar, la tarea no está cerrada.

### E. Documentar y dejar el proyecto listo para otros

El último paso convierte el resultado en algo que otra persona pueda retomar sin preguntar. Se escribe el README que la *Guía de trabajo diario Claude/Git* espera encontrar al empezar en un proyecto: qué es la herramienta, qué produce, dónde está cada dato, dónde está la lógica, cómo se comprueba que funciona. Se recogen las convenciones que se hayan ido fijando (cómo se nombran los ficheros de datos, en qué idioma van los mensajes de commit) y se anota lo que quedó pendiente. El artefacto original se conserva en el repositorio como referencia de partida, no se borra.

A partir de aquí el proyecto entra en el flujo normal de la guía diaria, y cualquier cambio futuro (un dato que se actualiza, una regla que se afina) es una tarea corriente sobre una base ordenada, no una cirugía sobre un bloque único.

## 5. La red de seguridad: por qué esto se puede hacer sin ser programadora

Toda la descomposición descansa en una garantía que ya está en las guías existentes y que conviene tener presente en cada paso. Cada cambio se hace en una rama, no sobre la versión validada; cada bloque extraído es un commit propio; y la comprobación del paso D confirma que el comportamiento no ha cambiado. Las tres cosas juntas significan que ningún error es irreversible: siempre se puede volver al commit anterior, y siempre se sabe qué cambio causó qué. Este es el mismo mecanismo de la guía diaria, y es lo que permite que una persona no técnica dirija un trabajo técnico sin miedo a romper nada de forma definitiva.

El reparto de papeles es el mismo que describe la guía diaria, aplicado a este trabajo concreto. La persona decide qué dato sale, dónde va y qué cuenta como cálculo frente a presentación; revisa que cada paso tenga sentido; y juzga si el resultado es correcto. Claude Code lee, propone, extrae, edita y ejecuta los comandos de Git, explicando siempre qué hace. La mecánica la lleva la herramienta; el criterio lo pone la persona. Que un artefacto se haya construido sin conocimientos técnicos avanzados demuestra que ese criterio existe; descomponerlo solo lo aplica a una tarea distinta.

## 6. Cuándo parar y preguntar

La autonomía tiene el mismo límite sano que fija la guía diaria, con un par de situaciones propias de este trabajo. Conviene detenerse y consultar cuando la comprobación del paso D da una diferencia que no se explica y no se localiza su origen; cuando no está claro si un dato es texto que debe ir al repositorio o un binario que debe quedarse fuera, y la duda persiste tras aplicar la frontera del *Anexo B*; cuando al separar la lógica aparece una función que mezcla cálculo y presentación de forma que no se deja separar limpiamente; y cuando el artefacto no tiene documentación previa y reconstruirla está llevando más tiempo del que la tarea tenía previsto. En los cuatro casos, la vía es la de siempre: abrir una ficha describiendo el bloqueo, o preguntar en el contexto del proyecto. Preguntar a tiempo evita rehacer, que en este trabajo cuesta más que en el ofimático.

## 7. Este procedimiento como formación

El recorrido descrito es, a la vez, la forma de descomponer un artefacto y una de las primeras experiencias prácticas del equipo con Claude Code y GitHub sobre un trabajo con sentido propio. Esa doble función es deliberada. Se aprende el ciclo de ramas, commits y pull requests de la guía diaria haciéndolo sobre algo que a la empresa le importa, no sobre un ejercicio de prueba que se tira después. El primer artefacto que se lleve entero por este camino es el proyecto piloto en el sentido que describe la sección 7 de la guía diaria: el primero que recorre el proceso completo, en equipo, observando qué cuesta y qué falla, y ajustando el procedimiento con lo aprendido.

De ese pilotaje debería salir una versión revisada de esta misma guía, con los tropiezos reales de la primera descomposición ya incorporados. Es el modo correcto de madurar un procedimiento: escribir la primera versión con lo que se sabe, y corregirla con lo que se aprende haciéndola. Esta es esa primera versión.

*T_NEUTRAL · Fuente en control de versiones: `11_procedimiento_descomposicion-artefactos.md`. La versión viva y editable reside en el repositorio de procedimientos; cualquier copia en PDF u otro formato es para consulta.*
