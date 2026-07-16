# Anexo A · Microsoft 365: dónde vive cada cosa
 
**Anexo del documento troncal *Entornos de trabajo*.**
Aplicable a todo el equipo. Es la base de la higiene documental de la empresa. Para la visión de conjunto de todos los entornos, ver el documento troncal. Para el día a día, ver la *Guía de trabajo diario con documentos de Office*.
 
---
 
## 1. Por qué este documento existe
 
SharePoint, OneDrive y Teams generan más confusión que cualquier otra herramienta de la empresa, y no por ser complicadas, sino por una razón que casi nadie conoce: **las tres son, por debajo, el mismo sistema de almacenamiento visto desde tres puertas distintas.** Cuando no se entiende esto, la misma empresa acaba con documentos duplicados en tres sitios, versiones que se pisan, enlaces que dejan de funcionar y la pregunta recurrente de "¿dónde estaba ese archivo?".
 
Este documento explica qué es cada herramienta, qué papel cumple, cómo se relacionan entre sí y qué hábitos mantienen el trabajo ordenado. Leerlo entero, una vez, ahorra decenas de "¿me reenvías el archivo?" a lo largo del año.
 
---
 
## 2. La idea que lo desatasca todo
 
Detrás de SharePoint, OneDrive y Teams hay una única tecnología de almacenamiento. Lo que cambia es la puerta por la que entras y para qué está pensada cada puerta.
 
```mermaid
flowchart TD
    STORE[(Almacenamiento Microsoft 365<br/>la misma tecnología por debajo)]
 
    STORE --> OD[OneDrive<br/>tu espacio personal]
    STORE --> SP[SharePoint<br/>los espacios compartidos]
 
    SP --- TEAMS[Teams<br/>no guarda archivos:<br/>es una ventana a SharePoint]
 
    OD --> OD1[Borradores propios<br/>Trabajo aún no compartido<br/>Cosas personales de trabajo]
    SP --> SP1[Documentos del equipo<br/>Entregables · Proyectos<br/>Todo lo colaborativo]
 
    style STORE fill:#2D5016,color:#fff
    style OD fill:#F4A460,color:#1A1A1A
    style SP fill:#6B8E4E,color:#fff
    style TEAMS fill:#FDF3E7,color:#1A1A1A
    style OD1 fill:#FDF3E7,color:#1A1A1A
    style SP1 fill:#F4F7F0,color:#1A1A1A
```
 
De este esquema salen las tres reglas que resuelven la mayoría de las dudas:
 
1. **OneDrive es tu cajón personal.** Lo que guardas ahí es tuyo, privado por defecto, y desaparece de la vista del equipo si tú te vas.
2. **SharePoint es el archivo común.** Lo que vive ahí es de la empresa, sobrevive a las personas y es donde debe estar cualquier cosa que otro pueda necesitar.
3. **Teams no guarda nada.** Cuando ves archivos en un canal de Teams, estás mirando una carpeta de SharePoint a través de una ventana. El archivo vive en SharePoint; Teams solo te lo enseña.
Si interiorizas solo esto, ya evitas el 80 % de los problemas.
 
---
 
## 3. OneDrive: tu espacio personal
 
### Qué es
 
OneDrive es tu cajón privado en la nube. Cada persona del equipo tiene el suyo, ligado a su cuenta. El espacio disponible por cuenta depende del plan de Microsoft 365 contratado; la cifra concreta se consulta en la administración de la cuenta.
 
### Para qué sirve
 
- Borradores y trabajo en curso que todavía no quieres que nadie vea.
- Notas personales de trabajo, tu propia organización.
- Archivos que son tuyos por rol pero no del equipo (tu firma, tus plantillas personales).
### Para qué NO sirve
 
- **Cualquier cosa que otra persona pueda necesitar.** Si un documento importa a alguien más, no puede vivir solo en tu OneDrive.
- **Entregables, documentos de proyecto, versiones finales.** Eso es de la empresa y va a SharePoint.
### El riesgo que hay que entender
 
Lo que está en tu OneDrive **depende de ti**. Si compartes un enlace a un archivo de tu OneDrive y luego lo mueves, lo renombras o dejas la empresa, ese enlace se rompe y el equipo pierde acceso. Por eso la regla es tajante: en cuanto algo deja de ser un borrador privado y pasa a ser trabajo compartido, se mueve a SharePoint. OneDrive es la sala de espera, no el destino.
 
