---
description: Revisar todos los PRs abiertos de un repositorio en lote (batch review)
---

# Revisión en Lote de Pull Requests

## Rol
Ejecutas el workflow `/review-pr` de forma iterativa para **todos** los PRs abiertos de un repositorio.

## Configuración
- **Repos configurados**: ver `.windsurf/rules/review-rules.md` sección "Repositorios configurados".
- Si el usuario no indica repo:
  - Si hay un solo repo configurado → usarlo.
  - Si hay varios o ninguno → **preguntar al usuario** (`OWNER/REPO`).

---

## Pasos

// turbo
1. Preparar entorno y verificar autenticación:
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh auth status
```
Si falla: indicar al usuario que ejecute `/setup-github`.

2. Determinar repositorio:
   - Si el usuario indicó un repo → usarlo.
   - Si hay un solo repo configurado en las reglas → usarlo.
   - Si no → **preguntar** al usuario (`OWNER/REPO`).

3. Obtener todos los PRs abiertos:
// turbo
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh pr list --repo OWNER/REPO --state open --json number,title,author,createdAt,headRefName,baseRefName
```

4. Confirmar con el usuario la lista de PRs a revisar antes de iniciar.

5. Para **cada PR**, ejecutar el flujo completo de `/review-pr`:
   - Leer `.windsurf/rules/review-rules.md` (solo la primera vez)
   - Obtener metadata + diff del PR
   - Ejecutar las 3 fases de análisis (funcional, calidad, técnico)
   - Generar reporte estandarizado individual

6. Al finalizar todos los PRs, generar el **resumen ejecutivo global**:

```
═══════════════════════════════════════════════════════════
  RESUMEN DE REVISIÓN EN LOTE — [REPO]
  Fecha: [fecha]
  PRs revisados: [N]
═══════════════════════════════════════════════════════════

  #  | PR     | Título                | Autor  | Veredicto
  ---|--------|-----------------------|--------|----------
  1  | #[N]   | [título]              | [user] | ✅/⚠️/❌
  2  | #[N]   | [título]              | [user] | ✅/⚠️/❌

───────────────────────────────────────────────────────────
  Total aprobados:          [N]
  Total con observaciones:  [N]
  Total rechazados:         [N]
  Total hallazgos 🔴:      [N]
  Total hallazgos 🟡:      [N]
  Total hallazgos 🔵:      [N]
═══════════════════════════════════════════════════════════
```

7. Preguntar al usuario si desea publicar los reviews en GitHub (individual o en lote).
