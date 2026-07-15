# Anexo B · Git y GitHub: control de versiones

**Anexo del documento troncal *Entornos de trabajo*.**
Aplicable a quienes trabajen en proyectos que vivan en un repositorio (código, configuración, criterios de un modelo, documentación técnica en texto). Para el trabajo ofimático de todos los días, ver el Anexo A (Microsoft 365). Para el día a día de desarrollo, ver la *Guía de trabajo diario Claude/Git*.

---

## 1. Propósito de este documento

Este documento explica qué es Git, qué es GitHub, qué problemas resuelven y cómo encajan con el resto de herramientas de T_NEUTRAL. Está dirigido a quienes trabajen en un proyecto que viva en un repositorio; no todo el trabajo de la empresa lo hace. No cubre el flujo de trabajo diario (ver la *Guía de trabajo diario Claude/Git*) ni la configuración de Claude (Anexo C). Su lectura es el primer paso antes de tocar cualquier repositorio.

Antes de entrar en Git conviene tener claro dónde encaja, porque comparte terreno con Microsoft 365 y confundirlos es la primera fuente de desorden.

---

## 2. Dónde encaja Git frente a Microsoft 365

El trabajo de T_NEUTRAL produce dos tipos de resultado, con necesidades distintas:

**Contenido y decisiones que evolucionan con el tiempo** (código, configuración, criterios de un modelo, documentación técnica en texto): necesita historial, la posibilidad de que dos personas trabajen en paralelo sin pisarse, y un punto de revisión antes de que un cambio se dé por válido. Ese es el terreno de **Git**.

**El trabajo ofimático de todos los días** (una memoria, un deck, una hoja de cálculo, una plantilla): se abre en Word, PowerPoint o Excel y vive en **Microsoft 365**, que tiene su propio anexo (Anexo A) y su propio sistema de orden.

La frontera decide dónde va cada cosa. Ante cualquier cosa que produzcas, la pregunta es una sola: ¿es texto que evoluciona línea a línea, o un fichero de Office cerrado?

```mermaid
flowchart TD
    A[Algo que produzco] --> B{¿Es texto plano<br/>que evoluciona línea a línea<br/>y otros pueden revisar?}
    B -->|Sí| C[Git + GitHub<br/>este documento]
    B -->|No| D{¿Se abre en Word,<br/>PowerPoint o Excel?}
    D -->|Sí| E[Microsoft 365<br/>ver Anexo A]
    D -->|No| F[Herramienta<br/>correspondiente]

    C --> C1[Código · Configuración<br/>Criterios de un modelo<br/>Instrucciones de Claude<br/>Documentación técnica]
    E --> E1[Memorias · Presentaciones<br/>Hojas de cálculo · Plantillas<br/>Entregables del consorcio]

    style C fill:#2D5016,color:#fff
    style E fill:#F4A460,color:#1A1A1A
    style C1 fill:#F4F7F0,color:#1A1A1A
    style E1 fill:#FDF3E7,color:#1A1A1A
```

Por qué no se mezclan: Git está hecho para comparar texto línea a línea y no aporta nada útil sobre un fichero binario de Office, mientras que Microsoft 365 da colaboración y versionado cómodos sobre documentos de Office pero no ofrece el control fino de cambios que necesita el código. Cada herramienta donde le corresponde. No se añaden herramientas adicionales (wikis, Notion, tableros externos) mientras esta frontera baste.

---

## 3. Git y GitHub

### 3.1. Qué resuelven

El trabajo compartido sobre un mismo contenido tiene tres problemas recurrentes cuando se hace con ficheros sueltos, por email o en una carpeta compartida sin control de versiones:

1. **No se puede trabajar en paralelo con seguridad.** Dos personas editando el mismo documento a la vez acaban con copias divergentes y la incertidumbre de cuál es la buena.
2. **No hay forma controlada de integrar cambios.** Ver con exactitud qué ha cambiado, detectar cuándo dos cambios chocan y decidir cómo resolverlo requiere una herramienta, no buena voluntad.
3. **No hay un punto de aprobación.** Un cambio pasa a ser "el bueno" sin que nadie lo haya revisado formalmente.

**Git** es el sistema que resuelve estos tres problemas: registra el historial completo de cambios de un conjunto de ficheros y permite trabajar en paralelo con la garantía de poder fusionar el trabajo de forma controlada. **GitHub** es la plataforma que aloja ese historial en la nube y añade una interfaz para revisar, comentar y aprobar cambios desde el navegador.

Ambos nacieron para desarrollar software, pero su mecánica funciona sobre cualquier fichero de texto plano: markdown, CSV, YAML, código, configuración. La condición para aprovecharlos es que el contenido viva en texto, no en un binario de Word o Excel.

### 3.2. Cinco conceptos imprescindibles

| Concepto | Qué es |
|---|---|
| **Repositorio** | La carpeta de un proyecto alojada en GitHub, con todo su contenido y todo su historial. Es la fuente de verdad de ese proyecto. |
| **Commit** | Una fotografía del proyecto en un momento dado, con un mensaje que explica qué cambió y por qué. |
| **Rama** | Una línea de trabajo paralela. Permite editar sin afectar a la versión validada hasta que el cambio esté listo. |
| **Pull request** | La solicitud formal de incorporar una rama a la versión validada. Muestra el cambio exacto, permite comentarlo y exige aprobación antes de fusionarse. |
| **Local / remoto** | Tu ordenador tiene una copia del repositorio (local). GitHub tiene la copia de referencia (remota). Se sincronizan en dos direcciones: subir cambios (*push*) y bajar cambios (*pull*). |

