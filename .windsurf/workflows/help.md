---
description: Mostrar índice de comandos disponibles y guía rápida de uso
---

# Ayuda — Sistema de Revisión de PRs

Muestra al usuario el siguiente índice de comandos y guía rápida.

---

## Comandos Disponibles

| Comando            | Descripción                                             | Cuándo usarlo                          |
|--------------------|---------------------------------------------------------|----------------------------------------|
| `/setup-github`    | Instalar y configurar GitHub CLI                        | Primera vez o máquina nueva            |
| `/review-pr`       | Revisar un PR individual                                | Revisión detallada de un PR específico |
| `/list-prs`        | Listar PRs abiertos de un repositorio                   | Ver qué PRs están pendientes          |
| `/review-all-prs`  | Revisar TODOS los PRs abiertos en lote                  | Revisión masiva antes de release       |
| `/review`          | Revisión genérica de código (no PR)                     | Revisar código local o cambios locales |
| `/help`            | Mostrar esta ayuda                                      | Cuando no sepas qué comando usar       |

---

## Inicio Rápido

1. **¿Primera vez?** → Ejecuta `/setup-github`
2. **¿Quieres revisar un PR?** → Ejecuta `/review-pr`
3. **¿No sabes qué PR revisar?** → Ejecuta `/list-prs`
4. **¿Quieres revisar todo?** → Ejecuta `/review-all-prs`

---

## Configuración Actual

- **Repos configurados**: ver `.windsurf/rules/review-rules.md` sección 6
- **Reglas de evaluación**: `.windsurf/rules/review-rules.md`
- **Documentación completa**: `README.md`

---

## ¿Necesitas más ayuda?

- Para ver los criterios de evaluación: pide "muéstrame las reglas de revisión"
- Para cambiar el repositorio: indica el repo en formato `OWNER/REPO`
- Para personalizar reglas: edita `.windsurf/rules/review-rules.md`
