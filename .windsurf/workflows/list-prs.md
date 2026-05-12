---
description: Listar todos los PRs abiertos de un repositorio para seleccionar cuál revisar
---

# Listar Pull Requests

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

3. Listar PRs abiertos:
// turbo
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh pr list --repo OWNER/REPO --state open --json number,title,author,createdAt,headRefName,baseRefName
```

4. Mostrar los resultados en formato tabla legible:

| #PR | Título | Autor | Rama | Creado |
|-----|--------|-------|------|--------|
| ... | ...    | ...   | ...  | ...    |

5. Preguntar al usuario si desea revisar alguno con `/review-pr`.
