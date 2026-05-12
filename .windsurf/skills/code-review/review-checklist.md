# Checklist de Revisión de Código

> Este archivo contiene los criterios detallados que el agente aplica al revisar un PR.
> Es la fuente de verdad para los checklists de evaluación.

---

## Stack Tecnológico del Proyecto

| Capa       | Tecnología                        | Convenciones               |
|------------|-----------------------------------|----------------------------|
| Backend    | Java 21+, Spring                  | Maven, paquetes por capa   |
| Frontend   | JSP, JSTL, jQuery 3.x, CSS3      | Carpetas por tipo          |
| VCS        | GitHub                            | PR por feature, main base  |

---

## 1. Validación Funcional y de Alcance

### 1.1 Mapeo de Features

| #  | Pregunta                                                              | Si falla         |
|----|-----------------------------------------------------------------------|------------------|
| 1  | ¿El título del PR describe claramente el feature?                     | 🔵 Observación   |
| 2  | ¿El body del PR explica qué se implementó y por qué?                 | 🔵 Observación   |
| 3  | ¿Todos los archivos modificados están relacionados con el feature?    | 🟡 Importante    |
| 4  | ¿Hay archivos modificados sin relación (cambios colaterales)?         | 🟡 Importante    |

**Regla**: Si el PR no tiene descripción, solicitar al autor que documente el propósito.

### 1.2 Completitud

| #  | Pregunta                                                              | Si falla         |
|----|-----------------------------------------------------------------------|------------------|
| 1  | ¿Se crearon los endpoints necesarios en el backend?                   | 🔴 Crítico       |
| 2  | ¿Se actualizaron las vistas JSP correspondientes?                     | 🔴 Crítico       |
| 3  | ¿Se incluyeron validaciones del lado del servidor?                    | 🟡 Importante    |
| 4  | ¿Se incluyeron validaciones del lado del cliente?                     | 🟡 Importante    |
| 5  | ¿Se manejan los casos de error?                                       | 🟡 Importante    |
| 6  | ¿Hay código incompleto (TODOs, métodos vacíos, stubs)?                | 🔴 Crítico       |

### 1.3 Granularidad

- **Regla estricta**: Máximo **1 feature por PR**.
- Si contiene más de 1 feature:
  - Marcar como 🟡 **Importante**.
  - Recomendar dividir en PRs separados.
  - Listar claramente los features detectados.
- **Excepción**: Refactors que afectan múltiples áreas por dependencia directa.

---

## 2. Calidad de Código y Estándares

### 2.1 Java — Clean Code

**Reglas descriptivas:**
* **Naming**: Clases en PascalCase, métodos y variables en camelCase, constantes en UPPER_SNAKE_CASE.
* **Métodos**: Máximo ~30 líneas. Si excede, sugerir extracción.
* **Métodos**: Deben tener un propósito claro y descriptivo.
* **Métodos**: Aplicar el principio *Fail Fast* usando cláusulas de guarda (*early returns*) al inicio para las validaciones y dejar el "camino feliz" al final sin indentar.
* **Clases**: Máximo ~100 líneas. Si excede, sugerir dividir.
* **Clases**: Principio de responsabilidad única (SRP).
* **Archivos**: Máximo ~500 líneas. Si excede, sugerir dividir.
* **Imports**: No debe haber imports no utilizados ni wildcards (`import java.util.*`).
* **Excepciones**: No usar `catch (Exception e)` genérico. Capturar excepciones específicas.
* **Null safety**: Preferir `Optional` sobre retornos null.
* **Magic numbers/strings**: Deben ser constantes con nombre descriptivo.
* **Comentarios**: Los comentarios deben explicar *por qué* se hace algo, no *qué*.
* **Logging**: Usar `logger` para registrar eventos, no `System.out.println`.
* **Testing**: Si hay código nuevo, debe incluir pruebas unitarias o de integración.
* **Complejidad**: Evitar métodos con demasiados parámetros (idealmente máximo 3 o 4). Si se necesitan más, considerar el uso de un objeto (`record` o `class`) para agruparlos.
* **Complejidad**: Evitar bucles anidados. Utilizar `Map` o la API de `Streams` para aplanar la lógica y optimizar el rendimiento.
* **Complejidad**: Ocultar condiciones booleanas complejas (múltiples `&&` o `||`) extrayéndolas a métodos privados con nombres autodescriptivos (ej. `esUsuarioValido()`).
* **Control de Flujo**: Reemplazar estructuras masivas de múltiples `if/else` o `switch` utilizando polimorfismo (Patrón Strategy), Mapas de acciones o *Pattern Matching* (Java 21).
* **Estructuras de Datos**: Utilizar `record` (introducidos en Java 14) para definir DTOs inmutables en las capas de entrada/salida.

**Tabla de severidades:**

