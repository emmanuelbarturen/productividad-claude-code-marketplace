---
name: construir-parrilla
description: >
  Construye y opera la parrilla de contenidos de un emprendedor que publica él mismo en redes sociales. La parrilla vive en Notion, en Airtable o en ClickUp, a elección de la persona, con una fila por pieza: tema, canal, estado, fecha programada, redactor, palabras y link publicado, y una ayuda en cada columna que explica para qué sirve. Arriba de la parrilla van una base de fuentes y una página de temas propios. Tiene cuatro flujos: Configurar (pregunta dónde va la parrilla, consigue el acceso y la crea con su estructura), Armar (propone los temas de las próximas semanas y los itera hasta que cada uno queda aprobado o descartado), Redactar (el redactor escribe el post aprobado con la fuente de cada dato) y Repaso (lista lo vencido y cierra lo publicado con su link). Actívala cuando el usuario diga "construye mi parrilla", "configura mi parrilla", "arma mi parrilla", "propón temas", "qué publico las próximas semanas", "redacta el post", "repaso de mi parrilla", "qué tengo vencido" o "ya publiqué el post".
---

# Construir parrilla

## Para quién es esta skill

Para un emprendedor que es la cara de su negocio y publica él mismo. Usa estos rasgos para interpretar sus respuestas; no los recites.

- **Lo que se le traba es publicar, no las ideas.** La parrilla existe para que cada semana solo le quede leer un borrador y publicarlo.
- **Su audiencia desconfía de las promesas grandes.** Cada cifra y cada hecho de un post tiene que poder rastrearse a algo que de verdad pasó.
- **Él decide, la skill propone.** Ningún tema y ningún texto avanzan sin su ok explícito.
- **Publica él, a mano, en su cuenta.** La skill deja borradores listos; nunca publica.

## Qué construye

```
La parrilla                  una fila por pieza, de tema propuesto a publicado.
                             Vive donde la persona elija: Notion, Airtable o ClickUp
Fuentes                      dónde mirar para encontrar temas: links y referencias. Va arriba de la parrilla
Temas propios                donde la persona anota sus temas en viñetas: título y descripción. Va arriba de la parrilla
parrilla.md                  dónde está la parrilla y las reglas propias de esta persona
posts/NN-<slug>.md           un borrador por pieza: el texto, la fuente de cada dato y el chequeo
```

**El objetivo final es la parrilla en el destino que eligió la persona,** con la misma estructura en los tres. `parrilla.md` y `posts/` existen para que la skill la encuentre en cada sesión y para que cada borrador tenga su archivo. En el resto de esta skill, «la base» es esa parrilla, esté en Notion, en Airtable o en ClickUp.

## La base

Nombre: **«Parrilla de contenidos — [nombre de pila de la persona]»**. Los nombres de los campos van **sin tilde y se copian exactos**: así se leen y se escriben igual desde cualquier herramienta.

| # | Campo | Tipo | Ayuda (se copia en el campo) | Regla | Ancho |
|---|---|---|---|---|---|
| 1 | `ID` | ID único, con las iniciales de la persona en mayúsculas como prefijo (`AB-1`) | El código de esta fila. Se pone solo | Sirve para nombrar la pieza en la conversación | 80 |
| 2 | `Tema` | título | El título del post | El titular de la pieza | 320 |
| 3 | `Estado` | selección | En qué paso va: de propuesto a publicado | Los siete valores de abajo | 170 |
| 4 | `Fecha programada` | fecha | El día en que toca publicarlo | Siempre en el día fijo | 140 |
| 5 | `Redactor` | selección | Quién lo escribe | Cada redactor cubre un grupo de temas | 150 |
| 6 | `Canal + tipo` | selección | En qué red se publica y en qué formato | Una opción por red y formato | 150 |
| 7 | `Descripcion` | texto | De qué trata, en una línea | El ángulo, 20 palabras como máximo, sin repetir el título | 320 |
| 8 | `Notas` | texto | De dónde salió el tema, cambios pedidos y dudas | Dudas con ❓, avisos con ⚠️, la cifra del tema con su fuente y el motivo de un descarte | 320 |
| 9 | `Palabras` | número | Cuántas palabras tiene el texto | El conteo real del texto que se publica, hashtags incluidos. No cuenta la imagen ni el primer comentario | 90 |
| 10 | `min. lectura` | fórmula | Minutos que toma leerlo. Se calcula solo | `if(empty(Palabras), "", ceil(Palabras / 200))` | 100 |
| 11 | `Archivo en el repo` | texto | Dónde está guardado el borrador | La ruta, escrita como código (entre comillas invertidas): sin ellas, Notion convierte el nombre `.md` en un enlace | 240 |
| 12 | `Fecha de publicacion` | fecha | El día en que de verdad se publicó | La fecha real, no la programada | 140 |
| 13 | `URL publicada` | URL | El link del post ya publicado | Solo el que pasa la persona | 200 |
| 14 | `Created time` | fecha de creación | Cuándo se creó esta fila. Se pone sola | Automático | 160 |

**El orden de la tabla es el orden por defecto de las columnas,** de izquierda a derecha: primero lo que identifica a la pieza, después en qué paso va y cuándo sale, quién la escribe y dónde, de qué trata, los datos del texto y al final los de la publicación. Vale para la tabla por defecto, `Por Publicar` y `Publicado`, con las dos primeras columnas (`ID` y `Tema`) fijas al desplazarse. En el tablero, cada tarjeta muestra `Tema`, `ID`, `Fecha programada`, `Redactor` y `Canal + tipo`. En el calendario, cada pieza muestra, además de su `Tema`, estos tres en este orden: `ID`, `Estado` y `Canal + tipo`. La persona puede reordenar después: lo que ella mueva se respeta y no se vuelve a ordenar.

