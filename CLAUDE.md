# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Qué es este repo

Un **marketplace de plugins de Claude Code**, todo en español. No es una app: el producto son las skills (Markdown
con frontmatter), las plantillas y validadores en TypeScript. Hoy tiene dos plugins: `contenido` (redactores que escriben con tu voz, tus formatos de publicación por canal y una parrilla de contenidos en Notion, Airtable o ClickUp) y `proyectos`, que lleva el ciclo de
trabajo de un repo de empresa con la forma de **Company Cycle OS** (repo aparte): explorar → proponer → aplicar →
archivar.

- `.claude-plugin/marketplace.json` — catálogo **y** manifiesto: cada entrada apunta a `source: "./plugins/<plugin>"`
  y lleva `version`, autor y keywords (`strict: false`, no hay `plugin.json`).
- `plugins/<plugin>/skills/<nombre>/SKILL.md` — cada skill es un comando `/<plugin>:<nombre>`; `name:` igual a la carpeta.
- `plugins/<plugin>/VERSIONS.md` — historial propio de cada plugin.
- `validar-skills.ts` (raíz) — formato de todas las skills de todos los plugins.
- `plugins/contenido/.mcp.json` — los conectores que `contenido` trae consigo (Notion, Airtable, ClickUp). El repo no
  depende de plugins externos: lo que una skill necesita va dentro de su plugin.
- `plugins/proyectos/scripts/validar.ts` — validador de estructura del repo de la **empresa** (lo ejecutan las skills).

Al instalar un plugin solo se copia su carpeta: **nada se comparte entre plugins**, ni se puede referenciar algo de
la raíz desde una skill.

## Comandos

Todo con `bun` (nunca npm/npx). No hay `package.json` ni dependencias. Desde la raíz:

```bash
bun test                       # todos: tests/ del marketplace y plugins/*/tests/
bun test -t "V5"               # un solo caso, por nombre
bun validar-skills.ts          # formato de skills (exit 0/1)
claude plugin validate .       # manifiesto del marketplace
claude --plugin-dir plugins/proyectos   # cargar el plugin sin instalarlo
```

Validador de empresa a mano: `bun plugins/proyectos/scripts/validar.ts --raiz plugins/proyectos/tests/fixtures/empresa`
(añade `--publicar --json` para higiene V11 y salida JSON). Exit: 0 limpio · 1 estructura (V1–V10) · 2 solo higiene ·
3 uso.

## Arquitectura de `proyectos`

**Dos repos, dos roles.** El plugin trae la lógica. El repo de la empresa (Company Cycle OS) trae solo los datos:
`_context.md` en la raíz con la tabla de áreas, cada área con `_context.md` · `_rules.md` · `_enlaces.md` y sus
temas, y `Proyectos/`. Su `.claude/settings.json` declara este marketplace y el plugin. Por eso las skills referencian
`${CLAUDE_PLUGIN_ROOT}/templates/...` y `${CLAUDE_PLUGIN_ROOT}/scripts/validar.ts`, y operan sobre
`${CLAUDE_PROJECT_DIR}`. Mover `templates/` o `scripts/` dentro del plugin rompe esas rutas.

**Invocación de skills.** `setup`, `proponer`, `aplicar` y `archivar` llevan `disable-model-invocation: true`: solo
corren cuando el usuario los escribe. `explorar`, `validar` y `reglas` también los puede cargar Claude solo, y lo
decide por el `description:` del frontmatter — para cambiar cuándo se activa una skill, edita ahí. `reglas` contiene
las reglas del repo de la empresa.

**El validador de empresa es un contrato duplicado.** `scripts/validar.ts` (un archivo, solo `node:fs`/`node:path`)
implementa V1–V11; `skills/validar/SKILL.md` describe los mismos chequeos para hacerlos a mano cuando no hay `bun`.
Si cambias un chequeo, cambia los dos. Las reglas que valida (descriptores, tabla de áreas ↔ carpetas, cabecera
`<!-- Creado: … · Actualizado: … · Creador: … -->`, tope de 120 líneas, bloque `## Estado` con `Fase`, manifiesto
del ejemplo en `.ccos/ejemplo.txt`) también las enuncian `reglas`, `setup` y las plantillas: mantenlas en sintonía.

**Tests.** `plugins/proyectos/tests/validar.test.ts` copia `tests/fixtures/empresa/` a un temporal, la rompe a
propósito y corre el script con `Bun.spawnSync` comprobando el exit code. Un chequeo nuevo = un caso nuevo con su
rotura mínima. `tests/skills.test.ts` (raíz) exige que `validar-skills.ts` dé 0 errores.

## Dónde va cada skill nueva

Cada vez que Emmanuel quiera agregar o importar una skill, **antes de crear archivos** recomienda en qué carpeta
`plugins/<plugin>/` va, con una línea de por qué. Criterio: un plugin agrupa skills que se usan juntas para un mismo
resultado (quien instala uno recibe todas); nombre en español, kebab-case, sustantivo del dominio (`proyectos`,
`contenido`), nunca el nombre de la skill ni de su autor. Prefiere un plugin existente; propone uno nuevo solo si la
skill no comparte resultado con ninguno. Plugins actuales: `proyectos` (ciclo de trabajo de una empresa en Markdown) ·
`contenido` (redactores que escriben con tu propia voz, los formatos de publicación por canal y la parrilla de contenidos, en Notion, Airtable o ClickUp, que los pone a publicar).

**`formatos.md` es un contrato entre dos skills de `contenido`.** `construir-formatos` lo escribe y `construir-parrilla`
lo lee: `## <Canal>`, las líneas `Por defecto:` y `Texto:`, `### <tipo>` y sus seis campos, con «Opción en la parrilla»
y los nombres de bloque del borrador (`## Láminas`, `## Infográfico`, `## Guion de video`). Si cambias uno de esos
nombres, cámbialo en las dos skills.

Skill importada de terceros: copia sin cambios con su `LICENSE` dentro de la carpeta de la skill, y anota origen,
commit y licencia en el `README.md` del plugin.

## Agregar un plugin o publicar una versión

Plugin nuevo: carpeta `plugins/<plugin>/`, entrada en `marketplace.json`, fila en la tabla del `README.md` raíz
(detalle en `CONTRIBUTING.md`). Versión: sube `version` en su entrada de `marketplace.json` y anótala en su
`VERSIONS.md`; sin cambio de versión, quien ya lo instaló no recibe nada. El repo es público
(`emmanuelbarturen/productividad-claude-code-marketplace`): nada de rutas personales, correos ni secretos.
