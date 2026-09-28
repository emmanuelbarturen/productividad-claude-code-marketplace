# Productividad para Claude Code

Marketplace de plugins de productividad para [Claude Code](https://code.claude.com), en español.

| Plugin | Qué hace |
|---|---|
| [`proyectos`](plugins/proyectos/) | El ciclo de trabajo de una empresa en Markdown: explorar → proponer → aplicar → archivar, con reglas, plantillas y validador |

## Instalar

**Desde la app de escritorio de Claude**, pestaña *Code*: botón **+** junto al cuadro de texto → **Plugins** →
**Add plugin** → agrega el marketplace `emmanuelbarturen/productividad-claude-code-marketplace` → instala `proyectos`.

**Desde la terminal:**

```
claude plugin marketplace add emmanuelbarturen/productividad-claude-code-marketplace
claude plugin install proyectos@productividad-claude-code-marketplace
```

Si usas la plantilla de empresa Company Cycle OS, no hace falta nada de esto: su `.claude/settings.json` ya declara el
marketplace y el plugin, y la app los ofrece al aceptar la confianza de la carpeta.

## Actualizar

`/plugin` → *Marketplaces* → `productividad-claude-code-marketplace` → *Update*. Para recibir cambios solos, activa
*Enable auto-update* en ese mismo menú.

## Licencia

MIT.