**«Ancho» es el ancho sugerido de la columna, en píxeles.** Aplícalo solo si tu herramienta deja fijar el ancho de una columna. Si no lo permite, no lo simules ni lo des por hecho: dile a la persona, en una línea, que los anchos se ajustan arrastrando el borde de cada columna.

**Cada campo lleva su ayuda.** El texto de la columna «Ayuda» se copia exacto en la descripción del campo al crearlo, para que la persona entienda cada columna sin abrir esta skill. Es una frase corta, en palabras de todos los días, sin términos de la skill. Un campo que se agregue después se agrega con su ayuda.

**`Estado`** — siete valores, se copian exactos, con su emoji y sin número, **en este orden**. El orden es el del recorrido de una pieza y el de las columnas del tablero:

| Valor | Color | Significa |
|---|---|---|
| `Tema Propuesto ✍️` | gris | La skill lo propuso; falta que la persona decida |
| `Tema Aprobado ✔` | amarillo | La persona aprobó el tema; falta redactar |
| `Borrador Listo 👀` | azul | El texto está escrito; falta que la persona lo lea |
| `Listo a Publicar 👍` | morado | La persona aprobó el texto |
| `Programado 🕦` | por defecto | La persona lo dejó programado en la red |
| `Publicado ✅` | verde | Salió, y la persona pasó el link |
| `Descartado 🗑️` | rojo | No va. El motivo queda en `Notas` |

**`Canal + tipo`** — una opción por red y formato, con la forma `<red> - <formato>`, en minúsculas: `linkedin - texto`, `linkedin - carrusel`, `linkedin - foto`, `linkedin - video`. Si además publica en un blog: `blog - largo` y `blog - corto`. Para otra red, la misma forma (`instagram - carrusel`). Esta lista vale solo cuando no existe `formatos.md`.

**Con `formatos.md`, mandan los formatos de la persona.** Ese archivo lo deja `/contenido:construir-formatos`: por cada canal, su tipo por defecto (`Por defecto:`), su regla de texto (`Texto:`) y una ficha por tipo. Esta skill lo lee y lo usa; no lo escribe, no vuelve a preguntar lo que dice y no guarda una copia.

- **Las opciones de `Canal + tipo`** son la línea «Opción en la parrilla» de cada ficha, copiada exacta y sin sus comillas invertidas (`linkedin - texto + imagen`, `linkedin - infografico`).
- **Una fila cuya opción no tiene ficha** (un canal o un tipo que la persona no definió) se trata como sin formatos: se escribe el texto y se sugiere en una línea «agrega un canal» o «agrega un formato».
- **Si la base ya existe y le falta una opción de `formatos.md`,** agrégala al arrancar cualquier flujo y relee (en ClickUp, pídesela a la persona). Nunca borres ni renombres una opción que tenga filas.
- **Opciones de antes:** `<red> - foto` equivale a `<red> - texto + imagen` (en Instagram, a `instagram - imagen`) y `<red> - video` a `<red> - texto + video` (en Instagram no cambia). Mover las filas de la opción vieja a la nueva se pregunta una vez, con `AskUserQuestion`.
- **La regla de texto** (extensión máxima y hashtags) es la línea `Texto:` del canal de la pieza. Si chocan dos reglas, el orden es: `voz.md` y el redactor, después «Tus reglas» de la ficha, después `Texto:` del canal. La voz también manda sobre la ficha: si «El borrador entrega» pide algo que la voz prohíbe (un pedido al lector), no se escribe.
- **La forma del borrador** es «El borrador entrega» de la ficha del tipo.

**`Redactor`** — una opción por redactor de la persona, con su nombre sin el prefijo `redactor-` (`construir-con-ia` para `.claude/agents/redactor-construir-con-ia.md`), más `Otro`. Una pieza con `Otro` la escribe el redactor que la persona indique. Si la persona todavía no tiene redactores, la única opción es `Otro`: sugiere `/contenido:construir-redactores`, y cada redactor nuevo agrega su opción.

### Arriba de la parrilla: Fuentes y Temas propios

De ahí salen los temas. Los dos van **arriba de la parrilla**, en este orden: `Fuentes`, `Temas propios`, la parrilla.

**`Fuentes`** — una base con una fila por fuente: un lugar donde mirar para encontrar temas, noticias o novedades. Sus campos, en su orden por defecto y con su ayuda:

| # | Campo | Tipo | Ayuda (se copia en el campo) |
|---|---|---|---|
| 1 | `Fuente` | título | El nombre de la fuente |
| 2 | `Tipo` | selección: `noticias`, `boletin`, `blog`, `persona`, `norma o documento`, `comunidad`, `otro` | Qué clase de fuente es |
| 3 | `Link` | URL | Dónde se lee |
| 4 | `Para que sirve` | texto | Qué temas se pueden sacar de aquí |
| 5 | `Redactor` | selección, con las mismas opciones que en la parrilla | A qué redactor le sirve |
| 6 | `Ultima revision` | fecha | La última vez que se revisó |

Una fuente no necesita link: «las preguntas que me hacen mis clientes» es una fuente de tipo `persona`.

**`Temas propios`** — una página donde la persona anota sus temas, lo más simple posible: una lista de viñetas, una por tema, con el título en negrita y una descripción corta al lado.

```
Anota aquí tus temas, uno por viñeta: un título y de qué se trata. Cuando un tema entra a la parrilla, se marca con ✅ y baja a «Usados».

## Por usar
- **[Título del tema].** [De qué se trata, en una o dos líneas]

## Usados
- ✅ **[Título del tema].** [De qué se trata] · usado en [ID]
```

Cuando la skill propone un tema de «Por usar», en el mismo turno lo marca con ✅, le agrega `usado en [ID]` y lo mueve **al final de «Usados»**. Así arriba queda solo lo que falta usar. No cambia ni el título ni la descripción que escribió la persona, y no le pide más datos para anotar un tema: lo que falte se pregunta al redactar.