---
 
## 4. SharePoint: el archivo de la empresa
 
### Qué es
 
SharePoint es el sistema donde viven los documentos compartidos, organizados en **sitios**. Un sitio es un espacio de almacenamiento con sus carpetas, sus permisos y sus miembros, pensado para un equipo o un propósito.
 
La diferencia esencial con OneDrive: **lo que está en SharePoint pertenece a la empresa, no a una persona.** Sobrevive a quien lo creó, mantiene su historial de versiones y sigue accesible aunque alguien se vaya.
 
### Para qué sirve
 
- Todos los documentos de proyecto, presentes y pasados.
- Entregables, memorias, plantillas oficiales, material que circula.
- Cualquier cosa que más de una persona necesite abrir, ahora o en el futuro.
### El historial de versiones, que casi nadie usa y debería
 
SharePoint guarda automáticamente el historial de cada documento. Puedes ver quién cambió qué y volver a una versión anterior. Esto tiene una consecuencia liberadora que corrige el peor hábito documental: **no hace falta guardar `propuesta_v3_final_FINAL_revisada.docx`.** El archivo se llama `propuesta.docx` y punto; sus versiones anteriores están guardadas por debajo, accesibles con un par de clics desde el menú del archivo (Historial de versiones). Poner fechas y "v_final" en el nombre es hacer a mano, y mal, lo que la herramienta ya hace sola y bien.
 
---
 
## 5. Teams: la ventana, no el almacén
 
### Qué es
 
Teams es donde el equipo conversa, se reúne y trabaja. Se organiza en **equipos** (por ejemplo, un equipo por área o por proyecto), y cada equipo tiene **canales** (subdivisiones temáticas dentro de él).
 
### La clave que resuelve la confusión
 
**Cada equipo de Teams crea automáticamente un sitio de SharePoint por detrás.** Cuando alguien sube un archivo a la pestaña "Archivos" de un canal, ese archivo no se guarda "en Teams": se guarda en el sitio de SharePoint de ese equipo, en una carpeta con el nombre del canal. Teams solo te lo muestra.
 
```mermaid
flowchart LR
    subgraph T[Lo que ves en Teams]
        CH[Canal 'Proyecto X'<br/>pestaña Archivos]
    end
 
    subgraph S[Dónde vive de verdad]
        SPS[Sitio de SharePoint<br/>del equipo]
        FOLD[Carpeta 'Proyecto X']
        SPS --> FOLD
    end
 
    CH -.es una ventana a.-> FOLD
 
    style T fill:#FDF3E7,color:#1A1A1A
    style S fill:#F4F7F0,color:#1A1A1A
    style SPS fill:#6B8E4E,color:#fff
    style CH fill:#F4A460,color:#1A1A1A
```
 
Esto tiene tres consecuencias prácticas que conviene tener claras:
 
- **Subir un archivo a un canal de Teams ES ponerlo en SharePoint.** No es un sitio distinto ni una copia. Es el mismo archivo, visto desde otra puerta. Por eso subir a Teams cuenta como archivar bien, siempre que sea el canal correcto.
- **No dupliques.** Si un documento ya está en el canal de Teams del proyecto, no hace falta "guardarlo también en SharePoint": ya está en SharePoint. Buscar el mismo archivo en las dos puertas y editar copias distintas es la causa número uno de versiones divergentes.
- **La conversación y el archivo van juntos.** La ventaja de trabajar desde Teams es que el chat del canal, las reuniones y los archivos del proyecto están en el mismo sitio. Esa es la razón de usar Teams como centro.
### Cada canal es una carpeta, y Teams te mete dentro de ella
 
Hay un detalle de esta relación que conviene entender bien, porque explica una confusión muy típica al montar la estructura. Dentro de la biblioteca de SharePoint de un equipo, **cada canal es una carpeta de primer nivel con el nombre del canal.** El canal General, que todo equipo trae de fábrica, es una carpeta llamada `General`. Si creas un canal «Línea A», aparece una carpeta `Línea A` junto a la anterior.
 
