# 🤖 Windsurf Code Review Agent

> Agente de IA para revisión automatizada de Pull Requests usando [Windsurf IDE](https://windsurf.com).

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Windsurf](https://img.shields.io/badge/Windsurf-IDE-purple)](https://windsurf.com)
[![GitHub CLI](https://img.shields.io/badge/GitHub_CLI-required-green)](https://cli.github.com)

---

## ¿Qué es esto?

Un **kit de configuración listo para usar** que convierte a Windsurf en un revisor de código automatizado. Usa correctamente las features de Windsurf (Skills, Rules, Workflows) para analizar Pull Requests con criterios estandarizados.

### Características

- ✅ Revisión automatizada de PRs con análisis triple (funcional + calidad + técnico)
- ✅ Criterios de evaluación personalizables por proyecto
- ✅ Reportes estandarizados con severidades (🔴 Crítico, 🟡 Importante, 🔵 Menor)
- ✅ Publicación opcional de análisis como comentario en GitHub
- ✅ Revisión en lote de todos los PRs abiertos
- ✅ **No aprueba ni rechaza** — la decisión final es del humano
- ✅ Genérico: funciona con cualquier repositorio Java/Spring + JSP/jQuery

---

## Inicio Rápido

### Prerrequisitos

| Herramienta     | Versión | Propósito                        |
|-----------------|---------|----------------------------------|
| [Windsurf IDE](https://windsurf.com) | Última | IDE con soporte de agente IA |
| [GitHub CLI](https://cli.github.com) | 2.x    | Conexión con GitHub         |
| Cuenta GitHub   | —       | Acceso a los repositorios        |

### Instalación

1. **Clona este repositorio** en tu máquina:
   ```bash
   git clone https://github.com/KevinMondragonDev/windsurf-code-review-agent.git
   ```

2. **Abre la carpeta** en Windsurf IDE.

3. **Configura tus repositorios** — edita `.windsurf/rules/review-rules.md`:
   ```markdown
   | Repositorio          | Rama base | Activo | Notas           |
   |----------------------|-----------|--------|-----------------|
   | tu-org/tu-repo       | main      | ✅     | Mi proyecto     |
   ```

4. **Configura GitHub CLI** — ejecuta en el chat de Windsurf:
   ```
   /setup-github
   ```

5. **Revisa tu primer PR**:
   ```
   /review-pr
   ```

---

## Comandos Disponibles

| Comando            | Qué hace                                             |
|--------------------|------------------------------------------------------|
| `/setup-github`    | Instala y configura GitHub CLI                       |
| `/review-pr`       | Revisa un PR individual (workflow principal)          |
| `/list-prs`        | Lista PRs abiertos para elegir cuál revisar          |
| `/review-all-prs`  | Revisa TODOS los PRs abiertos de un repo en lote     |
| `/review`          | Revisión genérica de código local (sin PR)           |
| `/help`            | Muestra índice de comandos                           |

---

## Flujo de Revisión

```
┌─────────────────────────────────────────────────────────────────┐
│                    FLUJO DE REVISIÓN DE PR                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Fase 0: Verificar autenticación (gh auth status)               │
│     │                                                           │
│     ▼                                                           │
│  Fase 1: Obtener datos del PR (metadata + diff)                 │
│     │                                                           │
│     ▼                                                           │
│  Fase 2: Análisis triple                                        │
│     ├── 2A: Validación funcional (¿cumple el feature?)          │
│     ├── 2B: Calidad de código (clean code, estándares)          │
│     └── 2C: Requisitos técnicos (cache busting, seguridad)      │
│     │                                                           │
│     ▼                                                           │
│  Fase 3: Generar reporte estandarizado                          │
│     │                                                           │
│     ▼                                                           │
│  Fase 4: (Opcional) Publicar análisis como comentario en el PR  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

> **Nota**: El agente **nunca** aprueba ni rechaza PRs. Solo genera el análisis y lo publica como comentario si el usuario lo autoriza.

---

## Estructura del Proyecto

```
.
├── .windsurfrules                          ← Reglas globales del agente (siempre activo)
├── .windsurf/
│   ├── rules/
│   │   └── review-rules.md                ← Repos + stack (regla ligera, model_decision)
│   ├── skills/
│   │   └── code-review/                   ← Skill principal (progressive disclosure)
│   │       ├── SKILL.md                   ← Entry point del proceso de revisión
│   │       ├── review-checklist.md        ← Checklists detallados con severidades
│   │       ├── severity-matrix.md         ← Matriz de decisión
│   │       ├── report-template.md         ← Formato del reporte
│   │       └── github-comment-templates.md← Plantillas para comentarios
│   └── workflows/
│       ├── setup-github.md                ← /setup-github
│       ├── review-pr.md                   ← /review-pr
│       ├── list-prs.md                    ← /list-prs
│       ├── review-all-prs.md              ← /review-all-prs
│       ├── help.md                        ← /help
│       └── review.md                      ← /review
├── GITHUB_CLI_README.md                   ← Referencia rápida de comandos gh
├── LICENSE                                ← MIT
└── README.md                              ← Este archivo
```

### Uso correcto de features Windsurf

| Feature | Archivo(s) | Cuándo se activa |
|---------|------------|------------------|
| **Global Rules** | `.windsurfrules` | Siempre — identidad del agente, idioma, comportamiento |
| **Rules** | `.windsurf/rules/review-rules.md` | `model_decision` — solo cuando es relevante |
| **Skills** | `.windsurf/skills/code-review/` | Automáticamente al pedir revisión, o con `@code-review` |
| **Workflows** | `.windsurf/workflows/*.md` | Manual — solo con `/slash-command` |

---

## Criterios de Evaluación

| Severidad  | Símbolo | Efecto en el análisis                  |
|------------|---------|----------------------------------------|
| Crítico    | 🔴      | 1 hallazgo → recomendación de rechazo  |
| Importante | 🟡      | 3+ hallazgos → recomendación de rechazo|
| Menor      | 🔵      | Solo observaciones, no bloquea         |

### Stack soportado por defecto

| Capa       | Tecnología                  |
|------------|-----------------------------|
| Backend    | Java 21+, Spring Framework  |
| Frontend   | JSP, JSTL, jQuery 3.x, CSS3|
| VCS        | GitHub                      |

> **¿Otro stack?** Modifica `review-checklist.md` en el Skill para adaptar los criterios a tu tecnología.

---

## Personalización

### Cambiar los repositorios a revisar
Edita `.windsurf/rules/review-rules.md` → tabla "Repositorios Configurados".

### Cambiar criterios de evaluación
Edita `.windsurf/skills/code-review/review-checklist.md` — agrega, quita o modifica reglas y severidades.

### Cambiar el formato del reporte
Edita `.windsurf/skills/code-review/report-template.md`.

### Cambiar el stack tecnológico
Modifica la tabla de Stack en `.windsurfrules` y en `review-rules.md`. Luego adapta el checklist.

### Agregar un nuevo workflow
Crea un archivo `.windsurf/workflows/mi-workflow.md` con frontmatter `description:`.

---

## Solución de Problemas

| Problema                          | Solución                                       |
|-----------------------------------|------------------------------------------------|
| `gh` no reconocido               | Ejecuta `/setup-github` o reinicia terminal    |
| No autenticado en GitHub          | `gh auth login --web --git-protocol https`     |
| PR no encontrado                  | Verifica número de PR y nombre del repo (`OWNER/REPO`) |
| Reporte no se genera              | Verifica que el diff del PR no esté vacío      |
| Skill no se invoca                | Usa `@code-review` manualmente en el chat      |

---

## Contribuir

¡Las contribuciones son bienvenidas! 🎉

- **Nuevos criterios de evaluación** → PR contra `review-checklist.md`
- **Soporte para otros stacks** (Python, Node, etc.) → Crea una variante del checklist
- **Mejoras a workflows** → PR contra `.windsurf/workflows/`
- **Bugs o sugerencias** → Abre un Issue

---

## Licencia

Este proyecto está bajo la licencia [MIT](LICENSE). Úsalo, modifícalo y compártelo libremente.
