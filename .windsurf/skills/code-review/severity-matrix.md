# Matriz de Severidad y Decisión

## Tabla de Decisión

| Condición                               | Veredicto                              |
|-----------------------------------------|----------------------------------------|
| ≥1 hallazgo 🔴 Crítico                  | ❌ **RECHAZADO**                       |
| ≥3 hallazgos 🟡 Importante              | ❌ **RECHAZADO**                       |
| 1-2 hallazgos 🟡 Importante             | ⚠️ **CON OBSERVACIONES** (aprobar con notas) |
| Solo hallazgos 🔵 Menor                 | ✅ **APROBADO**                        |
| Sin hallazgos                           | ✅ **APROBADO**                        |

## Categorías de Severidad

| Severidad  | Símbolo | Ejemplos                                                      |
|------------|---------|---------------------------------------------------------------|
| Crítico    | 🔴      | Bugs, SQL injection, credenciales expuestas, datos perdidos   |
| Importante | 🟡      | Code smells, violaciones SOLID, performance, var en JS        |
| Menor      | 🔵      | Estilo, naming, docs faltantes, imports innecesarios          |

## Reglas de Aplicación

1. Contar los hallazgos por severidad al finalizar las 3 fases de análisis.
2. Aplicar la tabla de decisión de arriba hacia abajo (la primera condición que se cumpla determina el veredicto).
3. El veredicto es **definitivo** — no se negocia en el reporte.
4. Si hay duda sobre la severidad de un hallazgo, clasificar con la **severidad más alta** aplicable.
