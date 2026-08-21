# Finanzas Sommos — Codex Skill

Skill de repositorio para operar y mantener el workflow financiero de Sommos.

## Instalación en un repositorio GitHub

Copia la carpeta:

`.agents/skills/finanzas-sommos/`

a la raíz de tu repositorio y haz commit.

Ejemplo:

```bash
git add .agents/skills/finanzas-sommos
git commit -m "feat: add Finanzas Sommos Codex skill"
git push
```

## Uso

En Codex CLI o extensión IDE:

```text
$finanzas-sommos revisa las fórmulas de CxC y CxP
```

También puede activarse implícitamente cuando la solicitud coincide con la descripción de la skill.

## Contenido

- `SKILL.md`: instrucciones principales.
- `references/sheet-schema.md`: estructura funcional de pestañas y columnas.
- `references/automation-rules.md`: categorización, TC, CxC/CxP, Bancos y Dashboard.
- `references/importacion-extractos.md`: flujo para CSV/PDF bancarios.
- `references/qa-checklist.md`: control de calidad después de cambios.
- `agents/openai.yaml`: metadata visual opcional.