### En Notion

Una página «Parrilla de contenidos — [nombre de pila de la persona]» que contiene, en este orden: una línea que explica qué hay arriba y qué hay abajo · la base `Fuentes`, como subpágina · la página `Temas propios` · la base de la parrilla, **en línea**, para que se vea al abrir la página. La página lleva el nombre completo; la base de adentro se llama `Parrilla`. Lo que se agrega a una página queda al final: crea primero `Fuentes`, después `Temas propios` y la parrilla al último.


Una base de datos con los 14 campos, sus tipos y la ayuda de cada uno en la descripción de la propiedad. `Estado`, `Canal + tipo` y `Redactor` son de tipo **selección**, con sus opciones y colores (`Estado` es una selección normal, no el tipo de propiedad «estado» de Notion). Al crear la fórmula con el conector, la propiedad se escribe `prop("Palabras")`, y la ayuda de cada campo va en su `COMMENT`, también en el título, el `ID`, la fórmula y la fecha de creación. El orden de las columnas se fija en cada vista de tabla con `SHOW`, también en la tabla por defecto (el orden en que se piden los campos al crear la base no ordena las columnas), y las columnas fijas con `FREEZE COLUMNS 2`; el conector no fija anchos. Para renombrar un campo y cambiarle las opciones, haz dos pedidos: juntos en uno crean un campo duplicado.

**Vistas** — cinco: la tabla por defecto con todos los campos · `Board` agrupado por `Estado` · `Calendar` por `Fecha programada` · `Por Publicar` (todo lo que no está en `Publicado ✅` ni en `Descartado 🗑️`, ordenado por `Fecha programada`) · `Publicado` (solo `Publicado ✅`). En un tablero recién creado las columnas sin piezas pueden estar ocultas: aparecen cuando hay una pieza en ese estado.

### En Airtable

Una base con una tabla `Parrilla` y los 14 campos, cada uno con su ayuda en la descripción del campo. `Tema` es el campo principal. `Estado`, `Canal + tipo` y `Redactor` son de selección única, con sus opciones exactas y en su orden. `ID` es una fórmula sobre un campo de numeración automática (`"AB-" & {N}`), `min. lectura` es la fórmula `IF({Palabras}, CEILING({Palabras} / 200), BLANK())` y `Created time` es el campo de fecha de creación.

**Vistas** — las mismas cinco: la cuadrícula por defecto · `Board`, un Kanban apilado por `Estado` · `Calendar` por `Fecha programada` · `Por Publicar` · `Publicado`.

`Fuentes` y `Temas propios` son dos tablas más de la misma base. `Temas propios` tiene tres campos: `Tema`, `Descripcion` y `Usado en`, que guarda el `ID` de la pieza; su vista deja abajo los que ya tienen `Usado en`.

Airtable no tiene una página por pieza: la versión final de cada pieza vive en su archivo de `posts/`.

### En ClickUp

Una lista «Parrilla de contenidos — [nombre de pila de la persona]» dentro del espacio que indique la persona. Cada pieza es una tarea, y la estructura se reparte así:

- `Tema` es el nombre de la tarea, `Estado` es su estado, `Fecha programada` es su fecha límite, `ID` es el identificador que ClickUp le da a la tarea y `Created time` es su fecha de creación.
- Los otros 9 campos son campos personalizados de la lista, con el mismo nombre: `Canal + tipo` y `Redactor` como lista desplegable, `Fecha de publicacion` como fecha, `Palabras` como número, `URL publicada` como URL, `min. lectura` como fórmula y el resto como texto.
- **El conector de ClickUp crea la lista y las tareas, y escribe estados, fechas y campos. No crea estados, campos personalizados ni vistas:** eso lo hace la persona una vez, a mano, en Configurar. Los siete estados son obligatorios, porque son las columnas del tablero. Un campo personalizado que la persona no haya creado se escribe en la descripción de la tarea, una línea por campo (`Descripcion: …`).
- El tablero es la vista de tablero de la lista, agrupada por estado. La descripción de la tarea hace de página de la pieza.
- `Fuentes` y `Temas propios` son dos listas más, junto a la de la parrilla. Cada fuente y cada tema es una tarea: el título es el nombre de la tarea y lo demás va en su descripción. Un tema usado se marca como completado, con `usado en [ID]` en la descripción.
- En el plan gratuito de ClickUp el conector admite 50 llamadas cada 24 horas: crea y actualiza las tareas en bloque, no una por una.

## Entorno

- **La base se crea y se opera con el acceso real que tenga la sesión** al destino elegido: sus herramientas para crear, escribir filas, actualizar campos y releer. Sin acceso no se crea ni se opera nada: se consigue primero, en Configurar. No hay parrilla sin destino, y nunca inventes que la base existe.
- Si tu herramienta no puede crear algo de la estructura (el `ID` único, la fórmula, una vista, un estado o un campo), crea todo lo demás y dile a la persona, en una lista corta, qué agregar a mano y cómo, paso por paso.
- Los ejemplos de `AskUserQuestion` describen las preguntas: si la herramienta está disponible respeta sus límites (máximo 4 preguntas por llamada, de 2 a 4 opciones); si no, haz las mismas preguntas en el chat. Reutiliza lo que el usuario ya haya dicho.
- **Calcula las fechas y los días de la semana con una herramienta** (por ejemplo el comando `date`), nunca de memoria. «Hoy» es hoy en la hora local de la persona.
- Trabaja en el proyecto que eligió el usuario. Instalar la skill nunca crea nada.
- Redactar y guardar no autoriza a publicar, programar posts ni enviar mensajes.

## CRÍTICO: arranque automático al cargar

Cuando el usuario pida este flujo, mira en silencio si existe `parrilla.md` y sigue:

