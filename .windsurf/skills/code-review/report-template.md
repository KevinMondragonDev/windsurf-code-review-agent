# Plantilla de Reporte de Revisión

Usa este formato exacto para generar el reporte de revisión de un PR:

```
═══════════════════════════════════════════════════════════
  REPORTE DE REVISIÓN DE PR #[NÚMERO] — [REPO]
═══════════════════════════════════════════════════════════

📌 INFORMACIÓN GENERAL
  Título:    [título del PR]
  Autor:     [autor]
  Rama:      [head] → [base]
  Archivos:  [N] modificados | +[additions] -[deletions]
  Fecha:     [fecha de creación del PR]

───────────────────────────────────────────────────────────
🔍 1. VALIDACIÓN FUNCIONAL Y ALCANCE
───────────────────────────────────────────────────────────
  Estado: ✅ APROBADO / ⚠️ OBSERVACIONES / ❌ RECHAZADO

  Mapeo:        [resultado]
  Completitud:  [resultado]
  Granularidad: [resultado]

  Hallazgos:
  - [severidad] [descripción] — `archivo` línea ~N

───────────────────────────────────────────────────────────
🧹 2. CALIDAD DE CÓDIGO Y ESTÁNDARES
───────────────────────────────────────────────────────────
  Estado: ✅ APROBADO / ⚠️ OBSERVACIONES / ❌ RECHAZADO

  [Por cada archivo con hallazgos:]
  📄 `path/to/file.ext`
  - [severidad] Línea ~N: [descripción del problema]
    → Sugerencia: [corrección concreta o snippet]

───────────────────────────────────────────────────────────
⚙️ 3. REQUISITOS TÉCNICOS
───────────────────────────────────────────────────────────
  Estado: ✅ APROBADO / ⚠️ OBSERVACIONES / ❌ RECHAZADO

  Cache Busting: [✅/❌ detalle]
  Seguridad:     [✅/❌ detalle]
  Estructura:    [✅/❌ detalle]

═══════════════════════════════════════════════════════════
📋 RESUMEN EJECUTIVO
═══════════════════════════════════════════════════════════
  Veredicto Final: ✅ APROBADO / ⚠️ CON OBSERVACIONES / ❌ RECHAZADO

  [Resumen de 2-3 líneas sobre el estado general]

  Hallazgos 🔴 Críticos:    [N]
  Hallazgos 🟡 Importantes: [N]
  Observaciones 🔵 Menores: [N]

═══════════════════════════════════════════════════════════
💬 COMENTARIO PARA EL DESARROLLADOR
═══════════════════════════════════════════════════════════

  [Texto profesional y constructivo con:
   - Motivos de aprobación/rechazo
   - Acciones específicas para corregir (si aplica)
   - Reconocimiento de lo bien hecho (si aplica)]

═══════════════════════════════════════════════════════════
```
