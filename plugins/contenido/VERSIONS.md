# Versiones

## 0.3.0 — 2026-10-01

- Nueva skill `construir-formatos`: define, por cada canal, los tipos de publicación que usas (texto solo,
  texto + imagen, texto + video, carrusel, infográfico, artículo) y una ficha por tipo. Deja `formatos.md`. La
  entrevista va con preguntas de opciones.
- `construir-parrilla` usa `formatos.md`: de ahí salen las opciones de `Canal + tipo`, la regla de texto de cada canal
  y la forma de cada borrador (un carrusel sale con su bloque `## Láminas`). Sin `formatos.md` sigue con su lista fija
  de opciones.
- La regla de texto (extensión máxima y hashtags) ya no la pregunta `construir-parrilla` ni se guarda en `parrilla.md`:
  la define `construir-formatos`. Una línea `Texto:` de antes se ofrece como primera opción al definir los formatos.

## 0.2.0 — 2026-09-30

- Nueva skill `construir-parrilla`: crea la parrilla de contenidos en Notion, Airtable o ClickUp y la opera con cuatro
  flujos (Configurar, Armar, Redactar y Repaso).
- El plugin trae sus conectores en `.mcp.json` (Notion, Airtable y ClickUp): no depende de ningún otro plugin.

## 0.1.0 — 2026-09-30

- Primera versión, con la skill `construir-redactores`: deja `sobre-mi.md`, `voz.md`, un redactor por grupo de temas
  en `.claude/agents/` y el aprendizaje de cada uno en `aprendizaje/`.
