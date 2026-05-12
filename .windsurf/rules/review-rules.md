---
trigger: model_decision
description: Configuración de repositorios y stack tecnológico para revisión automatizada de PRs. Contiene los repos configurados y el stack del proyecto. Los criterios detallados de evaluación están en el Skill code-review.
---

# Configuración de Revisión de PRs

## Stack Tecnológico

| Capa       | Tecnología                        | Convenciones               |
|------------|-----------------------------------|----------------------------|
| Backend    | Java 21+, Spring                  | Maven, paquetes por capa   |
| Frontend   | JSP, JSTL, jQuery 3.x, CSS3      | Carpetas por tipo          |
| VCS        | GitHub                            | PR por feature, main base  |

## Repositorios Configurados

<!-- Agrega aquí los repos que el agente debe revisar -->
| Repositorio          | Rama base | Activo | Notas                |
|----------------------|-----------|--------|----------------------|
| OWNER/REPO           | main      | ✅     | Ejemplo — reemplazar |

> **Instrucciones**:
> - Reemplaza la fila de ejemplo con tus repositorios reales (formato `OWNER/REPO`).
> - Si hay **un solo** repo activo, se usa automáticamente. Si hay **varios**, se pregunta al usuario.
> - Para desactivar un repo temporalmente, cambia ✅ por ❌.

## Criterios de Evaluación

Los checklists detallados, severidades y plantillas de reporte están en el **Skill `code-review`**:

```
.windsurf/skills/code-review/
├── SKILL.md                    ← Proceso de revisión
├── review-checklist.md         ← Checklists por categoría con severidades
├── severity-matrix.md          ← Matriz de decisión aprobado/rechazado
├── report-template.md          ← Formato del reporte
└── github-comment-templates.md ← Plantillas para publicar en GitHub
```

## Cómo Modificar

- **Agregar criterio de evaluación**: Edita `review-checklist.md` en el Skill.
- **Cambiar severidad**: Modifica el emoji (🔴/🟡/🔵) en `review-checklist.md`.
- **Cambiar formato de reporte**: Edita `report-template.md` en el Skill.
- **Agregar repo**: Añade una fila en la tabla de arriba.
- **Cambiar stack**: Modifica la tabla de Stack Tecnológico.
