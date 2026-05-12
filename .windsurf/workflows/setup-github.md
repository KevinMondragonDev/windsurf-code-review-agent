---
description: Configurar GitHub CLI y autenticación para revisión de PRs
---

# Configuración de GitHub CLI

## Propósito
Configura la conexión con GitHub necesaria para usar los workflows de revisión de PRs.
Solo necesitas ejecutar esto **una vez** por máquina.

## Prerrequisitos
- Windows 10/11
- Cuenta de GitHub con acceso a los repositorios del equipo
- Conexión a internet

---

## Pasos

### 1. Verificar si GitHub CLI ya está instalado
// turbo
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh --version
```
- Si muestra versión → ir al paso 3.
- Si falla → continuar con paso 2.

### 2. Instalar GitHub CLI
```powershell
winget install GitHub.cli
```
Después de instalar, actualizar el PATH:
// turbo
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh --version
```

### 3. Verificar si ya estás autenticado
// turbo
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh auth status
```
- Si muestra "Logged in" → ir al paso 5.
- Si falla → continuar con paso 4.

### 4. Autenticarse en GitHub
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh auth login --web --git-protocol https
```
Sigue las instrucciones:
1. Seleccionar **GitHub.com**
2. Presionar **Y** para autenticar Git con tus credenciales
3. Copiar el **código** que aparece en terminal
4. Se abrirá el navegador → pegar el código y autorizar

### 5. Verificar autenticación final
// turbo
```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User"); gh auth status
```

### 6. Confirmación
Si todo está correcto, confirmar al usuario que:
- GitHub CLI está instalado y autenticado.
- Ya puede usar `/review-pr`, `/list-prs` y `/review-all-prs`.

---

## Solución de Problemas

| Problema                              | Solución                                              |
|---------------------------------------|-------------------------------------------------------|
| `winget` no reconocido                | Actualizar Windows o instalar gh manualmente desde https://cli.github.com |
| `gh` no reconocido tras instalar      | Cerrar y reabrir terminal, o ejecutar el comando de PATH del paso 2 |
| Error de autenticación                | Verificar que la cuenta tiene acceso al repo           |
| Token expirado                        | Ejecutar `gh auth refresh`                             |
