# CONTRATO DE DISEÑO UX/UI Y ACCESIBILIDAD PARA AGENTES DE IA
**Proyecto:** [NOMBRE DEL PROYECTO]
**Versión:** 1.0 | **Fecha:** 15/06/2026 | **Autor:** Alexis Loyola Campos — Aloyc México

## ⚠️ INSTRUCCIONES PARA EL AGENTE DE IA
Este documento es un contrato vinculante de Experiencia de Usuario (UX) e Interfaz (UI) que DEBES cumplir al 100%. La IA tiende a generar interfaces que "funcionan en teoría" pero fallan en casos reales de uso. Tu objetivo NO es solo que el código compile, sino que la interfaz sea **utilizable, accesible, predecible y elegante** en todos los escenarios posibles.

Este contrato tiene prioridad absoluta sobre cualquier decisión estética arbitraria o atajo de desarrollo que degrade la experiencia del usuario.

## ÍNDICE
* [1. Principios Fundamentales de UX/UI](#1-principios-fundamentales-de-uxui)
* [2. Sistema de Diseño y Consistencia](#2-sistema-de-diseño-y-consistencia)
* [3. La Regla de los 4 Estados Obligatorios](#3-la-regla-de-los-4-estados-obligatorios)
* [4. Accesibilidad (a11y) y Estándares WCAG](#4-accesibilidad-a11y-y-estándares-wcag)
* [5. Diseño Responsive y Mobile-First](#5-diseño-responsive-y-mobile-first)
* [6. Formularios, Validación y Feedback](#6-formularios-validación-y-feedback)
* [7. Tipografía, Color y Contraste](#7-tipografía-color-y-contraste)
* [8. Navegación y Arquitectura de Información](#8-navegación-y-arquitectura-de-información)
* [9. Performance Percibido y Skeletons](#9-performance-percibido-y-skeletons)
* [10. Preferencias del Usuario (Dark Mode, Reducir Movimiento)](#10-preferencias-del-usuario-dark-mode-reducir-movimiento)
* [11. Microinteracciones y Lenguaje Corporal de la UI](#11-microinteracciones-y-lenguaje-corporal-de-la-ui)
* [12. Copywriting y Tono de Voz (UX Writing)](#12-copywriting-y-tono-de-voz-ux-writing)
* [13. Testing y Checklist Final de UX](#13-testing-y-checklist-final-de-ux)

---

## 1. PRINCIPIOS FUNDAMENTALES DE UX/UI

### 1.1 Filosofía de Diseño
**CLÁUSULA 1.1.1 — LEY DE JAKOB (FAMILIARIDAD)**
Los usuarios pasan la mayor parte de su tiempo en OTROS sitios. No reinventes la rueda. Los patrones de interacción (dónde va el logo, cómo funciona el carrito, dónde está el perfil) deben seguir las convenciones estándar de la industria a menos que haya una justificación UX documentada para innovar.

**CLÁUSULA 1.1.2 — LEY DE HICK (SIMPLICIDAD)**
El tiempo que tarda un usuario en tomar una decisión aumenta con el número y la complejidad de las opciones. Cada pantalla debe tener UN objetivo principal (Primary CTA). Evitar menús o formularios abrumadores; usar "Progressive Disclosure" (mostrar opciones avanzadas solo cuando se necesiten).

**CLÁUSULA 1.1.3 — TOLERANCIA AL ERROR (LEYES DE POKA-YOKE)**
La interfaz debe prevenir errores antes de que ocurran. Ejemplos: deshabilitar botones de envío hasta que el formulario sea válido, pedir confirmación en acciones destructivas, auto-guardar borradores.

**CLÁUSULA 1.1.4 — VISIBILIDAD DEL ESTADO DEL SISTEMA**
El sistema siempre debe mantener al usuario informado sobre qué está pasando en un tiempo razonable. Nunca debe haber una pantalla "congelada" sin un indicador visual (spinner, skeleton, barra de progreso, toast).

**CLÁUSULA 1.1.5 — CONTROL Y LIBERTAD DEL USUARIO**
Los usuarios a menudo ejecutan funciones por error. Siempre debe existir una "salida de emergencia" claramente marcada: botones de "Cancelar", "Deshacer" (Undo), "Volver", o papeleras de reciclaje (Soft Delete) antes de la eliminación permanente.

---

## 2. SISTEMA DE DISEÑO Y CONSISTENCIA

### 2.1 Tokens de Diseño
**CLÁUSULA 2.1.1 — USO ESTRICTO DE DESIGN TOKENS**
Nunca usar valores arbitrarios (magic numbers) como `margin: 17px`, `color: #4a90e2`, `font-size: 13px`. Todo debe provenir del sistema de diseño (Tailwind config, CSS Variables, Figma Tokens).
```css
/* ❌ PROHIBIDO */
.card { padding: 17px; border-radius: 9px; color: #333; }

/* ✅ CORRECTO — Usando escala predefinida */
.card { padding: var(--spacing-4); border-radius: var(--radius-md); color: var(--color-text-primary); }
/* O en Tailwind */
.card { p-4 rounded-lg text-gray-900 dark:text-gray-100; }
```

**CLÁUSULA 2.1.2 — ESCALA ESPACIAL BASADA EN 4px/8px**
Todos los márgenes, paddings, gaps y tamaños de iconos deben seguir una escala múltiplo de 4px (4, 8, 12, 16, 24, 32, 48, 64, 96). Esto crea un ritmo visual armónico y predecible.

**CLÁUSULA 2.1.3 — JERARQUÍA DE BOTONES**
Cada vista debe tener una jerarquía clara de acciones:
* **Primary Button:** Solo UNO por vista (ej. "Guardar", "Comprar"). Color de marca sólido.
* **Secondary Button:** Acciones alternativas (ej. "Cancelar"). Outline o ghost.
* **Tertiary/Link:** Acciones de bajo impacto (ej. "¿Olvidaste tu contraseña?"). Solo texto.
* **Destructive Button:** Rojo, para eliminar. Requiere confirmación.

---

## 3. LA REGLA DE LOS 4 ESTADOS OBLIGATORIOS
*(La cláusula más importante de este contrato. Las IAs suelen olvidar esto)*

**CLÁUSULA 3.0.1 — MANEJO EXPLÍCITO DE ESTADOS**
Todo componente o vista que dependa de datos asíncronos (API, DB) DEBE manejar y diseñar explícitamente estos 4 estados. No se acepta el estado por defecto del framework.

1. **Loading (Cargando):** Uso de Skeletons (esqueletos) en lugar de spinners genéricos siempre que sea posible. El skeleton debe imitar la forma del contenido real para reducir la ansiedad del usuario.
2. **Empty (Vacío / Estado Cero):** Qué se muestra cuando no hay datos (ej. "Aún no tienes facturas"). Debe incluir un Call-to-Action (CTA) para resolver el vacío (ej. "Crear tu primera factura").
3. **Error (Fallo):** Qué se muestra cuando la API falla. Debe explicar qué pasó en lenguaje humano, ofrecer un botón de "Reintentar" y, si es crítico, un enlace a "Soporte".
4. **Success (Éxito / Datos):** El estado ideal con datos poblados.

```jsx
// ✅ ESTRUCTURA OBLIGATORIA
function UserDashboard() {
  const { data, isLoading, isError, error } = useQuery(...);

  if (isLoading) return <DashboardSkeleton />;
  if (isError) return <ErrorState message={error.message} onRetry={refetch} />;
  if (!data || data.length === 0) return <EmptyState type="no-invoices" />;
  
  return <DataView data={data} />;
}
```

---

## 4. ACCESIBILIDAD (a11y) Y ESTÁNDARES WCAG

### 4.1 Cumplimiento WCAG 2.1 Nivel AA (Mínimo)
**CLÁUSULA 4.1.1 — NAVEGACIÓN POR TECLADO**
Toda funcionalidad debe ser operable mediante teclado. El orden de foco (Tab index) debe ser lógico y seguir el orden visual. Nunca usar `outline: none` en estados de `:focus` sin proveer un reemplazo visible y de alto contraste (`focus-visible:ring-2 ring-offset-2`).

**CLÁUSULA 4.1.2 — ETIQUETAS ARIA Y SEMÁNTICA HTML**
Usar etiquetas HTML semánticas (`<button>`, `<nav>`, `<main>`, `<article>`, `<aside>`) antes que `div` genéricos. Si se usan componentes personalizados, añadir roles ARIA (`role="dialog"`, `aria-modal="true"`, `aria-expanded`).
```html
<!-- ❌ PROHIBIDO -->
<div onClick={openModal}>Abrir</div>

<!-- ✅ CORRECTO -->
<button onClick={openModal} aria-haspopup="dialog" aria-controls="modal-id">
  Abrir
</button>
```

**CLÁUSULA 4.1.3 — IMÁGENES Y MEDIOS**
Toda imagen que transmita información debe tener un `alt` descriptivo. Las imágenes puramente decorativas deben tener `alt=""` (vacío) para que los lectores de pantalla las ignoren. Los videos deben tener opción de subtítulos.

**CLÁUSULA 4.1.4 — NO DEPENDER SOLO DEL COLOR**
Nunca usar el color como único medio para transmitir información (ej. "los campos en rojo son obligatorios"). Acompañar siempre con iconos, texto o patrones. Esto es vital para usuarios con daltonismo.

---

## 5. DISEÑO RESPONSIVE Y MOBILE-FIRST

**CLÁUSULA 5.1.1 — MOBILE-FIRST POR DEFECTO**
El CSS debe escribirse primero para móviles (pantallas < 640px) y luego expandirse con `@media (min-width: ...)` o breakpoints de Tailwind (`sm:`, `md:`, `lg:`).
```css
/* ✅ CORRECTO — Mobile First */
.container { padding: 1rem; }
@media (min-width: 768px) { .container { padding: 2rem; } }
```

**CLÁUSULA 5.2.1 — ÁREAS TÁCTILES (TOUCH TARGETS)**
En dispositivos móviles, todo elemento interactivo (botones, enlaces, iconos) debe tener un área mínima de impacto de **44x44 píxeles** (iOS) o **48x48 píxeles** (Android/Material Design). Si el icono es pequeño, aumentar el padding del contenedor.

**CLÁUSULA 5.3.1 — OCULTAR vs REORGANIZAR**
En responsive, no solo "ocultar" elementos con `display: none` en móvil. Reorganizar el contenido para que fluya verticalmente de manera lógica. Ej: un dashboard de 3 columnas en desktop debe convertirse en tarjetas apiladas en móvil, no en columnas comprimidas e ilegibles.

---

## 6. FORMULARIOS, VALIDACIÓN Y FEEDBACK

**CLÁUSULA 6.1.1 — VALIDACIÓN EN TIEMPO REAL (ON BLUR)**
La validación de campos debe ocurrir al perder el foco (`onBlur`) o al escribir (`onChange` con debounce), NO solo al intentar enviar el formulario. El feedback de error debe aparecer inmediatamente debajo del campo correspondiente.

**CLÁUSULA 6.1.2 — MENSAJES DE ERROR ACCIONABLES**
Los mensajes de error deben explicar CÓMO solucionar el problema, no solo qué está mal.
* ❌ "Contraseña inválida"
* ✅ "La contraseña debe tener al menos 8 caracteres, una mayúscula y un número."

**CLÁUSULA 6.1.3 — AUTOCOMPLETADO DEL NAVEGADOR**
Usar los atributos `autocomplete` correctos (`autocomplete="email"`, `autocomplete="current-password"`, `autocomplete="shipping-address"`) para que los gestores de contraseñas y el navegador puedan ayudar al usuario a llenar el formulario rápidamente.

**CLÁUSULA 6.1.4 — ESTADOS DEL BOTÓN DE ENVÍO**
Al hacer clic en "Enviar":
1. El botón cambia a estado `disabled`.
2. El texto cambia a "Guardando..." o muestra un spinner.
3. Se previene el doble clic (doble envío).

---

## 7. TIPOGRAFÍA, COLOR Y CONTRASTE

**CLÁUSULA 7.1.1 — CONTRASTE DE COLOR (WCAG AA)**
El texto normal debe tener un ratio de contraste de al menos **4.5:1** contra su fondo. El texto grande (>18px o bold >14px) debe tener al menos **3:1**. Nunca usar gris claro sobre blanco.

**CLÁUSULA 7.2.1 — ESCALA TIPOGRÁFICA MODULAR**
Usar una escala tipográfica (ej. Major Third 1.250 o Perfect Fourth 1.333) para definir tamaños de fuente. No inventar tamaños.
* H1: 36px / 2.25rem
* H2: 30px / 1.875rem
* H3: 24px / 1.5rem
* Body: 16px / 1rem (Nunca menos de 16px para cuerpo de texto en web)
* Small: 14px / 0.875rem

**CLÁUSULA 7.3.1 — LONGITUD DE LÍNEA LEGIBLE**
El texto corrido (párrafos) debe tener entre **45 y 75 caracteres por línea** (incluyendo espacios). Usar `max-w-prose` en Tailwind o `max-width: 65ch` en CSS para evitar que el ojo se pierda al saltar de línea.

---

## 8. NAVEGACIÓN Y ARQUITECTURA DE INFORMACIÓN

**CLÁUSULA 8.1.1 — REGLA DE LOS 3 CLICS (CON MATICES)**
El usuario debe poder llegar a cualquier sección crítica en máximo 3 clics desde la Home. Si la arquitectura es más profunda, proveer breadcrumbs (migas de pan) y búsqueda global.

**CLÁUSULA 8.2.1 — BREADCRUMBS EN JERARQUÍAS PROFUNDAS**
En cualquier página que esté a más de 2 niveles de profundidad, mostrar breadcrumbs para que el usuario sepa dónde está y pueda retroceder un nivel fácilmente.

**CLÁUSULA 8.3.1 — ENLACES EXTERNOS**
Los enlaces que abren en una nueva pestaña (`target="_blank"`) deben:
1. Indicar visualmente que son externos (icono de flecha saliendo).
2. Tener `rel="noopener noreferrer"` por seguridad.
3. Advertir al usuario (vía aria-label o tooltip) que saldrá del sitio.

---

## 9. PERFORMANCE PERCIBIDO Y SKELETONS

**CLÁUSULA 9.1.1 — OPTIMISTIC UI (CUANDO APLIQUE)**
Para acciones como "Dar Like", "Marcar como favorito" o "Agregar al carrito", actualizar la UI instantáneamente (Optimistic Update) y revertir solo si el servidor falla. Esto hace que la app se sienta instantánea.

**CLÁUSULA 9.2.1 — SKELETONS SOBRE SPINNERS**
Para cargas de contenido estructurado (listas, dashboards, perfiles), usar Skeleton Screens (rectángulos grises animados que imitan la estructura) en lugar de un spinner centrado. Reduce la percepción de espera hasta en un 30%.

**CLÁUSULA 9.3.1 — LAZY LOADING DE IMÁGENES Y COMPONENTES**
Todas las imágenes debajo del fold (no visibles al cargar) deben tener `loading="lazy"`. Los componentes pesados (modales, editores, charts) deben cargarse mediante Dynamic Imports / Lazy Loading.

---

## 10. PREFERENCIAS DEL USUARIO (DARK MODE, REDUCIR MOVIMIENTO)

**CLÁUSULA 10.1.1 — DARK MODE COMO CIUDADANO DE PRIMERA CLASE**
El Dark Mode no es un "hack" con filtros CSS invertidos. Debe diseñarse con una paleta específica:
* Fondos: Nunca negro puro `#000`. Usar grises oscuros (`#121212`, `zinc-900`).
* Elevación: Los elementos elevados (modales, cards) deben ser ligeramente más claros que el fondo para simular luz.
* Contraste: Reducir ligeramente el contraste del texto blanco puro a `gray-200` o `gray-300` para evitar fatiga visual.

**CLÁUSULA 10.2.1 — RESPETO A `prefers-reduced-motion`**
Si el usuario tiene configurado "Reducir movimiento" en su SO, TODAS las animaciones complejas (parallax, slides, transiciones largas) deben deshabilitarse o reducirse a un simple `fade-in`.
```css
@media (prefers-reduced-motion: reduce) {
  * { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
}
```

---

## 11. MICROINTERACCIONES Y LENGUAJE CORPORAL DE LA UI

**CLÁUSULA 11.1.1 — CURSORES ADECUADOS**
Todo elemento clickeable debe tener `cursor: pointer`. Los campos de texto `cursor: text`. Los elementos deshabilitados `cursor: not-allowed` y `opacity` reducida.

**CLÁUSULA 11.2.1 — FEEDBACK TÁCTIL EN HOVER Y ACTIVE**
Los botones deben cambiar de color o elevación al hacer `:hover` (desktop) y tener un efecto de "presión" al hacer `:active` (clic). La UI debe sentirse física y receptiva.

**CLÁUSULA 11.3.1 — TOASTS Y NOTIFICACIONES**
Las notificaciones temporales (Toasts/Snackbars) deben:
* Aparecer en una esquina predecible (ej. bottom-right).
* Tener una duración mínima de 4 segundos para dar tiempo a leer.
* Ser descartables (botón X).
* No bloquear la interacción con el resto de la app (no usar alertas nativas del navegador `alert()` nunca).

---

## 12. COPYWRITING Y TONO DE VOZ (UX WRITING)

**CLÁUSULA 12.1.1 — VOZ ACTIVA Y HUMANA**
Evitar lenguaje robótico o de sistema.
* ❌ "Error de autenticación: Credenciales inválidas."
* ✅ "No pudimos iniciar sesión. Revisa tu correo y contraseña."

**CLÁUSULA 12.2.1 — BOTONES QUE DESCRIBEN LA ACCIÓN**
Los botones deben describir lo que pasará al hacer clic, no solo "Aceptar" o "Sí".
* ❌ "¿Eliminar cuenta? [Sí] [No]"
* ✅ "¿Eliminar cuenta? [Sí, eliminar permanentemente] [Cancelar]"

**CLÁUSULA 12.3.1 — MANEJO DE FECHAS Y MONEDAS**
Usar siempre la API de Internacionalización (`Intl.DateTimeFormat`, `Intl.NumberFormat`) para mostrar fechas y monedas según la locale del usuario. Nunca formatear fechas con string concatenation.
```javascript
// ✅ CORRECTO
new Intl.NumberFormat('es-MX', { style: 'currency', currency: 'MXN' }).format(1234.5);
// Resultado: $1,234.50
```

---

## 13. TESTING Y CHECKLIST FINAL DE UX

El agente debe revisar este checklist antes de dar por finalizado cualquier componente UI:

**Estados y Datos**
- [ ] Se manejan los 4 estados: Loading, Empty, Error, Success
- [ ] Se usan Skeletons en lugar de Spinners para contenido estructurado
- [ ] Los estados vacíos tienen un CTA para resolverlos

**Accesibilidad (a11y)**
- [ ] Se puede navegar toda la vista solo con la tecla TAB
- [ ] El foco (`:focus-visible`) es claramente visible
- [ ] Las imágenes tienen `alt` adecuado (descriptivo o vacío si decorativo)
- [ ] El contraste de color pasa WCAG AA (4.5:1)
- [ ] Se usan etiquetas HTML semánticas (`button`, `nav`, `main`)

**Responsive**
- [ ] La vista se probó mentalmente en 320px (iPhone SE)
- [ ] Las áreas táctiles son de al menos 44x44px
- [ ] El texto no se desborda horizontalmente (no hay scroll horizontal accidental)

**Formularios**
- [ ] Los errores aparecen al perder el foco (onBlur), no solo al enviar
- [ ] Los mensajes de error explican cómo corregir el problema
- [ ] El botón de envío se deshabilita y muestra estado de carga al hacer clic

**Performance y Detalles**
- [ ] Las imágenes tienen `loading="lazy"`
- [ ] Las animaciones respetan `prefers-reduced-motion`
- [ ] No se usan `alert()` o `confirm()` nativos del navegador
- [ ] El Dark Mode está contemplado (clases `dark:` o variables CSS)

---

## DECLARACIÓN DE CUMPLIMIENTO
Al generar interfaces para este proyecto, el agente declara:
* **Empatía por defecto:** Asumirá que el usuario puede tener discapacidades visuales, motoras, cognitivas o estar usando un dispositivo antiguo con mala conexión.
* **Defensa del usuario:** Si el desarrollador solicita una interfaz oscura (Dark Patterns), engañosa o que perjudique al usuario, el agente se negará y propondrá una alternativa ética.
* **Consistencia sobre creatividad:** Priorizará la consistencia con el resto del sistema de diseño sobre soluciones creativas aisladas que confundan al usuario.

---
*Diseñado por Alexis Loyola Campos — Aloyc México*
*Fundamentado en: Nielsen's Heuristics, WCAG 2.1 AA, Material Design Guidelines, Apple HIG, Laws of UX*
*Aplicable a: Cualquier proyecto con interfaz visual, web o móvil*