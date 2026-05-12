# Plantillas de Comentarios para GitHub

## PR RECHAZADO
```
❌ PR Rechazado — Revisión Automatizada

Se encontraron [N] hallazgos que requieren corrección antes de aprobar.

🔴 Hallazgos Críticos:
1. [Descripción] — `path/to/file.java` línea ~[N]
   → Corrección: [snippet o descripción concreta]

🟡 Hallazgos Importantes:
1. [Descripción] — `path/to/file.java` línea ~[N]
   → Sugerencia: [snippet o descripción]

🔵 Observaciones Menores:
1. [Descripción]

Por favor corrige los hallazgos críticos e importantes y solicita nueva revisión.
```

## PR APROBADO CON OBSERVACIONES
```
⚠️ PR Aprobado con Observaciones — Revisión Automatizada

El código es funcional pero se detectaron hallazgos menores.

🟡 Hallazgos Importantes (no bloquean pero se recomienda corregir):
1. [Descripción] — `path/to/file.java` línea ~[N]

🔵 Observaciones Menores:
1. [Descripción]

Se aprueba el PR. Considerar las observaciones para futuras iteraciones.
```

## PR APROBADO
```
✅ PR Aprobado — Revisión Automatizada

El código cumple con los estándares del proyecto. Buen trabajo 👍

🔵 Sugerencias opcionales (no bloquean):
1. [Sugerencia de mejora, si aplica]
```

## Publicar en GitHub

> **IMPORTANTE**: El agente **NO aprueba ni rechaza** el PR.
> Solo publica el análisis como **comentario**. La decisión final es del integrador humano.

**Comando para publicar el análisis:**
```powershell
gh pr comment PR_NUMBER --repo OWNER/REPO --body "COMENTARIO"
```