Lo que despista viene de aquí: **cuando entras a un canal desde Teams, la pestaña Archivos te lleva directamente al interior de la carpeta de ese canal, no a la raíz de la biblioteca.** Es decir, ves lo que hay *dentro* del canal, pero no ves lo que esté en la raíz del sitio, al lado de las carpetas-canal. Una carpeta que crees tú en la raíz del sitio (desde SharePoint web o desde el Explorador) no aparecerá en ningún canal de Teams, porque no está dentro de ninguna carpeta-canal; está un nivel por encima, donde Teams no mira.
 
La consecuencia práctica para organizar un equipo: **lo que quieras que el equipo vea desde Teams tiene que vivir dentro de la carpeta de un canal, no en la raíz del sitio.** Si un equipo va a trabajar todo desde su canal General, la estructura de carpetas va dentro de `General`. Si va a tener varios canales, cada uno con su trabajo, la estructura va dentro de cada canal. La raíz del sitio, la que solo se ve desde SharePoint web, se deja tranquila. Esto se desarrolla en la sección 11, al hablar de cómo organizar las carpetas.
 
### Para qué sirve cada parte de Teams
 
- **Chat de canal:** conversación del equipo sobre un tema, visible para todos los miembros. Preferible al chat privado para cualquier cosa que el equipo deba poder consultar después.
- **Chat privado:** conversaciones puntuales entre personas. Ojo: los archivos que compartes en un chat privado se guardan en TU OneDrive, no en SharePoint, con el riesgo del punto 3. Para archivos de trabajo, usa el canal, no el chat privado.
- **Reuniones:** las grabaciones, transcripciones y notas quedan asociadas al canal solo cuando la reunión se convoca desde el canal. La sección 7 explica por qué esto importa.
- **Pestañas:** puedes fijar en un canal un documento, un sitio o una herramienta de uso frecuente, para tenerlos a mano sin buscarlos.
---
 
## 6. Cómo se separan los espacios: equipos, sitios y permisos
 
Hasta aquí el anexo ha tratado SharePoint como un único archivo común. En una empresa con clientes y proveedores hay que afinar, porque no todo lo compartido es compartido con todos. Lo que un cliente puede ver y lo que se queda en casa viven en espacios distintos, y entender cómo se trazan esas fronteras evita el error más caro de todos: que alguien de fuera acabe viendo lo que no debía.
 
La pieza que lo ordena todo: **cada equipo de Teams tiene su propio sitio de SharePoint, con sus propios miembros y sus propios permisos.** No hay un SharePoint único con carpetas para todo; hay tantos sitios como equipos, cada uno una caja cerrada con su llave. Quien es miembro de un equipo ve su sitio; quien no lo es, no. Esa pertenencia es la frontera de permisos, y es la más fiable porque es la más simple: o estás dentro del equipo o no estás.
 
### A. Canales estándar y canales privados
 
Dentro de un mismo equipo, los canales no todos funcionan igual, y la diferencia es de seguridad, no de organización.
 
Un **canal estándar** lo ven todos los miembros del equipo. Los canales estándar de un equipo comparten los mismos permisos: si perteneces al equipo, ves todos sus canales estándar y sus archivos. Sirven para subdividir por temas un trabajo que todo el equipo puede ver.
 
Un **canal privado** tiene su propia lista de miembros, un subconjunto del equipo, y crea por debajo un almacenamiento separado que solo ese subconjunto ve. Es el mecanismo para tener, dentro de un equipo, una zona que no todos los miembros del equipo alcanzan.
 
La consecuencia práctica es importante cuando en un equipo hay gente de fuera (un cliente, un proveedor). Si el cliente es miembro del equipo, ve todos los canales estándar de ese equipo. Lo único que el cliente no ve es lo que esté en un canal privado del que no forma parte. Dicho de otro modo: en un equipo con un cliente dentro, la protección de lo interno descansa por completo en que ese material esté en un canal privado y no en uno estándar. Un canal estándar creado por descuido queda a la vista del cliente.
 
