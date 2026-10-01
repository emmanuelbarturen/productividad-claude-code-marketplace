# contenido

Skills para que tu contenido en redes lo escriban redactores con tu propia voz, y para que salga cada semana.

| Comando | Qué hace |
|---|---|
| `/contenido:construir-redactores` | Lee tus recursos (LinkedIn, webs), te entrevista y aprende de tus textos → deja `sobre-mi.md`, `voz.md` (la base), un redactor por grupo de temas en `.claude/agents/` y lo que cada uno aprendió en `aprendizaje/` |
| `/contenido:construir-formatos` | Define tus formatos: por cada canal (LinkedIn, Instagram, Facebook, blog u otro), qué tipos de publicación usas (texto solo, texto + imagen, texto + video, carrusel, infográfico, artículo), cuál va por defecto y tu regla de texto → deja `formatos.md`, con una ficha por tipo: qué es, cuándo conviene, qué entrega el borrador y tus reglas. Solo define: no arma la pieza visual |
| `/contenido:construir-parrilla` | Crea tu parrilla de contenidos en Notion, Airtable o ClickUp (una fila por pieza, de tema propuesto a publicado) y la opera: propone los temas de las próximas semanas, redacta el post aprobado con la fuente de cada dato y repasa lo vencido → deja la parrilla, `parrilla.md` y un borrador por pieza en `posts/` |

Lo primero que hace `construir-parrilla` es configurarse: pregunta dónde va la parrilla y consigue el acceso. El plugin
trae los tres conectores (`.mcp.json`): al instalarlo solo te falta autorizar tu cuenta con `/mcp`. No depende de ningún
otro plugin.

| Destino | Conector, si lo agregas a mano | Qué queda |
|---|---|---|
| Notion | `claude mcp add --transport http notion https://mcp.notion.com/mcp` | Una base de datos con tablero, calendario y una página por pieza |
| Airtable | `claude mcp add --transport http airtable https://mcp.airtable.com/mcp` | Una base con los mismos campos, tablero Kanban y calendario |
| ClickUp | `claude mcp add --transport http clickup https://mcp.clickup.com/mcp` | Una lista de tareas con tablero por estado. Los estados y los campos personalizados los creas tú una vez, a mano: el conector no los crea |

La estructura es la misma en los tres: 14 campos, cada uno con una ayuda que explica para qué sirve, y siete estados. Arriba de la parrilla
van dos lugares de donde salen los temas: `Fuentes` (links y referencias que conviene revisar) y `Temas propios` (una
lista de viñetas donde anotas tus ideas: título y descripción; lo usado se marca y baja al final).

Con `formatos.md`, la parrilla usa tus formatos: las opciones de `Canal + tipo` son tus tipos, la regla de texto sale de
ahí y cada borrador llega con la forma de su tipo (un carrusel, con su guion lámina por lámina). Sin `formatos.md` la
parrilla funciona igual, con una lista fija de tipos.

La parrilla recién creada trae ejemplos marcados `[PRUEBA]` y `[EJEMPLO]` para que veas cómo se usa; al terminar, la skill
pregunta si los borra.

Pensada para un emprendedor que es la cara de su negocio y publica él mismo. Un redactor es un subagente que escribe
como tú sobre un grupo de temas. Cada redactor tiene su propia voz, porque cada grupo de temas pide un lector, un
propósito y un tono distintos. Para usarlo: «redactor-<nombre>, escribe un post sobre…».

## Origen

`construir-redactores` es una obra adaptada de `voice-builder`, de
[charlie947/social-media-skills](https://github.com/charlie947/social-media-skills) (commit `8cefb5b`), licencia MIT,
© 2026 Charlie Hills. Su `LICENSE` va dentro de la carpeta de la skill. Cambios respecto del original: traducida al
español; construye redactores (subagentes) en lugar de un solo perfil de voz; aprende la forma de escribir por reescritura (la persona reescribe un texto plano) y guarda el aprendizaje de cada redactor; lee los recursos de la persona antes de
preguntar; opciones de entrevista armadas con esos recursos; lector, propósito y material propio por redactor;
conserva el registro de quien escribe en lugar de normalizarlo.

Historial en [VERSIONS.md](VERSIONS.md).