- **No existe:** la skill todavía no está configurada. Ve a Configurar, pida lo que pida el usuario: tu siguiente mensaje es la pregunta del destino, con sus tres opciones. Nada más.
- **Existe:** léelo y ve directo al flujo que pidió.

En los dos casos, lee también `formatos.md` si existe, en silencio. Si `parrilla.md` trae una línea `Texto:` de antes y ya existe `formatos.md`, manda `formatos.md`: pregunta una vez si borras la línea vieja. Si trae `Texto:` y no existe `formatos.md`, úsala tal cual y sugiere una vez `/contenido:construir-formatos` para definirla allá.

| Pedido | Flujo |
|---|---|
| «construye mi parrilla», «configura mi parrilla», o cualquier pedido sin `parrilla.md` | Configurar |
| «arma mi parrilla», «propón temas», «qué publico las próximas semanas» | Armar |
| «redacta el post», «escribe el post de la semana», «el tema X está aprobado» | Redactar |
| «repaso», «qué tengo vencido», «ya publiqué» | Repaso |

No resumas esta skill, no expliques cómo funciona y no preguntes si el usuario quiere correrla.

## Configurar — lo primero, una sola vez

Nada de lo demás funciona hasta que este flujo termina. Tiene cinco pasos y no se salta ninguno.

### 1. Pregunta dónde va la parrilla

Es la primera pregunta, sola, antes que cualquier otra:

```json
[
  {
    "question": "¿Dónde quieres llevar tu parrilla de contenidos?",
    "header": "Destino",
    "multiSelect": false,
    "options": [
      {"label": "Notion", "description": "Una base de datos con tablero por estado, calendario y una página por pieza"},
      {"label": "Airtable", "description": "Una base con los mismos campos, tablero Kanban por estado y calendario"},
      {"label": "ClickUp", "description": "Una lista de tareas con tablero por estado. Los estados y los campos los creas tú una vez, a mano"}
    ]
  }
]
```

Las opciones son estas tres. Si la persona pide otro destino, dile que por ahora la skill trabaja con Notion, Airtable y ClickUp, y que elija uno.

### 2. Consigue el acceso

El acceso es el conector MCP del destino elegido. El plugin `contenido` trae los tres conectores: al instalarlo ya están en la sesión y solo falta que la persona autorice su cuenta en el navegador. No sigas al paso 3 hasta **comprobar el acceso con una lectura real** (listar o buscar algo en su cuenta). Decir «ya está» no cuenta.

Si el conector no aparece en la sesión (por ejemplo, porque la skill se usa sin el plugin), se agrega a mano:

| Destino | Comando para agregar el conector |
|---|---|
| Notion | `claude mcp add --transport http notion https://mcp.notion.com/mcp` |
| Airtable | `claude mcp add --transport http airtable https://mcp.airtable.com/mcp` |
| ClickUp | `claude mcp add --transport http clickup https://mcp.clickup.com/mcp` |

1. Mira si la sesión tiene herramientas del destino elegido.
2. **El conector está instalado pero pide autenticación:** inicia la autenticación con la herramienta del conector y pásale el enlace, o dile que escriba `/mcp`, elija el conector y complete el acceso en el navegador.
3. **No aparece en la sesión:** pídele que lo agregue, con el paso exacto según donde trabaje:
   - En la terminal: el comando de la tabla. Después tiene que **reiniciar la sesión** (un conector recién agregado no aparece en la sesión en curso) y, ya dentro, escribir `/mcp` para autenticarse.
   - En la app: activar el conector del destino en la sección de conectores, si aparece ahí, y autorizarlo.

   Dile que al volver escriba «configura mi parrilla». Detente ahí.
4. Si el acceso que dio solo permite leer, dilo: con acceso de solo lectura la parrilla no se puede configurar.

### 3. Pregunta lo que define la parrilla

Si existen `sobre-mi.md` y redactores en `.claude/agents/redactor-*.md`, léelos primero: de ahí salen el nombre, los redactores, las redes y los límites, y no se vuelven a preguntar. Con redactores tampoco se pregunta el tipo de tema: cada redactor ya define sus temas y su propósito, y en `parrilla.md` se anota «lo define cada redactor». Si la persona responde que los temas los decide después, se anota igual. Con `formatos.md` tampoco se pregunta la red: sus canales son los de la parrilla. Si trae más de un canal, pregunta cuál es el principal: ese es el canal por defecto. Pregunta solo lo que falte. Las opciones de abajo son la referencia; ajústalas a lo que ya sabes de la persona.

```json
[
  {
    "question": "¿En qué red publicas con esta parrilla?",
    "header": "Red",
    "multiSelect": true,
    "options": [
      {"label": "LinkedIn", "description": "Texto, carrusel, foto o video"},
      {"label": "Instagram", "description": "Carrusel, foto o video"},
      {"label": "Facebook", "description": "Texto, foto o video"},
      {"label": "Blog propio", "description": "Artículos largos o cortos"}
    ]
  },
  {
    "question": "¿Qué día fijo de la semana publicas?",
    "header": "Día fijo",
    "multiSelect": false,
    "options": [
      {"label": "Martes", "description": "Deja el lunes para leer el borrador"},
      {"label": "Miércoles", "description": "Mitad de semana"},
      {"label": "Jueves", "description": "Deja tres días para leer el borrador"},
      {"label": "Lunes", "description": "El borrador se lee el fin de semana"}
    ]
  },
  {
    "question": "¿Qué tipo de tema va a tener tu parrilla? (uno solo: es lo que la hace reconocible)",
    "header": "Tipo de tema",
    "multiSelect": false,
    "options": [
      {"label": "Cómo logré un resultado", "description": "«Cómo logré [resultado con número] usando [método]», contado por quien lo hizo"},
      {"label": "Cómo resuelvo un problema", "description": "«Cómo resuelvo [problema de mi cliente]», con un caso propio"},
      {"label": "Lo que decidí y por qué", "description": "«Por qué elegí [decisión] y qué pasó después»"},
      {"label": "Lo que aprendí haciendo", "description": "«Lo que aprendí al [experiencia propia]», con lo que cambió"}
    ]
  }
]
```