De ahí una regla que conviene fijar para cualquier equipo que incluya a alguien externo: **el canal nuevo se crea privado por defecto, y el canal general se trata como zona del externo, nunca como cajón interno.** Y una cautela de fondo: el material cuya filtración sería grave está más seguro en un equipo interno separado, al que el externo no pertenece, que en un canal privado dentro del equipo del externo. La frontera entre dos equipos distintos es física (se es miembro o no); la frontera de un canal privado es una configuración que hay que acertar cada vez que se crea un canal.
 
### B. Interno, cliente y proveedor: un espacio por frontera de confianza
 
De lo anterior se deriva cómo conviene repartir el trabajo en equipos. El criterio no es el proyecto, es quién puede ver qué. Cada frontera de confianza distinta pide su propio espacio.
 
Lo interno de la empresa vive en un equipo interno, del que solo forma parte el personal de T_NEUTRAL. Lo que se comparte con un cliente vive en un equipo con ese cliente, donde entra únicamente lo que el cliente puede ver. El trabajo interno de un proyecto de cliente, lo que se prepara antes de enseñárselo o lo que no se le enseña nunca, vive en el equipo interno, no en el del cliente. La misma lógica aplica a proveedores. Cuando un proveedor actúa de cara al cliente como parte de T_NEUTRAL, sigue siendo, en términos de permisos, alguien de fuera de la organización: se le da acceso a un canal o un equipo concretos, y ese acceso conviene tenerlo anotado, porque de puertas adentro cuenta como externo aunque de puertas afuera se presente con vosotros.
 
El material más sensible de la empresa (financiero, contratos, relación con socios y bancos) merece su propio equipo de acceso restringido, no un canal dentro del interno general. Un canal se puede configurar mal; un equipo aparte con dos miembros es una frontera que no depende de acertar una casilla.
 
### C. El sitio raíz de la organización: por qué no se trabaja ahí
 
Existe un sitio raíz de SharePoint de la organización, el que aparece al entrar en la página principal de SharePoint. No es un cajón neutro: en la configuración habitual, **ese sitio lo ve toda la empresa.** Una carpeta creada ahí queda a la vista de todo T_NEUTRAL, y además nadie es su dueño, con lo que acaba siendo tierra de nadie donde las cosas se acumulan sin orden.
 
La regla es sencilla: no se trabaja en la raíz. Todo documento vive en el sitio de un equipo, que es donde los permisos están definidos y hay un responsable. Si en algún momento hace falta un espacio para toda la empresa (una plantilla de uso común, el propio manual interno), eso merece un equipo con nombre y propósito, no una carpeta suelta en la raíz. La regla de higiene «un lugar evidente para cada cosa» y la carpeta huérfana en la raíz se excluyen mutuamente: una carpeta sin equipo dueño es, por definición, un lugar no evidente.
 
---
 
## 7. Dónde viven las reuniones
 
Una reunión de Teams produce cosas que conviene conservar: la grabación, la transcripción y las notas. Dónde acaban guardadas depende de un detalle que casi nadie tiene presente, y que es la causa de que tantas transcripciones se pierdan: **una reunión guarda lo que produce en el sitio del canal solo si nace en el canal.**
 
Una reunión convocada desde el calendario de Outlook o desde el calendario general de Teams, sin asociarla a ningún canal, no pertenece a ningún equipo. Su grabación se guarda en el OneDrive personal de quien la organizó, y la transcripción con ella. Queda en el cajón privado de una persona, con todo lo que eso implica: el equipo no la tiene a mano, depende de esa persona, y si esa persona se va el acceso se complica.
 
Una reunión convocada desde un canal pertenece a ese canal. Su grabación, su transcripción y sus notas se guardan en el sitio de SharePoint del equipo, en la carpeta del canal, a la vista de sus miembros sin que nadie mueva nada. Esa es la diferencia entre una reunión cuyo rastro se conserva donde el equipo lo encontrará y una cuyo rastro queda atrapado en un OneDrive ajeno.
 
El reflejo que conviene instalar: antes de convocar una reunión de proyecto, preguntarse dónde deben vivir sus notas, y convocarla desde ese canal. El detalle operativo (cómo se convoca desde el canal, cómo se activa la transcripción) está en la *Guía de trabajo diario con documentos de Office*.
 
---
 
## 8. Cómo se sincroniza lo de la nube con tu ordenador
 