| Regla                          | Criterio                                                    | Severidad |
|--------------------------------|-------------------------------------------------------------|-----------|
| Naming (clases)                | PascalCase                                                  | 🔵 Menor  |
| Naming (métodos/variables)     | camelCase                                                   | 🔵 Menor  |
| Naming (constantes)            | UPPER_SNAKE_CASE                                            | 🔵 Menor  |
| Longitud de métodos            | Máximo ~30 líneas, sugerir extracción si excede             | 🟡 Importante |
| Responsabilidad única (SRP)    | Una clase = una responsabilidad                             | 🟡 Importante |
| Imports no usados              | Prohibidos                                                  | 🔵 Menor  |
| Imports wildcard               | Prohibidos (`import java.util.*`)                           | 🔵 Menor  |
| Excepciones genéricas          | No usar `catch (Exception e)`, capturar específicas         | 🟡 Importante |
| Null safety                    | Preferir `Optional` sobre retornos null                     | 🟡 Importante |
| Magic numbers/strings          | Deben ser constantes con nombre descriptivo                 | 🟡 Importante |
| Inyección de dependencias      | Por constructor (NO `@Autowired` en campo)                  | 🟡 Importante |
| DTOs                           | No exponer entidades JPA directamente                       | 🟡 Importante |
| Validaciones                   | Usar `@Valid` / `@Validated`                                | 🔵 Menor  |

### 2.2 JavaScript / jQuery

| Regla                          | Criterio                                                    | Severidad |
|--------------------------------|-------------------------------------------------------------|-----------|
| Naming                         | camelCase para variables y funciones                        | 🔵 Menor  |
| var prohibido                  | Usar `const` por defecto, `let` solo si reasigna            | 🟡 Importante |
| Funciones anónimas largas      | Preferir funciones con nombre                               | 🔵 Menor  |
| Cachear selectores jQuery      | Si se usa más de una vez: `const $el = $('#id')`            | 🔵 Menor  |
| Event handlers inline          | Prohibido `onclick=""`. Usar `.on()`                        | 🟡 Importante |
| console.log en producción      | Prohibido                                                   | 🟡 Importante |

### 2.3 JSP

| Regla                          | Criterio                                                    | Severidad |
|--------------------------------|-------------------------------------------------------------|-----------|
| Scriptlets Java (`<% %>`)      | Minimizar. Preferir JSTL + EL                               | 🟡 Importante |
| Lógica de negocio en vista     | Prohibido. Solo presentación                                | 🔴 Crítico |
| Includes                       | Uso correcto de `<%@ include %>` y `<jsp:include>`          | 🔵 Menor  |

### 2.4 Documentación

| Regla                          | Criterio                                                    | Severidad |
|--------------------------------|-------------------------------------------------------------|-----------|
| Javadoc en clases públicas     | Obligatorio. Describir **qué hace**, no cómo               | 🔵 Menor  |
| Javadoc en métodos públicos    | `@param` y `@return` documentados                           | 🔵 Menor  |
| JSDoc en funciones expuestas   | Al menos descripción y parámetros                           | 🔵 Menor  |
| Header en archivos nuevos      | Comentario con propósito del archivo                        | 🔵 Menor  |

### 2.5 Detección de Intenciones

Cuando se detecta una mala práctica, el agente DEBE:
1. **Identificar** qué intentaba lograr el desarrollador.
2. **Explicar** por qué la implementación actual es problemática.
3. **Sugerir** la forma correcta con un snippet de código concreto.

---

## 3. Requisitos Técnicos

### 3.1 Cache Busting (CSS y JS)

**Regla estricta** — Severidad: 🔴 Crítico

Todo archivo estático (CSS/JS) referenciado en JSP **debe incluir versionado**.

✅ Correcto:
```html
<link rel="stylesheet" href="${pageContext.request.contextPath}/css/styles.css?v=${appVersion}">
<script src="${pageContext.request.contextPath}/js/app.js?v=${appVersion}"></script>
```

✅ Alternativa con timestamp:
```html
<link rel="stylesheet" href="css/styles.css?v=<%= System.currentTimeMillis() %>">
```

❌ Incorrecto (sin versión):
```html
<link rel="stylesheet" href="css/styles.css">
<script src="js/app.js"></script>
```

### 3.2 Seguridad

| #  | Regla                                                          | Severidad      |
|----|----------------------------------------------------------------|----------------|
| 1  | No hardcodear credenciales, tokens o API keys                  | 🔴 Crítico     |
| 2  | Validar inputs del usuario (frontend Y backend)                | 🔴 Crítico     |
| 3  | Usar PreparedStatement (prevenir SQL Injection)                 | 🔴 Crítico     |
| 4  | Escapar outputs en JSP (prevenir XSS)                           | 🔴 Crítico     |
| 5  | No exponer stack traces al usuario final                        | 🟡 Importante  |
| 6  | Validar permisos/roles en endpoints sensibles                   | 🟡 Importante  |

### 3.3 Estructura Spring Framework

```
src/main/java/com/proyecto/
├── controller/      ← Endpoints REST / MVC
├── service/         ← Lógica de negocio
├── repository/      ← Acceso a datos (JPA)
├── model/           ← Entidades JPA
├── dto/             ← Data Transfer Objects
└── config/          ← Configuración Spring
```

Si un archivo Java no está en la carpeta correcta según su responsabilidad: 🟡 Importante.