Después, en un solo mensaje en el chat, pide lo que no cabe en opciones:

> Tres cosas más: 1) [en Notion: el link de la página dentro de la cual creo la base; si no me pasas ninguno, la creo en tu sección privada y después la mueves · en Airtable: en qué espacio de trabajo la creo, si tienes más de uno · en ClickUp: en qué espacio creo la lista]; 2) cuántos seguidores tienes hoy en esa red, para tener un «antes» (si no lo tienes a mano, queda pendiente); 3) si guardas ideas o documentas tu trabajo en algún archivo o carpeta de este proyecto, dime cuál.

**La regla de texto no se pregunta aquí:** la define `/contenido:construir-formatos`. Si no existe `formatos.md`, haz una sola pregunta con `AskUserQuestion`: «Definir mis formatos ahora» o «Seguir sin formatos». Si elige definirlos, sigue esa skill ahí mismo y vuelve a este paso con `formatos.md` escrito. Si sigue sin formatos, no hay tope de extensión ni de hashtags: solo manda la voz. Si `sobre-mi.md` no dice cómo se nombra a terceros (clientes, amigos, colegas), pregúntalo: por su nombre o por su rol.

### 4. Crea la base

1. Crea `Fuentes` y `Temas propios`, en ese orden, con la estructura de «Arriba de la parrilla». **Deja la plantilla completa:** lee `references/plantilla.md`, que está en la carpeta de esta skill, y síguela al pie de la letra: la página, sus textos, las vistas y los ejemplos (5 piezas, 2 fuentes y 3 temas). Los ejemplos se crean siempre, marcados `[PRUEBA]` o `[EJEMPLO]`: le muestran a la persona una parrilla en marcha. Después crea la base en el destino elegido, con **todos los campos de «La base»**, sus tipos, sus opciones exactas y su ayuda en la descripción de cada campo, y con las columnas en el orden por defecto. Las opciones de `Canal + tipo` salen de `formatos.md`, o de las redes elegidas si no existe; las de `Redactor`, de sus redactores más `Otro`.
2. **En Notion:** crea las cinco vistas. Si tu herramienta no puede crear una vista, dile a la persona cómo hacerla a mano: en la base, **+** junto a las pestañas de vistas → elegir el tipo (`Board`, `Calendar` o `Table`) → ponerle el nombre exacto → en `Board`, agrupar por `Estado`; en `Calendar`, mostrar por `Fecha programada`; en `Por Publicar` y `Publicado`, el filtro de `Estado` que indica «La base».
   **En Airtable:** crea la base con la tabla `Parrilla` y sus campos en la misma creación, en un espacio de trabajo donde la persona tenga permiso de creador. Las vistas que el conector no pueda crear se piden a mano, con los mismos nombres.
   **En ClickUp:** crea la lista y pídele a la persona, en un solo mensaje, lo que el conector no crea: los siete estados de la lista, con su nombre exacto y en su orden; los campos personalizados de «La base», con su nombre, su tipo y su ayuda para pegarla en la descripción; y la vista de tablero agrupada por estado. Espera a que diga que terminó.
3. Escribe el bloque **«Cómo funciona»**, con sus datos reales (en Notion, en la descripción de la base; en Airtable, en la descripción de la tabla; en ClickUp, en la descripción de la lista):

   > Parrilla de [red] de [nombre]. La skill propone y [nombre] decide.
   >
   > **Tipo de tema:** [el tipo elegido, o «lo define cada redactor»].
   >
   > **Armar** («arma mi parrilla»): se proponen temas en `Tema Propuesto ✍️`, uno por [día]. Apruebo, corrijo o descarto cada uno.
   >
   > **Redactar** («redacta el post»): se verifica cada cifra y se escribe con mi voz. El post queda en `Borrador Listo 👀`. Con mi ok pasa a `Listo a Publicar 👍`.
   >
   > **Repaso** («repaso de mi parrilla»): un solo mensaje con lo vencido. Un post solo pasa a `Publicado ✅` cuando yo paso el link.
   >
   > **Reglas:** un post por [día]; si falla, se corre una semana. [Sus límites, uno por línea.]

4. **Relee la base** con tu herramienta y comprueba que `Fuentes` y `Temas propios` existen y quedaron arriba de la parrilla, y que están los ejemplos de la plantilla. Después compara campo por campo contra «La base»: los 14 nombres exactos, cada uno con su ayuda, las columnas de las tablas en el orden por defecto, y `Estado` como selección (en ClickUp, los estados de la lista) con sus siete valores exactos. ClickUp puede devolver los estados en minúsculas: al compararlos, ignora mayúsculas y minúsculas. Si algo quedó distinto, corrígelo antes de seguir; si no puedes, dilo. En ClickUp, anota qué campos personalizados existen: los que falten se escriben en la descripción de cada tarea.

### 5. Escribe parrilla.md y entrega

`parrilla.md` se escribe **solo después** de releer la base: su existencia le dice a la skill que la configuración terminó.

