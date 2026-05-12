---
name: code-review
description: Revisión automatizada de Pull Requests. Aplica criterios de calidad de código, validación funcional y requisitos técnicos para proyectos Java/Spring + JSP/jQuery. Invoca este skill cuando el usuario pida revisar un PR, analizar código o auditar calidad.
---

# Skill: Revisión de Código

## Cuándo se usa
- Revisión de Pull Requests (invocado por `/review-pr`)
- Auditoría de código local (invocado por `/review`)
- Cualquier solicitud de análisis de calidad de código

## Archivos de soporte en esta carpeta
| Archivo                    | Contenido                                      |
|----------------------------|-------------------------------------------------|
| `review-checklist.md`      | Checklists detallados por categoría con severidades |
| `report-template.md`       | Formato estandarizado del reporte de revisión   |
| `severity-matrix.md`       | Matriz de severidad y reglas de decisión        |
| `github-comment-templates.md` | Plantillas de comentarios para publicar en GitHub |

## Proceso de Revisión

### Paso 1 — Cargar contexto
1. Leer `review-checklist.md` para conocer los criterios de evaluación.
2. Leer `severity-matrix.md` para conocer las reglas de aprobación/rechazo.

### Paso 2 — Ejecutar análisis triple (en orden)
1. **Validación Funcional** — ¿El código cumple lo que dice el PR?
2. **Calidad de Código** — ¿Clean code, naming, documentación?
3. **Requisitos Técnicos** — ¿Cache busting, seguridad, estructura?

### Paso 3 — Determinar veredicto
Aplicar `severity-matrix.md` para calcular si el PR es aprobado, rechazado o con observaciones.

### Paso 4 — Generar reporte
Usar `report-template.md` para generar el reporte estandarizado.

### Paso 5 — (Opcional) Publicar en GitHub
Usar `github-comment-templates.md` para formatear el comentario a publicar.