Trabajar con los documentos del equipo desde el Explorador de Windows, en vez de desde el navegador, es más cómodo. Pero para entender por qué a veces aparecen carpetas que parecen duplicadas, o por qué algo no se reorganiza como uno espera, hay que tener claro el modelo de fondo. Es sencillo si se ve bien de una vez.
 
**La copia de verdad vive siempre en la nube, en SharePoint. Lo que tienes en tu ordenador es un reflejo de esa copia.** No son dos originales que se igualan entre sí; hay un único original en la nube y espejos locales en cada ordenador que lo haya traído. Cuando editas en tu ordenador, tu cambio sube a la nube; cuando alguien edita en la nube o desde otro ordenador, ese cambio baja a tu espejo. Todo pasa por la nube como punto central; los ordenadores no hablan entre sí directamente.
 
```mermaid
flowchart TD
    NUBE[(SharePoint · la nube<br/>la copia de verdad)]
    NUBE -->|baja los cambios| LOCAL1[Tu ordenador<br/>un reflejo]
    NUBE -->|baja los cambios| LOCAL2[Ordenador de otra persona<br/>otro reflejo]
    LOCAL1 -->|sube tus cambios| NUBE
    LOCAL2 -->|sube sus cambios| NUBE
 
    style NUBE fill:#2D5016,color:#fff
    style LOCAL1 fill:#F4F7F0,color:#1A1A1A
    style LOCAL2 fill:#F4F7F0,color:#1A1A1A
```
 
De este modelo salen dos cosas que conviene saber.
 
**La sincronización no es instantánea, pero sí automática.** No tienes que subir ni bajar nada a mano: al guardar, tu cambio sube solo; cuando otro cambia algo, baja solo. Pero tarda unos segundos, y en ese intervalo tu reflejo y la nube están momentáneamente desalineados. Por eso importa esperar a que termine de sincronizar antes de apagar, y por eso, si dos personas editan a la vez sin estar en el mismo documento abierto, puede haber un choque. El detalle de cómo se resuelve ese choque (la coautoría y las copias en conflicto) está en la guía diaria.
 
**Las carpetas que traes no se pueden reorganizar como carpetas normales.** Cada biblioteca que traes a tu ordenador es un punto de anclaje de ese reflejo, no una carpeta corriente. El sistema espera encontrarla donde la puso. Si la metes dentro de otra carpeta que crees tú, rompes el anclaje y la sincronización deja de funcionar. La libertad de organizar en carpetas vive *dentro* de cada biblioteca; por encima de las bibliotecas, la estructura la fija cómo están montados los equipos, y eso no se reordena desde el Explorador. El Explorador refleja esa arquitectura, no la define.
 
Una consecuencia de esto que sorprende y no es un error: a veces, al traer un equipo al Explorador, aparecen **dos entradas que parecen el mismo contenido** (por ejemplo, una «Equipo - Documentos» y otra «Equipo - General»). No son copias. Una es la biblioteca entera del sitio, y la otra es un atajo directo a una de sus carpetas internas (la del canal General, que está *dentro* de la primera). Es el mismo contenido visto por dos puertas, igual que Teams y SharePoint son dos puertas al mismo sitio. La guía diaria explica cómo quedarse con una sola y evitar la confusión.
 
---
 
## 9. Cómo interactúan las tres
 
El recorrido natural de un documento a lo largo de su vida ilustra cómo encajan las tres herramientas:
 
```mermaid
flowchart LR
    A[Empiezo un borrador<br/>en MI OneDrive] --> B{¿Ya es útil<br/>para el equipo?}
    B -->|Todavía no| A
    B -->|Sí| C[Lo subo al canal de Teams<br/>del proyecto]
    C --> D[Queda guardado en el<br/>SharePoint del equipo]
    D --> E[El equipo lo edita,<br/>comenta y versiona ahí]
    E --> F[Versión final:<br/>sigue en el mismo sitio,<br/>sin duplicar]
 
    style A fill:#F4A460,color:#1A1A1A
    style C fill:#FDF3E7,color:#1A1A1A
    style D fill:#6B8E4E,color:#fff
    style E fill:#F4F7F0,color:#1A1A1A
    style F fill:#2D5016,color:#fff
```
 