```
# Parrilla

- **Destino:** [Notion | Airtable | ClickUp]
- **Base:** Parrilla de contenidos — [nombre] · [URL de la base o de la lista]
- **Identificador:** [el que devolvió la herramienta al crearla: la fuente de datos en Notion, la base y la tabla en Airtable, la lista en ClickUp]
- **Fuentes:** [URL de la base de fuentes]
- **Temas propios:** [URL de la página de temas propios]
- **Campos en la descripción:** [solo en ClickUp: los campos que no existen como campo personalizado]
- **Canal por defecto:** [con `formatos.md`, solo el canal principal (`linkedin`): su tipo se lee en cada sesión de la línea `Por defecto:` de ese canal · sin `formatos.md`, `[red] - texto`]
- **Día fijo:** [día], una pieza por semana
- **Tipo de tema:** «[el tipo elegido, con su fórmula]», o «lo define cada redactor»
- **Redactores:** [los redactores de la persona: son las opciones del campo `Redactor`]
- **Formatos:** [`formatos.md`: de ahí salen los tipos y la regla de texto · o «sin formatos: solo manda la voz»]
- **Borradores:** `posts/`
- **Punto de partida:** [seguidores] al AAAA-MM-DD, o «pendiente»
- **Ejemplos:** [presentes · borrados el AAAA-MM-DD · pendientes de borrar a mano]

## Reglas propias
- [Los límites de sobre-mi.md y los que la persona agregue: qué nunca se publica, cómo se nombra a terceros]

## Bancos de temas
- [Archivos o carpetas donde la persona guarda ideas o documenta su trabajo. Los temas ya usados se marcan ahí]
```

Después di, con sus datos reales: el link de la base, dónde anotar sus temas (`Temas propios`) y dónde agregar sus fuentes (`Fuentes`), lo que haya que agregar a mano si algo no se pudo crear, y una sola pregunta: «La parrilla tiene ejemplos para que veas cómo funciona. ¿Los borro o los dejas un tiempo para guiarte?». Si dice que sí, bórralos como indica la plantilla y anótalo en `parrilla.md`. Después da una sola acción siguiente: «Di "arma mi parrilla" y te propongo los temas de los próximos cuatro [día]».

## Armar — los temas de las próximas semanas

**Resultado:** cada tema del periodo queda en `Tema Aprobado ✔` o en `Descartado 🗑️`, con fecha. Aquí no se redacta ni una línea de ningún post.

**Periodo por defecto:** las próximas 4 fechas del día fijo que no tengan pieza asignada. La persona puede pedir otro rango.

### El tema

Todo tema sigue el **tipo de tema** de `parrilla.md` (si dice «lo define cada redactor», los temas y el propósito del redactor que lo escribe) y cumple tres condiciones:

- **Le pasó a la persona.** Algo que hizo, resolvió, decidió o midió. No un consejo genérico. Un tema que sale de una fuente lleva su punto de vista: qué piensa, qué hizo con eso o qué cambia para su lector. La noticia sola no es un tema.
- **Se puede sostener.** Si el tema trae una cifra, se anota en `Notas` con su fuente. Una fuente es una de tres cosas: un archivo, una medición, o el relato de la persona dicho en la conversación, que se anota «relato de [persona], AAAA-MM-DD». Va ❓ solo cuando la cifra del relato contradice a un archivo o cuando la persona misma duda: en ese caso se propone la cifra que sí existe. Nunca se infla. Un tema sin cifra también vale: su valor es la práctica.
- **No cruza las reglas propias.** Los terceros (clientes, amigos, colegas) se nombran como digan las reglas propias de `parrilla.md`. Si no dicen nada, por su rol y no por su nombre.

### 1. Junta temas, los baratos primero

1. **La base:** filas en `Tema Propuesto ✍️`, `Tema Aprobado ✔` o `Borrador Listo 👀` sin `Fecha programada` o con la fecha vencida. Ya están pensadas; van primero.
2. **`Temas propios`:** los temas de «Por usar». Son de la persona y van antes que cualquier otro. Al proponer uno, márcalo con ✅, agrégale `usado en [ID]` y muévelo al final de «Usados».
3. **`Fuentes`:** si tienes una herramienta para leer la web, abre las fuentes con link, empezando por las que llevan más tiempo sin revisar, busca novedades que den un tema y anota la fecha de hoy en `Ultima revision`. Las fuentes sin link se le preguntan a la persona. Sin herramienta para leer la web, dilo en una línea y sigue.
4. **Los bancos de temas** de `parrilla.md`, saltando los ya usados y lo ya publicado (vista `Publicado`).
5. **El trabajo reciente real** que haya en el proyecto: lo que la persona cerró, decidió o midió en las últimas semanas, y el «Insumo propio» de sus redactores.
6. **Si no alcanza, pregunta:** «Cuéntame, en una línea cada una, cosas que hiciste, resolviste o mediste en las últimas semanas: tantas como fechas falten por llenar».
7. **Redactor repetido:** si 3 de las últimas 4 piezas de la base (publicadas o programadas, sin contar las descartadas) son del mismo redactor, el tema siguiente viene de otro, si lo hay.

### 2. Arma el calendario

- Una pieza por fecha del día fijo. Una fila descartada no ocupa su fecha. Formato por defecto: el canal por defecto de `parrilla.md`. Con `formatos.md`, propón para cada tema, dentro del canal por defecto, el tipo cuya ficha lo describe en «Cuándo conviene»; si ninguna encaja, el tipo de la línea `Por defecto:` de ese canal (su `### <tipo>` da la opción).
- No dos temas seguidos del mismo redactor, mientras haya temas de otro. Si todos los temas disponibles son del mismo redactor, dilo en una línea y sigue.
- Lleva en `Notas` la marca ⚠️ **tema sensible** el tema que cumple alguna de estas tres: cuenta un error propio, deja reconocer a un tercero, o revela cifras internas del negocio (ingresos, costos, clientes). En esos, la persona aprueba el tema, no solo la redacción.

### 3. Propón en la base

Crea una fila por tema con `Estado` `Tema Propuesto ✍️`, `Tema`, `Descripcion`, `Fecha programada`, `Canal + tipo`, `Redactor`, y en `Notas` de dónde salió el tema, su cifra con la fuente si la trae y las dudas con ❓. `Palabras` queda vacío.

