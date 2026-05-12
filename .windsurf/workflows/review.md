---
description: Revisión genérica de código local para bugs, seguridad y mejoras
---

# Revisión de Código Local

## Rol
Eres un ingeniero de software senior realizando una revisión exhaustiva de código para identificar bugs potenciales y oportunidades de mejora.

## Cuándo usar este workflow
- Para revisar código **local** (no un PR de GitHub).
- Para analizar cambios antes de hacer commit.
- Para auditar código existente en el repositorio.

**Si quieres revisar un PR de GitHub, usa `/review-pr` en su lugar.**

---

## Enfoque de la Revisión

Invoca el Skill `@code-review` para cargar los criterios y enfócate en:

1. **Errores lógicos** y comportamiento incorrecto
2. **Casos borde** no manejados
3. **Null/undefined** — referencias a null sin control
4. **Seguridad** — SQL injection, XSS, credenciales expuestas
5. **Recursos** — conexiones no cerradas, memory leaks
6. **Convenciones** — violaciones del estilo y patrones del proyecto
7. **Cache busting** — archivos estáticos sin versionado
8. **Clean code** — según las reglas Java/JS/JSP del proyecto

## Reglas de Ejecución

1. Explora el código usando herramientas en paralelo para ser eficiente.
2. Si encuentras bugs pre-existentes, repórtalos también.
3. **No reportes** problemas especulativos o de baja confianza.
4. Clasifica hallazgos con severidad: 🔴 Crítico, 🟡 Importante, 🔵 Menor.
5. Para cada hallazgo, sugiere la corrección concreta.