El documento nace privado en OneDrive, se hace público al subirlo al canal (con lo que pasa a SharePoint), y vive el resto de su vida ahí, editado en común y versionado solo. No cambia de sitio ni se copia: cambia de estado, de privado a compartido, una sola vez.
 
---
 
## 10. Buenas prácticas de higiene documental
 
Estas son las reglas que, sostenidas por todo el equipo, mantienen el orden. Ninguna es difícil; el valor está en que las cumpla todo el mundo.
 
**Una sola copia de cada cosa.** El mismo documento no vive en dos sitios. Si está en el canal del proyecto, no está además en tu OneDrive ni en una carpeta suelta. Duplicar es garantizar que dos versiones diverjan.
 
**El nombre del archivo no lleva versión ni fecha.** Nada de `_v3`, `_final`, `_FINAL2`, `_2026-07`. El historial de versiones de SharePoint hace ese trabajo. El nombre describe qué es el documento, no en qué estado está: `memoria-tecnica-cirtexcam.docx`, no `memoria_v4_final_rev_MG.docx`.
 
**Compartir por enlace, nunca por adjunto.** Enviar un documento como adjunto crea una copia que ya nace desactualizada. En su lugar, comparte el enlace al archivo en SharePoint o Teams: todos ven la misma versión viva, y los cambios se reflejan solos.
 
**Lo compartido va a un espacio compartido, no a tu OneDrive.** En cuanto algo deja de ser borrador tuyo, sube al canal del proyecto. Tu OneDrive es la sala de espera, no el archivo.
 
**Un lugar evidente para cada cosa.** Cada proyecto tiene su equipo o su canal, y cada tipo de documento su carpeta. Si al guardar algo dudas dónde va, esa duda es una señal de que la estructura de carpetas necesita aclararse; plantéalo, no improvises una ubicación nueva.
 
**Los borradores muertos se archivan o se borran.** Una carpeta `_archivo` para lo superado mantiene la vista limpia sin perder nada. Un espacio lleno de versiones muertas hace que nadie encuentre la viva.
 
---
 
## 11. Cómo se organizan las carpetas de un sitio
 
Las reglas anteriores evitan que se dupliquen y se versionen mal los documentos. Falta la capa de encima: cómo se ordenan las carpetas para que cualquiera encuentre las cosas sin preguntar. El riesgo aquí es doble y opuesto. Si no hay estructura, cada uno inventa la suya y el mismo tipo de documento acaba en tres sitios distintos según quién lo guardó. Si la estructura es un árbol profundo de cinco niveles, nadie la recuerda, la ruta se hace larguísima y a las pocas semanas la gente deja las cosas «temporalmente» donde caen.
 
El equilibrio que funciona se resume en una idea: fijar poco y fijarlo bien. Hay un primer nivel de carpetas corto e igual en todos los sitios, que es lo que da homogeneidad; y por debajo, cada equipo organiza como le pide su trabajo. Quien entra en un sitio ajeno se orienta enseguida porque el primer nivel es siempre el mismo, y a la vez nadie trabaja dentro de una estructura rígida que no encaja con lo suyo. Una guía práctica para no caer en la profundidad excesiva: que nada de uso habitual esté a más de tres clics desde la raíz del sitio. Más allá de eso, además de incómodo, se acerca al límite de longitud de ruta de SharePoint, que con carpetas anidadas y nombres largos da errores de sincronización.
 
### A. Reglas de nomenclatura
 
Cuatro reglas cubren casi todo, y son las mismas que rigen los nombres de fichero, aplicadas a carpetas.
 
El nombre describe qué contiene la carpeta, no quién la hizo ni cuándo. Sin iniciales ni fechas: una carpeta es `Entregables`, no `Entregables_MG_2026`. El sistema ya guarda autor y fecha. Tampoco se ponen versiones ni estados en el nombre de la carpeta; el estado de un documento lo cuenta su ubicación (una carpeta `_archivo` para lo cerrado) y su historial, no el nombre.
 
En el primer nivel se usa un prefijo numérico (`01_`, `02_`…) para forzar un orden de lectura con sentido, que de otro modo sería alfabético y arbitrario. Por debajo del primer nivel no hace falta numerar. El guion bajo inicial (`_archivo`, `_recursos`) se reserva para lo que conviene mantener separado del trabajo vivo, arriba o abajo del todo.
 
