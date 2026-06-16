# CONTRATO DE ARQUITECTURA DE SOFTWARE Y CLEAN CODE PARA AGENTES DE IA
**Proyecto:** [NOMBRE DEL PROYECTO]
**Versión:** 1.0 | **Fecha:** 15/06/2026 | **Autor:** Alexis Loyola Campos — Aloyc México

## ⚠️ INSTRUCCIONES PARA EL AGENTE DE IA
Este documento establece las reglas inquebrantables de Arquitectura de Software, Diseño de Código y Mantenibilidad. Tu objetivo NO es solo que el código "funcione" o "compile", sino que sea **legible, testeable, escalable y mantenible** por humanos (y por ti mismo en el futuro).

Queda estrictamente prohibido generar "Código Espagueti", "Archivos Dios" (God Files) o mezclar capas de responsabilidad. Si una solicitud del usuario te obliga a violar estos principios para "ir más rápido", DEBES advertir sobre la deuda técnica que se está creando y proponer la implementación arquitectónicamente correcta.

Este contrato tiene prioridad sobre la velocidad de generación de código.

## ÍNDICE
* [1. Principios Fundamentales de Ingeniería](#1-principios-fundamentales-de-ingeniería)
* [2. Estructura de Carpetas y Arquitectura](#2-estructura-de-carpetas-y-arquitectura)
* [3. Separación de Responsabilidades (Capas)](#3-separación-de-responsabilidades-capas)
* [4. Gestión de Estado y Datos](#4-gestión-de-estado-y-datos)
* [5. Límites de Tamaño y Complejidad](#5-límites-de-tamaño-y-complejidad)
* [6. Nomenclatura y Convenciones de Código](#6-nomenclatura-y-convenciones-de-código)
* [7. Patrones de Diseño Obligatorios](#7-patrones-de-diseño-obligatorios)
* [8. Tipado Estricto y Validación](#8-tipado-estricto-y-validación)
* [9. Comentarios y Documentación](#9-comentarios-y-documentación)
* [10. Manejo de Errores a Nivel Arquitectónico](#10-manejo-de-errores-a-nivel-arquitectónico)
* [11. Refactorización y Deuda Técnica](#11-refactorización-y-deuda-técnica)
* [12. Checklist Final de Clean Code](#12-checklist-final-de-clean-code)

---

## 1. PRINCIPIOS FUNDAMENTALES DE INGENIERÍA

### 1.1 Filosofía de Desarrollo
**CLÁUSULA 1.1.1 — PRINCIPIOS SOLID (OBLIGATORIOS)**
Todo código orientado a objetos o modular debe respetar SOLID:
* **S (Single Responsibility):** Una clase, función o componente debe tener UNA y solo una razón para cambiar.
* **O (Open/Closed):** Abierto para extensión, cerrado para modificación. Usa interfaces y polimorfismo.
* **L (Liskov Substitution):** Las subclases deben ser sustituibles por sus clases base sin romper el sistema.
* **I (Interface Segregation):** Muchas interfaces específicas son mejores que una interfaz general y gorda.
* **D (Dependency Inversion):** Depende de abstracciones (interfaces/types), no de implementaciones concretas. Inyecta dependencias, no las instancies internamente.

**CLÁUSULA 1.1.2 — DRY (DON'T REPEAT YOURSELF) CON MATICES**
No duplicar lógica de negocio. Si ves el mismo bloque de código 3 veces, DEBES extraerlo a una función, hook o utilidad compartida. *Excepción:* En pruebas (tests) y en configuraciones explícitas donde la duplicación mejora la legibilidad (WET - Write Everything Twice - es preferible a una abstracción prematura).

**CLÁUSULA 1.1.3 — KISS (KEEP IT SIMPLE, STUPID)**
La solución más simple que resuelva el problema es la correcta. Evita sobre-ingeniería, patrones de diseño complejos (ej. Abstract Factory) cuando una función simple basta. La complejidad accidental es el enemigo.

**CLÁUSULA 1.1.4 — YAGNI (YOU AIN'T GONNA NEED IT)**
Nunca escribir código "por si acaso se necesita en el futuro". Solo implementar lo que el requerimiento actual exige. El código no escrito es código que no tiene bugs, no requiere mantenimiento y no ralentiza el sistema.

**CLÁUSULA 1.1.5 — BOY SCOUT RULE (REGLA DEL BOY SCOUT)**
"Deja el código siempre más limpio de como lo encontraste". Si al agregar una feature tocas un archivo legacy, refactoriza pequeños detalles (nombres de variables, extracción de funciones) como parte de tu commit.

---

## 2. ESTRUCTURA DE CARPETAS Y ARQUITECTURA

### 2.1 Topología del Proyecto (Feature-Sliced / Modular)
**CLÁUSULA 2.1.1 — ORGANIZACIÓN POR FEATURES, NO POR TIPOS**
Queda prohibido agrupar archivos por tipo técnico en carpetas planas globales (ej. `/components`, `/hooks`, `/services` en la raíz con cientos de archivos). La estructura debe ser **Modular por Features (Dominios)**.

```text
# ❌ PROHIBIDO (Estructura Plana por Tipo)
/src
  /components
    Button.tsx
    UserCard.tsx
    InvoiceTable.tsx
    ... (100 archivos)
  /hooks
    useAuth.ts
    useInvoices.ts

# ✅ CORRECTO (Estructura Modular por Feature/Dominio)
/src
  /app (Next.js App Router)
    /dashboard
      /invoices
        page.tsx
        layout.tsx
  /features
    /invoices
      /components (Solo UI de invoices)
        InvoiceTable.tsx
        InvoiceCard.tsx
      /hooks (Solo lógica de invoices)
        useInvoices.ts
      /services (Llamadas a API de invoices)
        invoiceService.ts
      /types (Zod schemas y Types de invoices)
        invoice.types.ts
      index.ts (Barril de exportación pública)
    /auth
  /shared (Código transversal reutilizable)
    /ui (Componentes genéricos: Button, Input)
    /lib (Utilidades puras: formatDate, cn)
    /config (Constantes globales)
```

**CLÁUSULA 2.1.2 — BARRILES DE EXPORTACIÓN (INDEX.TS)**
Cada módulo/feature DEBE tener un archivo `index.ts` que exporte ÚNICAMENTE la API pública del módulo. Los imports desde fuera del módulo siempre deben usar la ruta del módulo, nunca rutas profundas a archivos internos.

```typescript
// ✅ CORRECTO - Importando desde el barril
import { InvoiceTable, useInvoices } from '@/features/invoices';

// ❌ PROHIBIDO - Rompiendo el encapsulamiento
import { InvoiceTable } from '@/features/invoices/components/InvoiceTable';
import { _internalHelper } from '@/features/invoices/utils/helper';
```

**CLÁUSULA 2.1.3 — PROHIBIDOS LOS IMPORTS CIRCULARES**
Ningún archivo puede importar a otro que a su vez lo importe a él (directa o indirectamente). Las dependencias deben fluir en una sola dirección: `Shared ← Features ← App`. Si necesitas comunicación bidireccional, usa eventos, Context o inyección de dependencias.

---

## 3. SEPARACIÓN DE RESPONSABILIDADES (CAPAS)

### 3.1 Arquitectura en Capas (Adaptada a Frontend Moderno)
**CLÁUSULA 3.1.1 — PROHIBIDO FETCHING EN COMPONENTES UI**
Los componentes de UI (React/Vue) deben ser "tontos" (Presentational). NUNCA deben hacer llamadas a APIs, acceder a `localStorage`, o ejecutar lógica de negocio compleja. Solo reciben `props` y renderizan UI.

```jsx
// ❌ PROHIBIDO — Componente con lógica de red acoplada
function UserList() {
  const [users, setUsers] = useState([]);
  useEffect(() => {
    fetch('/api/users').then(res => res.json()).then(setUsers); // MAL
  }, []);
  return <ul>{users.map(...)}</ul>;
}

// ✅ CORRECTO — Separación Hook (Lógica) + Componente (UI)
function UserList() {
  const { data: users, isLoading, error } = useUsers(); // Hook maneja la red
  if (isLoading) return <UserListSkeleton />;
  if (error) return <ErrorState error={error} />;
  return <UserListUI users={users} />;
}
```

**CLÁUSULA 3.1.2 — CAPA DE SERVICIOS (SERVICES)**
Toda interacción con APIs externas, Backend o DB debe vivir en archivos `*.service.ts` o `*.api.ts`. Estos archivos contienen las funciones que llaman a `fetch`, `axios` o el cliente de Supabase. Los Hooks consumen los Services, los Services NO consumen Hooks.

**CLÁUSULA 3.1.3 — CAPA DE REPOSITORIOS (SI APLICA)**
Para operaciones complejas de base de datos, usar el patrón Repository que abstrae el origen del dato (API, LocalStorage, IndexedDB). Esto permite cambiar la fuente de datos sin reescribir la lógica de negocio.

**CLÁUSULA 3.1.4 — UTILIDADES PURAS (PURE FUNCTIONS)**
Las funciones en `/shared/lib` deben ser PURAS: dado el mismo input, siempre retornan el mismo output y no tienen efectos secundarios (side-effects). No leen globales, no modifican argumentos, no hacen I/O. Son fácilmente testeables.

---

## 4. GESTIÓN DE ESTADO Y DATOS

**CLÁUSULA 4.1.1 — SERVER STATE VS CLIENT STATE**
Diferenciar estrictamente entre:
* **Server State (Datos del Backend):** NUNCA usar Redux/Context para esto. Usar librerías de Data Fetching con caché (TanStack Query / React Query, SWR, Apollo). Manejan caché, revalidación, reintentos y estados de carga/error automáticamente.
* **Client State (UI State):** Estado efímero de la UI (modales abiertos, tabs activos, filtros). Usar `useState`, `useReducer` o librerías ligeras (Zustand, Jotai) solo si es global.

**CLÁUSULA 4.1.2 — PROHIBIDO EL "PROP DRILLING" PROFUNDO**
Ninguna prop debe pasar por más de 3 niveles de componentes. Si ocurre, usar:
1. **Composition / Children Pattern** (pasar componentes como props).
2. **Context API** (solo para temas, auth, i18n).
3. **Zustand/Jotai** (para estado global complejo).

**CLÁUSULA 4.1.3 — ESTADO DERIVADO, NO DUPLICADO**
Nunca almacenar en estado un valor que puede calcularse a partir de otro estado existente.
```typescript
// ❌ PROHIBIDO — Estado duplicado
const [items, setItems] = useState([]);
const [total, setTotal] = useState(0); // Derivable

// ✅ CORRECTO — Estado derivado (Memoizado si es costoso)
const [items, setItems] = useState([]);
const total = useMemo(() => items.reduce((sum, i) => sum + i.price, 0), [items]);
```

**CLÁUSULA 4.1.4 — INMUTABILIDAD OBLIGATORIA**
El estado nunca se muta directamente. Siempre crear nuevas referencias.
```typescript
// ❌ PROHIBIDO
user.name = "New Name"; 
setUser(user);

// ✅ CORRECTO
setUser(prev => ({ ...prev, name: "New Name" }));
```

---

## 5. LÍMITES DE TAMAÑO Y COMPLEJIDAD

**CLÁUSULA 5.1.1 — LÍMITE DE LÍNEAS POR ARCHIVO**
* **Componentes UI:** Máximo **200 líneas**.
* **Hooks / Services:** Máximo **150 líneas**.
* **Archivos de configuración/tipos:** Máximo **300 líneas**.
Si un archivo excede estos límites, DEBE ser refactorizado y dividido en archivos más pequeños antes de continuar.

**CLÁUSULA 5.2.1 — LÍMITE DE LÍNEAS POR FUNCIÓN**
Una función debe poder verse completa en una pantalla de laptop. Máximo **30-40 líneas**. Si es más larga, extraer sub-funciones con nombres descriptivos.

**CLÁUSULA 5.3.1 — LÍMITE DE PARÁMETROS**
Máximo **3 parámetros** por función. Si se requieren más, agruparlos en un objeto de opciones (`options: { ... }`) o usar el patrón Builder.

**CLÁUSULA 5.4.1 — PROFUNDIDAD DE ANIDAMIENTO (NESTING)**
Máximo **3 niveles** de indentación (if/for/try). Si se excede, usar "Early Returns" (Guard Clauses) o extraer a funciones.
```typescript
// ❌ PROHIBIDO (Deep Nesting)
function process(user) {
  if (user) {
    if (user.isActive) {
      if (user.hasPermission) {
        // Do something
      }
    }
  }
}

// ✅ CORRECTO (Early Returns)
function process(user) {
  if (!user || !user.isActive || !user.hasPermission) return;
  // Do something (Nivel 0 de indentación)
}
```

---

## 6. NOMENCLATURA Y CONVENCIONES DE CÓDIGO

**CLÁUSULA 6.1.1 — CONVENCIONES DE NOMBRADO ESTRICTAS**
* **Variables y Funciones:** `camelCase`. Nombres descriptivos, nunca abreviaturas crípticas (`usr`, `mgr`, `tmp`).
* **Componentes React y Clases:** `PascalCase`.
* **Constantes Globales:** `UPPER_SNAKE_CASE` (ej. `MAX_RETRY_COUNT`).
* **Archivos de Componentes:** `PascalCase.tsx` (ej. `UserProfile.tsx`).
* **Archivos de Hooks:** `camelCase.ts` empezando con `use` (ej. `useUserProfile.ts`).
* **Archivos de Utilidades:** `kebab-case.ts` o `camelCase.ts` (ej. `format-date.ts`).
* **Interfaces/Types:** `PascalCase`, opcionalmente con sufijo `Props`, `Response`, `Type` (ej. `User`, `UserProfileProps`, `ApiError`).

**CLÁUSULA 6.2.1 — FUNCIONES QUE HACEN UNA COSA (VERBOS)**
El nombre de la función debe indicar su efecto o retorno:
* `getUser()` (Retorna dato)
* `isUserAdmin()` (Retorna boolean)
* `calculateTotal()` (Retorna cálculo)
* `handleSubmit()` (Acción/Evento)
* `toCurrency()` (Transformación)

**CLÁUSULA 6.3.1 — BOOLEANS DEBEN SONAR A PREGUNTA**
Todas las variables booleanas deben empezar con prefijos como `is`, `has`, `should`, `can`.
```typescript
// ✅ CORRECTO
const isVisible = true;
const hasError = false;
const shouldRetry = true;
```

---

## 7. PATRONES DE DISEÑO OBLIGATORIOS

**CLÁUSULA 7.1.1 — CUSTOM HOOKS PARA LÓGICA COMPARTIDA**
Si una lógica de estado + efecto se repite en 2 o más componentes, DEBE extraerse a un Custom Hook (`useSomething`).

**CLÁUSULA 7.2.1 — COMPOSITION SOBRE HERENCIA**
En React y TS moderno, prohibido usar herencia de clases para compartir lógica. Usar Composición (pasar componentes como `children` o props) y Custom Hooks.

**CLÁUSULA 7.3.1 — STRATEGY PATTERN PARA CASOS COMPLEJOS**
En lugar de un `switch` gigante o múltiples `if/else` anidados para diferentes comportamientos, usar un objeto de estrategias (Map/Dictionary).
```typescript
// ✅ CORRECTO — Strategy Pattern
const paymentStrategies = {
  credit_card: (data) => processCreditCard(data),
  paypal: (data) => processPaypal(data),
  oxxo: (data) => processOxxo(data),
};

const processPayment = (method: string, data: any) => {
  const strategy = paymentStrategies[method];
  if (!strategy) throw new Error('Método no soportado');
  return strategy(data);
};
```

**CLÁUSULA 7.4.1 — FACTORY PARA CREACIÓN DE OBJETOS**
Si la creación de un objeto es compleja o depende de condiciones, encapsularla en una Factory Function en lugar de instanciarlo directamente en el código de negocio.

---

## 8. TIPADO ESTRICTO Y VALIDACIÓN

**CLÁUSULA 8.1.1 — PROHIBICIÓN ABSOLUTA DE `ANY`**
El uso de `any`, `@ts-ignore`, `@ts-nocheck` o `as any` está **ESTRICTAMENTE PROHIBIDO**. Genera falsa sensación de seguridad y propaga bugs silenciosos. Usar `unknown` y Type Guards cuando el tipo sea genuinamente desconocido.

**CLÁUSULA 8.2.1 — SCHEMAS ZOD COMO SINGLE SOURCE OF TRUTH**
Todos los datos que entran o salen del sistema (APIs, Forms, LocalStorage) deben validarse con **Zod** (o similar). Los tipos de TypeScript deben inferirse del Schema Zod, no escribirse a mano, para evitar divergencias.
```typescript
// ✅ CORRECTO — Zod como fuente única
import { z } from 'zod';

export const UserSchema = z.object({
  id: z.string().uuid(),
  name: z.string().min(2),
  email: z.string().email(),
  role: z.enum(['admin', 'user']),
});

export type User = z.infer<typeof UserSchema>; // Inferencia automática
```

**CLÁUSULA 8.3.1 — TYPE GUARDS EN LUGAR DE CASTEOS**
Para verificar tipos en runtime, usar Type Guards (`isUser(obj)`), no castear con `as`.
```typescript
// ✅ CORRECTO
function isUser(obj: unknown): obj is User {
  return UserSchema.safeParse(obj).success;
}
```

---

## 9. COMENTARIOS Y DOCUMENTACIÓN

**CLÁUSULA 9.1.1 — CÓDIGO AUTO-EXPLICATIVO (CLEAN CODE)**
El código debe leerse como prosa. Si necesitas un comentario para explicar QUÉ hace el código, el código está mal escrito y debe renombrarse o extraerse a una función con mejor nombre.

**CLÁUSULA 9.1.2 — COMENTARIOS SOLO PARA EL "POR QUÉ"**
Los comentarios solo son válidos para explicar:
* Decisiones de negocio complejas.
* Workarounds por bugs de librerías de terceros.
* Razones de rendimiento (por qué se usó un algoritmo no obvio).
* Advertencias de seguridad.
* `TODOs` con ticket de issue asociado (`// TODO(PROJ-123): Refactorizar cuando...`).

**CLÁUSULA 9.1.3 — JSDOC / TSDOC EN APIs PÚBLICAS**
Todas las funciones, hooks y componentes exportados públicamente (especialmente en `/shared` y `/features`) deben tener documentación JSDoc/TSDoc explicando: propósito, parámetros, retorno y ejemplos de uso.

---

## 10. MANEJO DE ERRORES A NIVEL ARQUITECTÓNICO

**CLÁUSULA 10.1.1 — ERROR BOUNDARIES (REACT)**
Toda aplicación debe tener `Error Boundaries` estratégicamente colocados para atrapar crashes de componentes. Un error en un widget no debe tumbar toda la aplicación. Deben mostrar una UI de fallback amigable.

**CLÁUSULA 10.1.2 — RESULT TYPES / EITHER PATTERN (OPCIONAL PERO RECOMENDADO)**
Para lógica de negocio crítica, evitar lanzar excepciones (`throw`). En su lugar, retornar objetos tipo `Result<T, E>` que obliguen al consumidor a manejar el error explícitamente.
```typescript
type Result<T, E = Error> = 
  | { success: true; data: T } 
  | { success: false; error: E };
```

**CLÁUSULA 10.2.1 — MANEJO CENTRALIZADO DE ERRORES DE RED**
Todas las peticiones a APIs deben pasar por un cliente centralizado (Axios instance o fetch wrapper) que intercepte errores 401 (redirigir a login), 403 (mostrar aviso), 500 (reportar a Sentry) y maneje reintentos automáticamente.

---

## 11. REFACTORIZACIÓN Y DEUDA TÉCNICA

**CLÁUSULA 11.1.1 — DETECCIÓN DE CODE SMELLS**
El agente DEBE identificar y señalar activamente "Code Smells" al revisar código existente:
* Funciones con más de 3 parámetros.
* Nombres de variables de 1 o 2 letras (excepto `i`, `j` en loops, `e` en eventos).
* Números mágicos (hardcoded) sin constante nombrada.
* Código comentado (debe borrarse, Git guarda el historial).
* Logs de depuración (`console.log`) en producción.

**CLÁUSULA 11.2.1 — NO DEJAR "TODOs" HUÉRFANOS**
Todo comentario `TODO` o `FIXME` debe tener asociado un Issue en el sistema de tracking (GitHub Issues, Jira) o una fecha límite. Los TODOs sin tracking son deuda técnica invisible.

---

## 12. CHECKLIST FINAL DE CLEAN CODE

El agente debe revisar este checklist antes de entregar cualquier código:

**Estructura y Arquitectura**
- [ ] El código está ubicado en la carpeta `/features` o `/shared` correcta
- [ ] No hay imports circulares entre módulos
- [ ] Los imports usan rutas absolutas (`@/...`) en lugar de relativas profundas (`../../../`)
- [ ] Se exporta solo la API pública a través de `index.ts`

**Componentes y UI**
- [ ] El componente es "tonto" (solo recibe props y renderiza)
- [ ] No hay llamadas a API o lógica pesada dentro del componente
- [ ] El archivo tiene menos de 200 líneas
- [ ] Las props están tipadas estrictamente (no `any`)

**Lógica y Funciones**
- [ ] Cada función hace UNA sola cosa (SRP)
- [ ] Las funciones tienen menos de 40 líneas
- [ ] Máximo 3 parámetros por función
- [ ] Uso de Early Returns en lugar de anidamiento profundo
- [ ] No hay código comentado (se usa Git para el historial)

**Estado y Datos**
- [ ] Server State manejado con React Query / SWR (no Redux para APIs)
- [ ] No hay prop drilling de más de 3 niveles
- [ ] El estado es inmutable (no hay mutaciones directas)
- [ ] Valores derivados con `useMemo` (si el cálculo es costoso)

**Tipado y Validación**
- [ ] Cero uso de `any`, `@ts-ignore` o `as any`
- [ ] Datos externos validados con Zod antes de usarse
- [ ] Types inferidos de Schemas, no duplicados

**Nomenclatura**
- [ ] Variables en `camelCase` descriptivo
- [ ] Componentes en `PascalCase`
- [ ] Booleans empiezan con `is`, `has`, `should`
- [ ] Funciones empiezan con verbos (`get`, `set`, `handle`, `calculate`)

---

## DECLARACIÓN DE CUMPLIMIENTO
Al generar o modificar código para este proyecto, el agente declara:
* **Legibilidad sobre astucia:** Priorizará código que un desarrollador junior pueda entender en 5 minutos sobre soluciones "clever" o ultra-optimizadas que requieran explicación.
* **Deuda técnica visible:** Si se ve forzado a escribir un "hack" o atajo por limitaciones de tiempo o de la plataforma, lo marcará explícitamente con un comentario `// HACK:` explicando la razón y creando un plan de refactorización.
* **Mantenibilidad a largo plazo:** Cada línea de código se escribe asumiendo que será leída, modificada y debuggeada por múltiples personas (y por el propio agente) durante los próximos 5 años.
* **Performance consciente:** Toda decisión arquitectónica considerará el impacto en rendimiento sin caer en optimización prematura.

---
*Diseñado por Alexis Loyola Campos — Aloyc México*
*Fundamentado en: Clean Code (Robert C. Martin), Domain-Driven Design, Atomic Design, Patterns.dev, Bulletproof React*
*Aplicable a: Cualquier proyecto, cualquier framework, cualquier lenguaje*