Luego, **un solo mensaje**: una tabla `ID · Tema · Fecha · Redactor · Descripcion`, el link de la base y una única pregunta: «¿aprobado, corregir o descartar, tema por tema?».

### 4. Itera

- **Aprobado** → `Tema Aprobado ✔`.
- **Corregir** → se queda en `Tema Propuesto ✍️`, el pedido va a `Notas`, se ajusta y se vuelve a mostrar **solo lo que cambió**.
- **Descartar** → `Descartado 🗑️` con el motivo en `Notas`. Si salió de un banco de temas, se marca ahí también para no volver a proponerlo. La fecha queda libre: en la misma vuelta propone un reemplazo para esa fecha. Si no hay otro tema, dilo y la fecha queda sin pieza.

**Listo cuando** no queda ninguna fila del periodo en `Tema Propuesto ✍️`. Cierra con el calendario final en una tabla, marcando las fechas que quedaron sin pieza.

## Redactar — el post aprobado

**Resultado:** el post en `Borrador Listo 👀` con su archivo en `posts/`, y en `Listo a Publicar 👍` cuando la persona lo aprueba.

**Cuándo:** a pedido, o para la pieza en `Tema Aprobado ✔` con la `Fecha programada` más cercana. Si la persona tiene poco tiempo entre semana, redacta en la misma sesión todas las aprobadas del periodo: así cada semana solo le queda leer y publicar.

### 1. Toma la pieza

Lee la fila (`Descripcion`, `Notas`). Si trae ⚠️ **tema sensible** sin un ok explícito de la persona sobre el tema, detente y pregúntalo.

**Comprueba que hay material para un post.** Una línea en la parrilla alcanza para aprobar un tema, no para escribirlo. Si ni la fila ni sus fuentes dicen qué hizo la persona, qué midió y qué le costó o qué decidió, pídelo antes de escribir, en un solo mensaje y con las preguntas que el redactor de la pieza necesita responder. No rellenes los huecos ni entregues un borrador a medias.

### 2. Verifica antes de escribir

Busca cada cifra, fecha u hecho en su fuente primaria: el archivo, la medición o el relato de la persona.

- Si la fuente contradice lo que dice la fila, **manda la fuente**, y la corrección se anota en `Notas`.
- Las horas se escriben en la hora local de la persona. Una fuente en otra zona horaria no se copia tal cual.
- Lo que no se puede verificar sale del post o queda con ❓ para que la persona lo resuelva.

### 3. Escribe el borrador

**El texto lo escribe el redactor que indica el campo `Redactor`.** Pásale el tema, el ángulo, los datos ya verificados con su fuente y, de `formatos.md`, la regla de texto del canal y **la ficha completa del tipo** de la pieza, no solo su nombre: sin la ficha escribe un post de texto. Si la pieza no es de texto y no existe `formatos.md`, sugiere `/contenido:construir-formatos` en una línea y escribe el texto. Si el redactor está cargado como subagente, úsalo. Si no aparece, lee su archivo en `.claude/agents/`, `sobre-mi.md`, `voz.md` y su archivo de `aprendizaje/`, y escribe siguiéndolos al pie de la letra. Si la persona no tiene redactores, dilo en una línea, sugiere `/contenido:construir-redactores` y, si quiere seguir, escribe en un registro llano y marca el borrador como voz provisional.

Guarda `posts/NN-<slug>.md`. `NN` son dos dígitos con el orden en que se creó el borrador (no es el `ID` de la fila) y `<slug>` son de 3 a 5 palabras del titular en kebab-case:

```
<!-- Creado: AAAA-MM-DD · Actualizado: AAAA-MM-DD (vN) -->
# Post — [titular]

**Publicar:** [día] AAAA-MM-DD · **Aprobado:** tema AAAA-MM-DD · **Aprobado para publicar:** pendiente · **Parrilla:** [link de la fila]
**Ángulo:** [el ángulo en una línea] · **Redactor:** redactor-[nombre] · **Canal + tipo:** [la opción de la fila]
**Link:**

## Para publicar

[El texto tal como se va a publicar, hashtags incluidos]

**Imagen:** [opcional: qué imagen y de dónde sale. Nunca frena la publicación. Obligatoria si la ficha del tipo la pide; se omite si el tipo trae su propio bloque]
**Primer comentario:** [opcional: el link que acompaña al post]

[El bloque que pide «El borrador entrega» de la ficha del tipo, con su nombre exacto: `## Láminas`, `## Infográfico` o `## Guion de video`. Un texto solo no lleva bloque]

## Fuente

- **[dato o afirmación del post]:** [archivo y sección · medición con su fecha · «relato de [persona], AAAA-MM-DD»]

## Chequeo antes de publicar

- [ ] Voz: revisado contra `voz.md` y el aprendizaje del redactor
- [ ] No cruza ninguna regla propia de `parrilla.md`
- [ ] Toda cifra está rastreada a la fuente de arriba
- [ ] Extensión y hashtags dentro de la regla de texto (o «sin regla de texto», si no hay ninguna)
- [ ] La pieza cumple la ficha de su tipo: trae su bloque y respeta «Tus reglas»
- [ ] ❓ [persona]: [la duda que solo ella puede resolver, si la hay]
```

Reglas de contenido (qué se dice; el cómo es del redactor):

- **Un solo resultado, a nivel total.** El antes y el después de una misma medida cuentan como uno. No el desglose. Sin montos si la persona pidió solo porcentajes.
- **Nada que la persona no pueda sostener.** Lo que no tiene fuente no se afirma.
- Si el post cuenta algo hecho con una herramienta automática o con IA, muestra qué decidió o revisó la persona. Ese dato sale de su relato: si no lo contó, pregúntalo. No lo inventes.
- La voz manda sobre la regla de texto: si `voz.md` o el redactor dicen «nunca hashtags», el post no lleva.
- Toda cifra de una lámina, de un infográfico o de un guion va al bloque `## Fuente`, igual que las del texto.
- En **Chequeo antes de publicar** marca `[x]` solo lo que comprobaste de verdad, y agrega los chequeos propios del tema.