En T_NEUTRAL, los nombres de carpeta de primer nivel van **sin acentos ni ñ** (`Documentacion`, no `Documentación`). La razón es que esos nombres aparecen en las URL de los enlaces compartidos y en la sincronización con externos, donde los caracteres especiales pueden dar problemas. Por debajo del primer nivel se puede ser más flexible.
 
### B. El esqueleto de primer nivel de un sitio de proyecto
 
Un sitio de proyecto usa la misma base de cinco carpetas. No conviene pasar de cinco o seis en el primer nivel; a partir de ahí se pierde el valor de tener un estándar reconocible.
 
```
01_Entregables      Lo que sale del proyecto en su forma final: informes,
                    memorias, entregas al cliente o al consorcio.
02_Trabajo          El trabajo en curso: borradores compartidos y material
                    que el equipo edita, mientras se elabora.
03_Documentacion    Referencia que entra y se consulta, no se produce:
                    documentos recibidos, normativa, fuentes, apoyo.
04_Reuniones        Actas, grabaciones y notas. Si las reuniones se convocan
                    desde los canales, esta carpeta se llena sola.
_archivo            Lo superado que no se borra: versiones muertas de una
                    fase cerrada, material que ya no está vivo.
```
 
Lo que separa estas carpetas es el ciclo de vida del contenido, y ahí está la lógica que permite decidir sin dudar dónde va cada cosa. En `02_Trabajo` está lo que se cuece; en `01_Entregables`, lo que ya está listo para salir; en `03_Documentacion`, lo que entra de fuera y solo se consulta; en `_archivo`, lo que cumplió su función y se retira de la vista. Un documento típico nace en Trabajo y, al cerrarse, su versión final se publica en Entregables. La distinción entre lo que se está haciendo y lo que ya se entregó es la que más ayuda en el día a día.
 
Fijar estas cinco tiene una contrapartida menor: algún sitio tendrá una carpeta poco usada (un proyecto sin entregables formales apenas tocará `01_Entregables`). Es un precio pequeño frente al desorden de que cada sitio se organice distinto. Una carpeta poco usada no molesta; una estructura imprevisible, sí.
 
### C. Adaptación a los tipos de sitio
 
El esqueleto de proyecto encaja en un sitio de proyecto, pero el sitio interno y el de material sensible piden su propia variante, con el mismo criterio de pocas carpetas y nombres claros.
 
El **sitio interno** no es un proyecto, sino el espacio de todo lo de la empresa, así que se ordena por áreas: `01_Operaciones`, `02_Comercial`, `03_Proyectos` (con una carpeta por proyecto interno dentro), `04_Recursos` (plantillas, logos, material reutilizable), `05_Equipo` (procesos, documentación interna, onboarding) y `_archivo`.
 
El **sitio de material sensible** (financiero, contratos, societario) prioriza encontrar rápido y no mezclar: `01_Financiero`, `02_Contratos`, `03_Societario`, `04_Fiscal_laboral` y `_archivo`. Pocas carpetas, muy delimitadas.
 
El **sitio de cliente** tiene una particularidad que viene de cómo funcionan los canales. Como cada línea de trabajo es un canal y cada canal tiene su propia carpeta en SharePoint, el esqueleto de proyecto se replica dentro de la carpeta de cada canal, no en la raíz del sitio: el canal de una línea tendrá dentro sus `01_Entregables`, `02_Trabajo`, etc. El canal interno privado tiene su propia estructura, que el cliente no ve. En un sitio organizado por canales conviene no crear además carpetas en la raíz del sitio, porque competirían con las carpetas de canal y crearían dudas sobre dónde va cada cosa. La estructura vive dentro de los canales.
 
### D. Lo que sostiene la estructura en el tiempo
 
Un esqueleto sin explicación se erosiona: alguien duda entre `02_Trabajo` y `01_Entregables`, elige por intuición, y en unos meses la lógica se ha diluido. La defensa barata es un archivo breve de bienvenida en la raíz de cada sitio, de diez líneas, que diga qué va en cada carpeta de primer nivel y recuerde las reglas de higiene. No es burocracia, es lo que permite que la estructura sobreviva a la incorporación de gente nueva y al paso del tiempo. Conviene que ese archivo sea un `.txt` o un `.docx` corto, no un `.md`: SharePoint no renderiza el Markdown como sí lo hace GitHub, así que para un lector no técnico un texto plano o un Word se lee mejor.
 
