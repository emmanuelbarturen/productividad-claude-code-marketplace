# contenido

Skills para que tu contenido en redes lo escriban redactores con tu propia voz.

| Comando | Qué hace |
|---|---|
| `/contenido:construir-redactores` | Lee tus recursos (LinkedIn, webs), te entrevista y aprende de tus textos → deja `sobre-mi.md`, `voz.md` (la base), un redactor por grupo de temas en `.claude/agents/` y lo que cada uno aprendió en `aprendizaje/` |

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
