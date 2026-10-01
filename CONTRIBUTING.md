# Contribuir

## Inicio rápido

```bash
git clone https://github.com/emmanuelbarturen/productividad-claude-code-marketplace
cd productividad-claude-code-marketplace
bun test
```

## Estructura

```
.claude-plugin/marketplace.json   catálogo: una entrada por plugin
plugins/<plugin>/
  skills/<skill>/SKILL.md         cada skill es /<plugin>:<skill>
  templates/  scripts/  tests/    lo que el plugin necesite
  README.md  VERSIONS.md
validar-skills.ts                 formato de todas las skills
tests/                            tests del marketplace
```

## Agregar un plugin

1. Crea `plugins/<plugin>/` (kebab-case) con `skills/`, `README.md` y `VERSIONS.md`.
2. Agrega su entrada a `.claude-plugin/marketplace.json`:

   ```json
   { "name": "<plugin>", "source": "./plugins/<plugin>", "description": "...", "version": "0.1.0",
     "category": "productivity", "keywords": [], "strict": false }
   ```

3. Suma una fila a la tabla *Plugins disponibles* del `README.md` raíz.

Un plugin agrupa skills que se usan juntas: quien lo instala recibe todas. Al instalarse solo se copia su carpeta,
así que **nada se comparte entre plugins**: si dos usan la misma plantilla, cada uno lleva su copia.

## Agregar una skill

1. Crea `plugins/<plugin>/skills/<nombre>/SKILL.md`. La carpeta va en kebab-case.
2. Abre con frontmatter:

   ```yaml
   ---
   name: <nombre>            # igual a la carpeta
   description: <qué hace y cuándo usarla>
   argument-hint: [argumentos]
   disable-model-invocation: true   # solo si debe correr únicamente cuando el usuario la invoca
   ---
   ```

3. Para archivos del plugin usa `${CLAUDE_PLUGIN_ROOT}/templates/...` o `${CLAUDE_PLUGIN_ROOT}/scripts/...`; para el
   repo del usuario, `${CLAUDE_PROJECT_DIR}`.
4. Si pasa de 500 líneas, mueve el detalle a `skills/<nombre>/references/`.
5. Corre `bun validar-skills.ts`.

## Mejorar una skill existente

Claude decide cuándo cargar una skill leyendo su `description:`. Si cambias cuándo debe activarse, edítalo ahí.

## Convenciones

- Todo en español.
- `bun` siempre; nada de npm ni dependencias.
- Nada de rutas personales, correos ni secretos en lo que se commitea: el repo es público.

## Probar en local

```bash
bun test                                         # todos los tests, del marketplace y de cada plugin
bun validar-skills.ts                            # solo el formato de skills
claude plugin validate .                         # manifiesto del marketplace
claude --plugin-dir plugins/<plugin>             # cargar un plugin sin instalarlo
```

## Publicar una versión

Sube `version` en la entrada del plugin en `.claude-plugin/marketplace.json` y anota el cambio en
`plugins/<plugin>/VERSIONS.md`. Sin cambio de versión, quien ya lo instaló no recibe nada.