---
 
## 12. Errores frecuentes y cómo evitarlos
 
**"Tengo el archivo en Teams y también en SharePoint, ¿cuál edito?"** Son el mismo archivo. Teams te lo muestra; SharePoint lo guarda. Edita cualquiera de los dos: es el mismo. El problema solo aparece si en algún momento subiste una copia por separado; en ese caso, quédate con una y borra la otra.
 
**"Compartí un archivo y ahora el otro no puede abrirlo."** Probablemente estaba en tu OneDrive y lo moviste o renombraste, o compartiste desde un chat privado. Muévelo al canal del proyecto y comparte el enlace desde ahí.
 
**"No encuentro la última versión."** Suele ser síntoma de duplicación: hay varias copias y cada una avanzó por su lado. La solución de fondo es la regla de copia única; la inmediata, consolidar en una y borrar el resto.
 
**"Subí el documento al canal equivocado."** Como el archivo vive en SharePoint, puedes moverlo entre carpetas del mismo sitio sin perder su historial. Muévelo a la carpeta del canal correcto.
 
**"Adjunté el documento en un correo y ahora hay tres versiones circulando."** El adjunto es el origen del problema. A partir de ahora, enlace en lugar de adjunto: una sola versión viva para todos.
 
**"Grabé una reunión importante y ahora no la encuentra el equipo."** Probablemente la convocaste desde Outlook o desde el calendario general, sin asociarla a un canal. En ese caso la grabación fue a tu OneDrive personal, no al sitio del equipo. Para la próxima, convoca la reunión desde el canal del proyecto y quedará donde el equipo la encuentre; la actual puedes moverla al sitio del equipo y compartir el enlace.
 
**"Arrastré un documento a un chat de Teams y ahora hay una copia rara en mi OneDrive."** Es el comportamiento normal de un chat privado: al soltar un archivo ahí, Teams sube una copia a tu OneDrive y comparte esa copia, no el original. Si el documento ya vivía en un sitio de equipo, tienes ahora dos. Quédate con el del sitio del equipo, borra la copia del chat, y la próxima vez comparte el enlace al original en lugar de arrastrar el fichero.
 
**"Dejé una carpeta en la raíz de SharePoint y la ve todo el mundo."** El sitio raíz de la organización suele ser visible para toda la empresa. Nada de trabajo vive ahí: mueve esa carpeta al sitio del equipo que corresponda, donde los permisos están definidos.
 
---
 
## 13. Punto de partida tras la lectura
 
Con este documento leído, cualquier persona del equipo sabe:
 
- Que SharePoint, OneDrive y Teams son tres puertas al mismo almacenamiento.
- Que OneDrive es personal y provisional; SharePoint es compartido y permanente.
- Que subir un archivo a un canal de Teams es, en realidad, guardarlo en SharePoint.
- Que cada canal es una carpeta del sitio, y que Teams te muestra el interior de esa carpeta, no la raíz.
- Que cada equipo de Teams tiene su propio sitio con sus permisos, y que la frontera entre interno y externo se traza separando equipos, no confiando en un canal.
- Que una reunión conserva su rastro en el equipo solo si se convoca desde el canal.
- Que lo que hay en el ordenador es un reflejo de la copia de la nube, que sube y baja solo pasando por SharePoint.
- Que cada sitio se organiza con un primer nivel de carpetas corto e igual para todos, y libertad por debajo.
- Que no se duplica, no se ponen versiones en el nombre y se comparte por enlace.
- Dónde debe vivir cada documento según sea borrador propio o trabajo del equipo.
Para el trabajo que vive en repositorios de Git (código, configuración, criterios de un modelo), el sistema es otro y se explica en el Anexo B. La forma de saber cuál te corresponde: si produces texto plano que evoluciona y varias personas revisan, es Git; si produces documentos de Office que se abren en Word, PowerPoint o Excel, es Microsoft 365.
