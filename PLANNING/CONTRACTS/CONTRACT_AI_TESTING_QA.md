# CONTRATO DE TESTING, QA Y CALIDAD DE CÓDIGO PARA AGENTES DE IA
**Proyecto:** [NOMBRE DEL PROYECTO]
**Versión:** 1.0 | **Fecha:** 15/06/2026 | **Autor:** Alexis Loyola Campos — Aloyc México

## ⚠️ INSTRUCCIONES PARA EL AGENTE DE IA
Este documento establece las reglas inquebrantables de Aseguramiento de Calidad (QA), Testing Automatizado y Estándares de Código. Tu objetivo NO es escribir tests para "cumplir con la cobertura", sino para **prevenir regresiones, documentar el comportamiento esperado y garantizar la confiabilidad del sistema en escenarios del mundo real**.

Queda estrictamente prohibido generar tests superficiales que solo validen el "Camino Feliz" (Happy Path) o aserciones triviales (`expect(result).toBeDefined()`). Si una feature no tiene tests que cubran sus Edge Cases y escenarios de fallo, la feature se considera **INCOMPLETA** y no debe marcarse como terminada.

Este contrato tiene prioridad sobre la velocidad de entrega. Código sin tests es deuda técnica inaceptable.

## ÍNDICE
* [1. Principios Fundamentales de Testing](#1-principios-fundamentales-de-testing)
* [2. La Pirámide de Testing y Cobertura Obligatoria](#2-la-pirámide-de-testing-y-cobertura-obligatoria)
* [3. Anatomía de un Test Perfecto (Estructura AAA)](#3-anatomía-de-un-test-perfecto-estructura-aaa)
* [4. La Matriz de Edge Cases (Lo que SIEMPRE debes testear)](#4-la-matriz-de-edge-cases-lo-que-siempre-debes-testear)
* [5. Mocking, Stubs y Aislamiento](#5-mocking-stubs-y-aislamiento)
* [6. Testing de UI y Componentes (Frontend)](#6-testing-de-ui-y-componentes-frontend)
* [7. Testing de APIs y Backend](#7-testing-de-apis-y-backend)
* [8. Calidad de Código Estática y Dinámica](#8-calidad-de-código-estática-y-dinámica)
* [9. CI/CD y Gatekeeping Automatizado](#9-cicd-y-gatekeeping-automatizado)
* [10. Checklist Final de QA](#10-checklist-final-de-qa)

---

## 1. PRINCIPIOS FUNDAMENTALES DE TESTING

### 1.1 Filosofía de Calidad
**CLÁUSULA 1.1.1 — LOS TESTS SON DOCUMENTACIÓN EJECUTABLE**
Los tests son la mejor documentación del sistema. Un desarrollador nuevo debe poder leer el nombre de un test y entender exactamente qué hace la función, qué acepta y qué rechaza, sin leer el código de implementación.

**CLÁUSULA 1.1.2 — PRINCIPIOS F.I.R.S.T.**
Todo test debe cumplir con el acrónimo F.I.R.S.T.:
* **F**ast (Rápido): Los tests unitarios deben ejecutarse en milisegundos.
* **I**solated (Aislado): Un test no debe depender de otro test ni de su orden de ejecución.
* **R**epeatable (Repetible): Debe pasar igual en cualquier entorno (local, CI, sin internet).
* **S**elf-Validating (Auto-validante): El test debe decir si pasó o falló (booleano). Cero logs manuales para verificar.
* **T**imely (Oportuno): Se escribe junto con el código (TDD) o inmediatamente después.

**CLÁUSULA 1.1.3 — PROBAR COMPORTAMIENTO, NO IMPLEMENTACIÓN**
Los tests deben verificar QUÉ hace el código (entradas y salidas/efectos), no CÓMO lo hace internamente. Los tests acoplados a la implementación (ej. verificar que se llamó a una función privada específica) son frágiles y rompen con cada refactor.

**CLÁUSULA 1.1.4 — DETERMINISMO ABSOLUTO**
Los tests NO pueden ser "flaky" (intermitentes). Prohibido depender de `Date.now()`, `Math.random()` o tiempos de red reales en tests unitarios. Todo factor externo debe ser inyectado o mockeado para garantizar que el test pase el 100% de las veces.

---

## 2. LA PIRÁMIDE DE TESTING Y COBERTURA OBLIGATORIA

**CLÁUSULA 2.1.1 — DISTRIBUCIÓN DE TESTS**
El proyecto debe seguir la Pirámide de Testing de Mike Cohn:
1. **Unit Tests (70%):** Lógica de negocio pura, utilidades, validaciones, modelos de dominio. (Herramienta: Vitest / Jest).
2. **Integration Tests (20%):** Interacción entre módulos, Hooks con APIs, Base de Datos. (Herramienta: Vitest + MSW / Supertest).
3. **E2E Tests (10%):** Flujos críticos de usuario (Login, Checkout, Core Feature). (Herramienta: Playwright).

**CLÁUSULA 2.1.2 — COBERTURA MÍNIMA POR CAPA**
* **Lógica de Negocio Crítica (Pagos, Permisos, Cálculos):** 100% de cobertura de ramas (Branch Coverage).
* **Utilidades y Helpers:** 90%+ de cobertura.
* **Componentes UI:** No medir por cobertura de líneas, sino por **Cobertura de Funcionalidad** (todos los estados, interacciones y props).
* **Código Legacy:** No se permite escribir código nuevo sin tests. Si se toca código legacy sin tests, se DEBE agregar cobertura como parte del commit (Boy Scout Rule).

**CLÁUSULA 2.1.3 — PROHIBIDO `test.skip` O `xtest` EN PRODUCCIÓN**
Ningún test puede estar deshabilitado (`skip`, `todo`, `xit`) en la rama principal (`main`/`master`). Si un test falla, se arregla el código o el test; no se silencia. Las excepciones temporales deben tener un comentario con ticket de Issue y fecha de expiración.

---

## 3. ANATOMÍA DE UN TEST PERFECTO (ESTRUCTURA AAA)

**CLÁUSULA 3.1.1 — PATRÓN AAA (ARRANGE, ACT, ASSERT)**
Todo test debe estar visualmente dividido en tres bloques claros separados por una línea en blanco.

```typescript
// ✅ CORRECTO — Estructura AAA clara
describe('calculateDiscount', () => {
  it('should apply 20% discount for premium users on orders over $100', () => {
    // ARRANGE (Preparar datos y estado)
    const user = { role: 'premium', id: '1' };
    const cartTotal = 150;

    // ACT (Ejecutar la acción a probar)
    const finalPrice = calculateDiscount(cartTotal, user);

    // ASSERT (Verificar el resultado esperado)
    expect(finalPrice).toBe(120);
  });
});
```

**CLÁUSULA 3.2.1 — NOMENCLATURA DESCRIPTIVA (BDD STYLE)**
El nombre del test (`it` / `test`) debe leerse como una especificación de negocio en lenguaje casi natural.
* ❌ `test('test function 1')`
* ❌ `test('returns false if invalid')`
* ✅ `it('should return false when user age is below 18')`
* ✅ `it('should throw UnauthorizedError if token is expired')`

**CLÁUSULA 3.3.1 — UNA ASERCIÓN LÓGICA POR TEST**
Un bloque `it()` debe probar UN solo concepto lógico. Puede tener múltiples `expect()` si verifican el mismo resultado desde distintos ángulos, pero si fallan por razones distintas, deben separarse en tests independientes.

---

## 4. LA MATRIZ DE EDGE CASES (LO QUE SIEMPRE DEBES TESTEAR)
*(Esta es la cláusula más importante. Las IAs suelen olvidar esto).*

**CLÁUSULA 4.1.1 — LA REGLA DE LOS EXTREMOS Y LÍMITES**
Para toda función que acepte parámetros o procese datos, DEBES generar tests explícitos para:

| Categoría | Qué testear | Ejemplo |
| --- | --- | --- |
| **Vacío / Nulo** | `null`, `undefined`, `[]`, `{}`, `""` | `getTotal([])` debe retornar 0, no `NaN`. |
| **Límites Inferiores** | Cero, números negativos, strings vacíos | `calculateAge(-1)` debe lanzar error. |
| **Límites Superiores** | `MAX_SAFE_INTEGER`, strings de 10MB, arrays gigantes | Evitar desbordamiento de memoria o loops infinitos. |
| **Tipos Incorrectos** | Pasar string donde va number, objeto donde va array | El validador (Zod) debe rechazarlo elegantemente. |
| **Caracteres Especiales** | Emojis, Unicode, inyección SQL/XSS básica | `"Robert'); DROP TABLE Students;--"` |
| **Concurrencia** | Múltiples llamadas simultáneas a la misma función | Evitar *Race Conditions* en actualizaciones de estado. |

**CLÁUSULA 4.2.1 — TESTS DE ESCENARIOS DE FALLO (UNHAPPY PATH)**
Por cada llamada a API, Base de Datos o Servicio Externo, DEBE existir un test que simule el fallo:
* ❌ Timeout de red (Network Error).
* ❌ Respuesta 401 / 403 / 500 del servidor.
* ❌ Base de datos caída o sin permisos.
* ❌ Datos corruptos o formato JSON inválido desde el servidor.

```typescript
// ✅ CORRECTO — Probando el Unhappy Path
it('should display error toast when API returns 500', async () => {
  server.use(rest.get('/api/data', (req, res, ctx) => res(ctx.status(500))));
  
  render(<UserProfile />);
  
  await waitFor(() => {
    expect(screen.getByText(/Error al cargar datos/i)).toBeInTheDocument();
  });
});
```

---

## 5. MOCKING, STUBS Y AISLAMIENTO

**CLÁUSULA 5.1.1 — MOCKEAR SOLO LO EXTERNO (FRONTERAS DEL SISTEMA)**
Solo se deben mockear:
1. APIs de terceros (Stripe, OpenAI, SendGrid).
2. Base de datos (si no se usa una DB en memoria para testing).
3. Reloj del sistema (`Date`, `setTimeout`) y Generadores Aleatorios (`Math.random`).
**NUNCA** mockear módulos internos del propio proyecto para "facilitar" el test. Eso oculta bugs de integración.

**CLÁUSULA 5.2.1 — USO DE MSW (MOCK SERVICE WORKER) PARA APIs**
Para pruebas de frontend e integración, usar **MSW** para interceptar peticiones a nivel de red en lugar de mockear `fetch` o `axios` directamente. Esto prueba el código de red real de la aplicación.

**CLÁUSULA 5.3.1 — LIMPIEZA DE MOCKS (TEARDOWN)**
Todo mock, stub o espía DEBE limpiarse después de cada test usando `afterEach(() => vi.restoreAllMocks())` o configuraciones globales. Los mocks "filtrados" causan que tests subsecuentes fallen misteriosamente.

---

## 6. TESTING DE UI Y COMPONENTES (FRONTEND)

**CLÁUSULA 6.1.1 — REACT TESTING LIBRARY (FILOSOFÍA)**
Los tests de UI deben probar la aplicación **como lo hace un usuario real**.
* ❌ Prohibido buscar elementos por `className`, `id` o `data-testid` (salvo excepción justificada).
* ✅ Buscar por rol (`getByRole('button')`), texto (`getByText`), etiqueta (`getByLabelText`) o placeholder.

**CLÁUSULA 6.2.1 — PROBAR ESTADOS ASÍNCRONOS**
Todo componente que cargue datos debe tener tests para:
1. Estado de Carga (¿Aparece el Skeleton/Spinner?).
2. Estado de Éxito (¿Se renderizan los datos?).
3. Estado de Error (¿Aparece el mensaje de error y el botón de reintentar?).
4. Estado Vacío (¿Aparece el "Empty State"?).

**CLÁUSULA 6.3.1 — TESTING DE ACCESIBILIDAD (a11y)**
Integrar `jest-axe` o `@axe-core/playwright` en los tests de componentes para detectar automáticamente violaciones de WCAG (contraste, etiquetas ARIA faltantes, foco).
```typescript
import { axe, toHaveNoViolations } from 'jest-axe';
expect.extend(toHaveNoViolations);

it('should have no accessibility violations', async () => {
  const { container } = render(<CheckoutForm />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

**CLÁUSULA 6.4.1 — E2E CON PLAYWRIGHT PARA FLUJOS CRÍTICOS**
Los flujos de negocio principales (Registro, Login, Checkout, Core Action) DEBEN tener al menos un test E2E en Playwright que recorra el flujo completo en un navegador real (Chromium, WebKit, Firefox).

---

## 7. TESTING DE APIS Y BACKEND

**CLÁUSULA 7.1.1 — TESTS DE CONTRATO (SCHEMA VALIDATION)**
Toda respuesta de API debe ser validada contra su Schema (Zod / JSON Schema) en los tests de integración. Esto previene que cambios en el backend rompan a los clientes silenciosamente.

**CLÁUSULA 7.2.1 — AISLAMIENTO DE BASE DE DATOS EN TESTS**
Los tests de backend NUNCA deben correr contra la base de datos de desarrollo o producción. Usar:
* **Opción A:** Base de datos en memoria (SQLite para pruebas).
* **Opción B:** Transacciones de Base de Datos que hacen `ROLLBACK` al final de cada test (rápido y limpio).
* **Opción C:** Contenedores Docker efímeros (TestContainers) por cada suite de tests.

**CLÁUSULA 7.3.1 — VERIFICACIÓN DE HEADERS Y COOKIES**
Los tests de API deben verificar no solo el `body` de la respuesta, sino también:
* Status Code correcto (200, 201, 400, 401, 403, 429).
* Headers de Seguridad presentes (CSP, HSTS).
* Cookies de sesión configuradas con `HttpOnly`, `Secure`, `SameSite`.

---

## 8. CALIDAD DE CÓDIDO ESTÁTICA Y DINÁMICA

**CLÁUSULA 8.1.1 — LINTEO ESTRICTO OBLIGATORIO**
El proyecto DEBE tener configurado ESLint con las siguientes reglas en modo "Error" (bloquean el commit):
* `@typescript-eslint/no-explicit-any` (Cero `any`).
* `@typescript-eslint/no-unused-vars` (Cero variables muertas).
* `no-console` (Cero `console.log` en producción, usar logger).
* `react-hooks/exhaustive-deps` (Previene bugs de closures en React).

**CLÁUSULA 8.2.1 — COMPLEJIDAD CICLOMÁTICA**
Ninguna función puede tener una complejidad ciclomática mayor a **10**. (La complejidad ciclomática mide el número de caminos independientes a través del código; muchos `if/else` y `switch` la aumentan). Si se excede, la función DEBE refactorizarse y dividirse.

**CLÁUSULA 8.3.1 — ANÁLISIS ESTÁTICO DE SEGURIDAD (SAST)**
Integrar herramientas como **Semgrep** o **CodeQL** en el pipeline de CI para detectar vulnerabilidades comunes (SQLi, XSS, Path Traversal) analizando el código fuente sin ejecutarlo.

---

## 9. CI/CD Y GATEKEEPING AUTOMATIZADO

**CLÁUSULA 9.1.1 — EL PIPELINE ES LA LEY**
El pipeline de Integración Continua (GitHub Actions / GitLab CI) DEBE ejecutar en cada Pull Request:
1. Linter y Formateo (Prettier).
2. Análisis de Tipos (`tsc --noEmit`).
3. Suite completa de Tests Unitarios y de Integración.
4. Auditoría de Dependencias (`npm audit`).
**Si alguno de estos pasos falla, el botón de "Merge" debe estar bloqueado automáticamente.**

**CLÁUSULA 9.2.1 — TESTS EN MÚLTIPLES ENTORNOS**
La suite de CI debe ejecutarse al menos en:
* Node.js LTS actual y versión anterior.
* Matriz de navegadores para E2E (Chromium, Firefox, Safari).
* Sistema Operativo Linux (Ubuntu latest) como entorno base de producción.

**CLÁUSULA 9.3.1 — REPORTES DE COBERTURA**
Generar reportes de cobertura (usando `c8` o `istanbul`) en cada PR. Un PR que reduzca la cobertura global del proyecto en más de un **2%** sin justificación documentada debe ser rechazado.

---

## 10. CHECKLIST FINAL DE QA

El agente debe revisar este checklist antes de entregar cualquier código o Pull Request:

**Cobertura y Escenarios**
- [ ] Se escribió al menos 1 test unitario por cada función de lógica de negocio.
- [ ] Se probaron los Edge Cases: Datos nulos, vacíos, límites superior/inferior.
- [ ] Se probaron los "Unhappy Paths" (Errores de red, timeouts, respuestas 500).
- [ ] Los tests son deterministas (no hay `Math.random` ni fechas reales sin mockear).

**Estructura y Legibilidad**
- [ ] Los tests siguen el patrón AAA (Arrange, Act, Assert) con espacios en blanco.
- [ ] El nombre del `it()` describe el comportamiento en lenguaje de negocio.
- [ ] No hay tests anidados excesivamente (`describe` dentro de `describe` x 5).
- [ ] No hay lógica compleja (if/for) dentro de los bloques `expect`.

**Frontend / UI**
- [ ] Se usan queries de Testing Library (`getByRole`, `getByText`) en lugar de selectores CSS.
- [ ] Se probaron los 4 estados del componente (Loading, Empty, Error, Success).
- [ ] Se incluyó test de accesibilidad (`jest-axe`) para componentes complejos.

**Backend / API**
- [ ] Se validó que el Status Code retornado es el correcto.
- [ ] Se validó el Schema de la respuesta (Zod/JSON Schema).
- [ ] Los tests de DB usan transacciones o DB en memoria (no ensucian la DB real).

**Calidad Estática**
- [ ] `npm run lint` pasa sin errores ni warnings.
- [ ] `tsc --noEmit` pasa sin errores de tipos.
- [ ] No hay `test.skip` o `xtest` en el código entregado.

---

## DECLARACIÓN DE CUMPLIMIENTO
Al escribir código para este proyecto, el agente declara:
* **Código sin tests es código roto:** Asumirá que cualquier línea de código no cubierta por un test es un bug latente esperando ocurrir.
* **Paranoia constructiva:** Escribirá tests asumiendo que el usuario final introducirá los datos más absurdos, destructivos e inesperados posibles.
* **Mantenibilidad del Test Suite:** Tratará el código de los tests con el mismo respeto y rigor de Clean Code que el código de producción. Un test sucio es peor que no tener test.

---
*Diseñado por Alexis Loyola Campos — Aloyc México*
*Fundamentado en: Clean Code, Google Testing Blog, Testing Library Principles, Playwright Best Practices*
*Aplicable a: Cualquier proyecto, cualquier framework, cualquier suite de testing*