### 3.3. Local y remoto, y por qué no se sincronizan solos

Es el punto que más confunde al empezar. Editar un fichero en tu ordenador y hacer un commit **no sube nada a GitHub**. El commit se guarda solo en tu copia local. La sincronización con GitHub ocurre únicamente en dos momentos, y ninguno es automático:

- **Push**: subes tus commits locales a GitHub.
- **Pull**: bajas a tu ordenador los cambios que otros han subido a GitHub.

Fuera de esos dos momentos, tu copia local y la copia de GitHub pueden estar desincronizadas sin que nada te avise.

```mermaid
flowchart LR
    subgraph LOCAL[Tu ordenador]
        L1[Editas ficheros]
        L2[Commit:<br/>guardas la foto<br/>en tu copia local]
        L1 --> L2
    end

    subgraph REMOTO[GitHub · la nube]
        R1[Copia de referencia<br/>del proyecto]
    end

    L2 -->|push: subes<br/>tus commits| R1
    R1 -->|pull: bajas<br/>lo que subieron otros| L1

    style LOCAL fill:#F4F7F0,color:#1A1A1A
    style REMOTO fill:#FDF3E7,color:#1A1A1A
    style R1 fill:#2D5016,color:#fff
```

Conviene fijarse en un detalle del diagrama: el commit se queda dentro de tu ordenador. Nada cruza hacia GitHub hasta que haces `push`, y nada llega desde GitHub hasta que haces `pull`. La costumbre que evita casi todos los problemas: **hacer pull al empezar a trabajar cada día, y push al terminar.** El detalle completo, con el flujo diario paso a paso, está en la *Guía de trabajo diario Claude/Git*.

### 3.4. GitHub Desktop

Aplicación de escritorio que permite clonar un repositorio (descargarlo a tu ordenador por primera vez), ver qué ficheros has cambiado, hacer commits y hacer push o pull, todo con botones en lugar de comandos de terminal. Es la vía recomendada para quien no tiene experiencia previa con la línea de comandos.

---

## 4. Qué contenido vive en un repositorio

Dentro del terreno de Git (el texto que evoluciona), esto es lo que T_NEUTRAL guarda en repositorios:

- Código de cualquier sistema.
- Configuración de cualquier sistema.
- Documentación técnica y conceptual en texto: criterios de un modelo, decisiones de arquitectura, especificaciones.
- Instrucciones y skills de Claude.
- Diagramas expresados como texto (por ejemplo, Mermaid), que GitHub renderiza automáticamente.

Lo que no es texto que evoluciona línea a línea (documentos de Office, logotipos, plantillas, memorias) vive en Microsoft 365, con las reglas de higiene documental del Anexo A. La razón técnica de la separación está en la sección 2: Git compara texto, no ficheros binarios.

---

## 5. Cómo se conecta Claude con los repositorios

De las tres superficies de Claude (Chat, Cowork y Code), solo **Code** trabaja directamente sobre un repositorio: edita sus ficheros, ejecuta comandos de Git y corre scripts. Es la única con acceso al repositorio clonado en tu ordenador. Chat y Cowork no tocan repositorios.

Por eso, cuando en la *Guía de trabajo diario Claude/Git* se pide a Claude que cree una rama o haga un commit, se está usando Code. El detalle de las tres superficies, de los tres niveles de instrucciones y de cómo se configura todo está en el Anexo C (Claude), que reúne todo lo relativo a ese entorno.

---

## 6. Glosario

| Término | Definición |
|---|---|
| Git | Sistema de control de versiones: registra el historial completo de cambios y permite trabajo en paralelo. |
| GitHub | Plataforma web que aloja repositorios Git y añade la interfaz de colaboración. |
| GitHub Desktop | Aplicación de escritorio para trabajar con Git sin usar la terminal. |
| Repositorio | El proyecto completo con su historial. Fuente de verdad de ese proyecto. |
| Commit | Fotografía del proyecto en un momento dado, con mensaje descriptivo. |
| Rama | Línea de trabajo paralela que no afecta a la versión validada hasta su fusión. |
| Pull request | Solicitud de incorporar una rama a la versión validada, con comparación exacta y aprobación. |
| Push | Subir commits del repositorio local al repositorio remoto (GitHub). |
| Pull | Bajar al repositorio local los cambios que hay en el repositorio remoto. |

---

## 7. Punto de partida tras la lectura

Con este documento leído, cualquier persona del equipo sabe:

- Qué diferencia hay entre Git/GitHub y OneDrive, y qué va en cada uno.
- Qué es un repositorio, un commit, una rama y un pull request.
- Por qué el trabajo local y el de GitHub no se sincronizan solos.
- Qué son Chat, Cowork y Code, y para qué sirve cada superficie de Claude Team.
- Que existen tres niveles de instrucciones, con organización por encima de proyecto y proyecto por encima de personal.

La *Guía de trabajo diario Claude/Git* explica cómo se usan estas herramientas en el día a día: cómo se reparten las tareas, qué pasos sigue un cambio desde que se empieza hasta que queda fusionado, y cómo funciona en la práctica la relación entre Git y Claude Code.