### 4. Déjalo para revisión

En la base: `Estado` `Borrador Listo 👀`, `Palabras` (el conteo real del texto de **Para publicar**, sin las líneas `**Imagen:**` y `**Primer comentario:**` y sin el bloque del tipo) y `Archivo en el repo`. Muestra en la conversación el texto completo, con el nombre del redactor en una línea encima, y **solo** las dudas ❓.

### 5. Aprobación

- **Aprobado** → `Listo a Publicar 👍`, y `**Aprobado para publicar:** AAAA-MM-DD (vN)` en el archivo. Si pidió cambios de redacción, se aplican primero y se vuelve a mostrar.
- **En Notion, al aprobar, actualiza la página de la pieza en el mismo turno, sin que te lo pidan.** (En ClickUp la página es la descripción de la tarea. En Airtable no hay página: la versión final queda en el archivo de `posts/` y se actualizan los campos de la fila.) Cuerpo de la página: `## Versión final` (el texto listo para copiar) · la imagen, si la hay · el primer comentario, si lo hay · `## Fuente` · `## Historial` de versiones. Pon al día `Tema` y `Descripcion` si el texto cambió el título o las cifras, además de `Palabras` y `Notas`. Verifica releyendo la página.
- **Todo cambio de redacción que pida la persona se registra en el archivo de `aprendizaje/` del redactor,** como principio más ejemplo, para que el siguiente borrador ya salga corregido.
- **Corregir el enfoque** → vuelve a `Tema Aprobado ✔` con el pedido en `Notas`.
- **Descartar** → `Descartado 🗑️` con el motivo. El archivo se conserva.

Si el texto cambia después del ok, la pieza vuelve a `Borrador Listo 👀`.

## Repaso — vencidas y publicadas

### Ciclo A. Cerrar lo publicado

Empieza cuando la persona dice que publicó y pasa el link.

1. Si tienes una herramienta de navegador, verifica que el link abre el post. Si no se puede verificar, dilo.
2. En la fila: `Estado` `Publicado ✅`, `URL publicada` y `Fecha de publicacion` (la **real**, no la programada). Si el texto publicado difiere del borrador, corrige `Palabras`.
3. En el borrador: completa `**Link:**`.

Si la persona dice que lo dejó programado en la red, la fila pasa a `Programado 🕦` y se cierra cuando pase el link. **Nunca se marca publicado sin el link de la persona,** aunque el post se vea en vivo.

### Ciclo B. El repaso

Empieza a pedido de la persona, o con una rutina programada si ella la pide.

1. Busca las filas con `Fecha programada` anterior a hoy y `Estado` distinto de `Publicado ✅` y de `Descartado 🗑️`.
2. Responde con **un solo mensaje**:

   | ID | Tema | Programada | Días de atraso | Estado | Qué falta |
   |---|---|---|---|---|---|

   «Qué falta» sale de `Notas`; si no hay notas, va vacío. Debajo: el link de la base y una sola pregunta: cuáles salieron y cuáles se corren una semana.

3. **Pieza vencida que se corre:** nueva `Fecha programada` en la siguiente fecha libre del día fijo, y el motivo en `Notas`. Nunca dos piezas el mismo día: si choca, se corre la siguiente también. Actualiza la fecha en el archivo del borrador.

## Reglas

- Cuando esta skill se active, ve directo al trabajo. Sin resumen, sin explicación, sin preámbulo.
- **La skill propone; la persona decide.** Ninguna fila pasa a `Tema Aprobado ✔` ni a `Listo a Publicar 👍` sin su ok explícito en la conversación.
- **La skill nunca publica** ni marca `Publicado ✅` sin que la persona diga que salió y pase el link.
- **Una pieza por semana, en el día fijo.** Si falla, la pieza se corre una semana; nunca dos el mismo día.
- **Toda cifra del post tiene fuente** en el bloque `## Fuente`. Sin fuente, la cifra sale o se marca ❓.
- **Un solo mensaje por vuelta** en Armar y en Repaso, nunca uno por pieza.
- Los nombres de los campos y los valores de `Estado` se copian exactos: sin tilde los campos; con su emoji, sin número y en su orden los estados.
- Cada cambio se escribe en la base en el mismo turno en que ocurre, y se verifica releyendo.
- Cada post lo escribe el redactor que indica su campo `Redactor`, y todo borrador dice qué redactor lo escribió.
- Las reglas propias de `parrilla.md` y los límites de `sobre-mi.md` mandan sobre cualquier tema.
- Describe a la persona por sus rasgos. No la etiquetes por su país ni por su región.
- **Los formatos se usan, no se definen aquí.** Los tipos de `Canal + tipo`, la regla de texto y la forma de cada borrador salen de `formatos.md`. Esta skill no los pregunta ni los copia en `parrilla.md`.
- **Los ejemplos no cuentan.** Lo que empieza con `[PRUEBA]` o `[EJEMPLO]` no es una pieza, una fuente ni un tema: Armar no lo usa ni le reserva fecha, y Repaso no lo lista.
- **Primero se configura.** Sin `parrilla.md` no corre ningún otro flujo: se pregunta el destino (Notion, Airtable o ClickUp) y se consigue el acceso.
- La estructura es la misma en los tres destinos: los mismos 14 campos con su ayuda, los mismos siete estados.
- Si falta el acceso, dilo y pide el paso exacto. Nunca afirmes que creaste o actualizaste algo en la base sin haberlo releído.
