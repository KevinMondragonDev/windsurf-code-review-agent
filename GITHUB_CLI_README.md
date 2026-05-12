# GitHub CLI — Referencia Rápida

> **Para configuración inicial**, ejecuta el workflow `/setup-github` en el chat del agente.
> Este archivo es solo una referencia rápida de comandos útiles.

## Comandos Frecuentes

| Acción                          | Comando                                                    |
|---------------------------------|------------------------------------------------------------|
| Ver versión                     | `gh --version`                                             |
| Estado de autenticación         | `gh auth status`                                           |
| Listar PRs abiertos de un repo | `gh pr list --repo OWNER/REPO --state open`                |
| Ver detalle de un PR            | `gh pr view NUMERO --repo OWNER/REPO`                      |
| Ver diff de un PR               | `gh pr diff NUMERO --repo OWNER/REPO`                      |
| Listar tus repos                | `gh repo list --limit=50`                                  |
| Aprobar un PR                   | `gh pr review NUMERO --repo OWNER/REPO --approve`          |
| Solicitar cambios en un PR      | `gh pr review NUMERO --repo OWNER/REPO --request-changes`  |
| Cerrar sesión                   | `gh auth logout`                                           |

## Nota sobre PATH en Windows

Si `gh` no es reconocido después de instalar, ejecuta esto en PowerShell:
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```
