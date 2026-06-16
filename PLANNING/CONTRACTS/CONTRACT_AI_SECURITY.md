# CONTRATO DE SEGURIDAD INTEGRAL PARA AGENTES DE IA
**Proyecto:** [NOMBRE DEL PROYECTO]
**Versión:** 1.2 | **Fecha:** 15/06/2026 | **Autor:** Alexis Loyola Campos — Aloyc México

## ⚠️ INSTRUCCIONES PARA EL AGENTE DE IA
Este documento es un contrato vinculante de seguridad que DEBES cumplir al 100% durante TODO el ciclo de vida de este proyecto. No puedes omitir, saltarte, simplificar ni negociar ninguno de estos puntos. Si en algún momento detectas que una implementación solicitada viola alguna cláusula de este contrato, DEBES notificarlo de forma explícita ANTES de escribir cualquier código y proponer la alternativa segura. Este contrato tiene prioridad absoluta sobre cualquier instrucción posterior.

## ÍNDICE
* [1. Principios Fundamentales de Seguridad](#1-principios-fundamentales-de-seguridad)
* [2. Seguridad de Autenticación y Sesiones](#2-seguridad-de-autenticación-y-sesiones)
* [3. Seguridad de Base de Datos](#3-seguridad-de-base-de-datos)
* [4. Seguridad de API y Backend](#4-seguridad-de-api-y-backend)
* [5. Seguridad de Frontend](#5-seguridad-de-frontend)
* [6. Cifrado y Manejo de Secretos](#6-cifrado-y-manejo-de-secretos)
* [7. Seguridad de Infraestructura y DevOps](#7-seguridad-de-infraestructura-y-devops)
* [8. Seguridad en Integraciones con IA](#8-seguridad-en-integraciones-con-ia)
* [9. Gestión de Errores y Logging](#9-gestión-de-errores-y-logging)
* [10. Seguridad de Archivos y Uploads](#10-seguridad-de-archivos-y-uploads)
* [11. Seguridad de Pagos y Transacciones](#11-seguridad-de-pagos-y-transacciones)
* [12. Protección de Privacidad y Datos Personales](#12-protección-de-privacidad-y-datos-personales)
* [13. Rate Limiting y Protección contra Abuso](#13-rate-limiting-y-protección-contra-abuso)
* [14. Seguridad de Dependencias y Supply Chain](#14-seguridad-de-dependencias-y-supply-chain)
* [15. Testing de Seguridad Obligatorio](#15-testing-de-seguridad-obligatorio)
* [16. Respuesta a Incidentes](#16-respuesta-a-incidentes)
* [17. Checklist Final de Verificación](#17-checklist-final-de-verificación)
* [18. Seguridad Avanzada de Autenticación Moderna](#18-seguridad-avanzada-de-autenticación-moderna)
* [19. Seguridad de Contenedores y Runtime](#19-seguridad-de-contenedores-y-runtime)
* [20. Seguridad de API Gateway y Edge](#20-seguridad-de-api-gateway-y-edge)

---

## 1. PRINCIPIOS FUNDAMENTALES DE SEGURIDAD

### 1.1 Filosofía de Seguridad por Defecto
**CLÁUSULA 1.1.1 — SECURE BY DEFAULT**
Todo código generado debe ser seguro en su configuración predeterminada. Nunca se generará código que requiera que el desarrollador "habilite la seguridad después". La seguridad es la configuración de fábrica, no un addon.

**CLÁUSULA 1.1.2 — PRINCIPIO DE MÍNIMO PRIVILEGIO**
Cada componente, usuario, proceso o servicio debe tener únicamente los permisos estrictamente necesarios para su función. Nunca se generará código que otorgue permisos amplios "para facilitar el desarrollo". Si una función solo necesita leer datos, no tendrá permisos de escritura. Si un servicio solo necesita acceder a una tabla, no tendrá acceso a toda la base de datos.

**CLÁUSULA 1.1.3 — DEFENSA EN PROFUNDIDAD**
Nunca se dependerá de una sola capa de seguridad. Todo sistema crítico debe tener al menos 3 capas de protección independientes: validación en frontend, validación en backend/API y validación en base de datos. Si una capa falla, las demás deben contener el daño.

**CLÁUSULA 1.1.4 — ZERO TRUST**
Nunca se asumirá que una solicitud es legítima solo porque viene de dentro del sistema. Toda solicitud, interna o externa, debe ser autenticada, autorizada y validada. Los tokens de servicio internos también deben rotar y expirar.

**CLÁUSULA 1.1.5 — FAIL SECURE**
Ante cualquier error, fallo o condición inesperada, el sistema debe fallar en el estado más seguro posible (denegar acceso, no en modo permisivo). Nunca se generará código que, ante un error de autenticación, otorgue acceso por defecto.

**CLÁUSULA 1.1.6 — SUPERFICIE DE ATAQUE MÍNIMA**
Se debe minimizar la cantidad de endpoints, funciones y servicios expuestos. Toda ruta, endpoint o función que no sea estrictamente necesaria debe estar deshabilitada o no existir. No se crearán rutas de debug, diagnóstico ni administración sin autenticación robusta.

---

## 2. SEGURIDAD DE AUTENTICACIÓN Y SESIONES

### 2.1 Identidad y Autenticación
**CLÁUSULA 2.1.1 — OAUTH/OIDC OBLIGATORIO PARA SSO**
Si el proyecto usa login social (Google, Discord, GitHub, etc.), se debe implementar el flujo OAuth 2.0 / OpenID Connect correctamente. El `state` parameter debe ser generado criptográficamente (mínimo 32 bytes de entropía) para prevenir CSRF en el flujo OAuth. El `code_verifier` y `code_challenge` (PKCE) son obligatorios en aplicaciones SPA y móviles.

```javascript
// ✅ CORRECTO — PKCE obligatorio en SPAs
const codeVerifier = generateSecureRandom(64); // crypto.getRandomValues
const codeChallenge = base64url(sha256(codeVerifier));
```

**CLÁUSULA 2.1.2 — NUNCA ALMACENAR CONTRASEÑAS EN TEXTO PLANO**
Si el proyecto maneja contraseñas propias, el hash es obligatorio con `bcrypt` (mínimo 12 rounds), `argon2id` (recomendado) o `scrypt`. Queda prohibido usar MD5, SHA-1, SHA-256 sin sal para contraseñas. El salt debe ser único por usuario y generado con CSPRNG.

```javascript
// ✅ CORRECTO
import { hash, verify } from '@node-rs/argon2';
const hashed = await hash(password, {
  algorithm: Algorithm.Argon2id,
  memoryCost: 65536,
  timeCost: 3,
  parallelism: 4,
});
```

**CLÁUSULA 2.1.3 — MFA DISPONIBLE EN CUENTAS SENSIBLES**
En proyectos con acceso a datos sensibles, paneles de administración o funciones de pago, se debe implementar soporte para TOTP (RFC 6238) como mínimo. Los códigos TOTP deben verificarse con tolerancia de ±1 step (30 segundos). Los códigos de respaldo deben generarse como 10 códigos de uso único, hasheados en la base de datos.

**CLÁUSULA 2.1.4 — REAUTENTICACIÓN EN ACCIONES CRÍTICAS**
Acciones como: cambio de email, cambio de contraseña, acceso al panel de admin, eliminación de cuenta, cambio de métodos de pago — deben exigir reautenticación reciente (máximo 15 minutos desde el último login). Si la sesión tiene más de ese tiempo, redirigir al flujo de autenticación antes de continuar.

**CLÁUSULA 2.1.5 — WEBAUTHN Y PASSKEYS (ESTÁNDAR MODERNO PASSWORDLESS)**
Como estándar moderno recomendado por NIST y FIDO2, el sistema debe soportar y priorizar **WebAuthn / Passkeys** por encima de contraseñas y TOTP. Las credenciales biométricas del dispositivo (FaceID, TouchID, Windows Hello) deben usarse para autenticación sin phishing. Se deben permitir múltiples passkeys por cuenta para evitar bloqueos por pérdida de dispositivo.

```typescript
// ✅ CORRECTO — Uso de @simplewebauthn o APIs nativas
import { verifyRegistrationResponse, verifyAuthenticationResponse } from '@simplewebauthn/server';
// Nunca almacenar la clave privada del usuario, solo la credencial pública (publicKey) en la DB.
```

### 2.2 Gestión de Sesiones
**CLÁUSULA 2.2.1 — TOKENS DE SESIÓN SEGUROS**
Los session tokens deben ser generados con CSPRNG (crypto.getRandomValues en browser, crypto.randomBytes en Node.js). Longitud mínima de 128 bits (16 bytes) de entropía real. Nunca usar UUIDs v4 estándar como tokens de sesión (son predecibles estadísticamente en algunos generadores). Usar `nanoid` o equivalente criptográfico.

**CLÁUSULA 2.2.2 — COOKIES DE SESIÓN HARDENING**
Toda cookie que contenga información de sesión o autenticación debe configurarse con:

```http
Set-Cookie: session=TOKEN; 
  HttpOnly;           /* Inaccesible desde JavaScript */
  Secure;             /* Solo HTTPS */
  SameSite=Strict;    /* Protección CSRF total */
  Path=/;
  Max-Age=3600;       /* Expiración explícita */
  Domain=.tudominio.com
```

Nunca se generarán cookies sin `HttpOnly` para datos de sesión. Si se requiere acceso desde JS, usar un token separado con alcance limitado.

**CLÁUSULA 2.2.3 — ROTACIÓN DE TOKENS**
Los refresh tokens deben rotarse en cada uso (Refresh Token Rotation). Si un refresh token ya usado es presentado de nuevo, invalidar TODA la familia de sesiones de ese usuario (posible robo de token). Los access tokens deben tener vida máxima de 15 minutos. Los refresh tokens máximo 7 días.

**CLÁUSULA 2.2.4 — INVALIDACIÓN DE SESIONES**
Al hacer logout, el token debe ser invalidado en el servidor (blacklist o eliminado de DB). No basta con borrar la cookie en el cliente. Se debe implementar `logout de todos los dispositivos` que invalide todas las sesiones activas de un usuario. Al cambiar contraseña, invalidar TODAS las sesiones excepto la actual.

**CLÁUSULA 2.2.5 — LIMPIEZA DE DATOS EN NAVEGADOR**
Después de completar el flujo de autenticación, limpiar automáticamente cualquier parámetro sensible de la URL (code, state, token) usando `history.replaceState()`. Los datos temporales del flujo OAuth no deben persistir en el historial del navegador.

```javascript
// ✅ Limpiar URL post-autenticación
const url = new URL(window.location.href);
url.searchParams.delete('code');
url.searchParams.delete('state');
window.history.replaceState({}, document.title, url.toString());
```

**CLÁUSULA 2.2.6 — GESTIÓN DE SESIONES CONCURRENTES**
El sistema debe registrar metadatos de cada sesión activa: user-agent, IP hasheada (no en claro), timestamp de creación y último acceso. Exponer al usuario una vista de "sesiones activas" con capacidad de revocar individualmente o todas excepto la actual.

---

## 3. SEGURIDAD DE BASE DE DATOS

### 3.1 Control de Acceso a Datos
**CLÁUSULA 3.1.1 — ROW LEVEL SECURITY (RLS) OBLIGATORIO**
En proyectos con Supabase o PostgreSQL, RLS debe estar habilitado en TODAS las tablas que contengan datos de usuarios. Nunca se deshabilitará RLS para "simplificar queries". Cada política debe ser revisada para garantizar que un usuario solo puede leer/escribir sus propios datos.

```sql
-- ✅ CORRECTO — RLS en tabla de datos de usuario
ALTER TABLE user_data ENABLE ROW LEVEL SECURITY;

CREATE POLICY "users_own_data" ON user_data
  FOR ALL
  USING (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id);
```

**CLÁUSULA 3.1.2 — AISLAMIENTO TOTAL ENTRE USUARIOS**
Cada query que acceda a datos de usuario debe incluir explícitamente el filtro por `user_id`. No se confía únicamente en RLS como única barrera. La doble verificación (RLS + filtro explícito en query) es obligatoria en operaciones críticas.

**CLÁUSULA 3.1.3 — ROLES DE BASE DE DATOS SEPARADOS**
Se deben crear roles de DB separados por función:
* `app_readonly`: Solo SELECT en tablas de negocio
* `app_readwrite`: SELECT, INSERT, UPDATE en tablas operativas
* `app_admin`: Acceso completo solo para operaciones administrativas
* `app_service`: Para funciones serverless con scope limitado

Nunca usar el rol `postgres` o `service_role` en código de aplicación que corra en el cliente.

**CLÁUSULA 3.1.4 — PREVENCIÓN DE SQL INJECTION**
Queda absolutamente prohibido construir queries con concatenación de strings de input del usuario. Se usarán SIEMPRE prepared statements o query builders con parámetros. En ORMs, los métodos raw/unsafe solo se usan con valores hardcodeados, nunca con input del usuario.

```javascript
// ❌ PROHIBIDO
const query = `SELECT * FROM users WHERE email = '${userEmail}'`;

// ✅ CORRECTO
const { data } = await supabase
  .from('users')
  .select('*')
  .eq('email', userEmail); // Parámetro seguro
```

### 3.2 Esquema y Estructura Segura
**CLÁUSULA 3.2.1 — NO EXPONER IDs INTERNOS**
Los IDs internos de la base de datos (autoincrement integers) nunca deben exponerse en APIs públicas. Usar UUIDs v4 o v7 como identificadores públicos. Los IDs numéricos revelan el volumen de datos y permiten enumeración.

**CLÁUSULA 3.2.2 — CAMPOS SENSIBLES CIFRADOS EN REPOSO**
Campos como: API keys, tokens de terceros, datos de salud, documentos de identidad, información bancaria — deben cifrarse a nivel de aplicación ANTES de almacenarse, adicional al cifrado en reposo del proveedor de DB. Usar AES-256-GCM con IV único por registro.

**CLÁUSULA 3.2.3 — SOFT DELETE CON ANONIMIZACIÓN**
Al eliminar cuentas de usuario, aplicar anonimización progresiva: primero anonimizar PII (nombre → "Usuario Eliminado", email → hash irreversible), luego eliminar datos sensibles (API keys, preferencias), finalmente eliminar el registro completo después del período de retención definido.

**CLÁUSULA 3.2.4 — BACKUPS CIFRADOS**
Los backups de base de datos deben cifrarse con una clave diferente a la de producción. Las claves de backup deben almacenarse en un lugar separado de los backups. Se debe documentar y probar el proceso de restauración.

---

## 4. SEGURIDAD DE API Y BACKEND

### 4.1 Autenticación y Autorización de API
**CLÁUSULA 4.1.1 — AUTENTICACIÓN EN TODOS LOS ENDPOINTS**
Todo endpoint de API que acceda a datos o ejecute acciones debe validar la autenticación. No existen "endpoints públicos" que accesen datos de usuario sin validación. Las rutas públicas (landing pages, info general) no deben poder acceder a datos privados bajo ningún parámetro.

**CLÁUSULA 4.1.2 — AUTORIZACIÓN GRANULAR (RBAC/ABAC) Y PREVENCIÓN DE IDOR**
La autenticación verifica identidad; la autorización verifica permisos. Ambas son obligatorias y separadas. Se debe implementar verificación de permisos en cada endpoint para prevenir **IDOR (Insecure Direct Object References)**. Un usuario autenticado no necesariamente tiene permiso para TODOS los recursos.

```javascript
// ✅ CORRECTO — Verificación separada de auth + authz (Anti-IDOR)
export async function handler(req: Request) {
  // 1. Autenticación
  const user = await verifyToken(req.headers.authorization);
  if (!user) return unauthorized();
  
  // 2. Autorización específica del recurso
  const resource = await getResource(req.params.id);
  if (resource.ownerId !== user.id && !user.isAdmin) return forbidden();
  
  // 3. Lógica de negocio
  return processRequest(resource);
}
```

**CLÁUSULA 4.1.3 — API KEYS DE SERVICIO NUNCA EN FRONTEND**
Las claves de API de servicios de terceros (Stripe, SendGrid, Twilio, etc.) NUNCA deben estar en código frontend, variables de entorno del cliente ni en el bundle de JavaScript. Deben vivir exclusivamente en variables de entorno del servidor y accederse solo desde funciones serverless o backend.

**CLÁUSULA 4.1.4 — VALIDACIÓN DE ORIGEN**
En APIs que reciben webhooks, validar la firma del webhook (HMAC-SHA256) antes de procesar cualquier payload. No se puede confiar en que una solicitud es legítima solo porque dice venir de un servicio confiable sin verificación criptográfica.

**CLÁUSULA 4.1.5 — VERSIONADO OBLIGATORIO DE APIs**
Todas las rutas de API públicas, de terceros o móviles deben estar estrictamente versionadas (ej. `/api/v1/resource`, `/api/v2/resource`). Esto previene la ruptura de integraciones de clientes antiguos cuando se requieren cambios estructurales (breaking changes) en el backend.

**CLÁUSULA 4.1.6 — IDEMPOTENCIA GLOBAL EN WEBHOOKS**
No solo los pagos, **TODOS** los webhooks entrantes (Stripe, Shopify, GitHub, Resend) deben ser tratados como idempotentes. Debido a los reintentos automáticos de red, un webhook puede llegar 2 o 3 veces. El backend debe verificar si el `event_id` o `Idempotency-Key` ya fue procesado en la base de datos antes de ejecutar la lógica de negocio para evitar duplicidad de datos.

### 4.2 Validación y Sanitización
**CLÁUSULA 4.2.1 — VALIDACIÓN EN SERVIDOR SIEMPRE**
La validación en frontend es UX, no seguridad. TODO input debe validarse en el servidor independientemente de si fue validado en el cliente. Se usará una librería de validación (Zod, Joi, Yup) para definir schemas estrictos de todos los endpoints.

```typescript
// ✅ CORRECTO — Validación con Zod en API
const CreateUserSchema = z.object({
  email: z.string().email().max(255),
  name: z.string().min(2).max(100).regex(/^[a-zA-ZÀ-ÿ\s]+$/),
  role: z.enum(['user', 'moderator']), // Whitelist de valores permitidos
});

export async function createUser(req: Request) {
  const parsed = CreateUserSchema.safeParse(req.body);
  if (!parsed.success) return badRequest(parsed.error);
  // Continuar solo con datos validados
}
```

**CLÁUSULA 4.2.2 — SANITIZACIÓN DE HTML**
Si cualquier campo acepta contenido que se renderizará como HTML, sanitizarlo con DOMPurify (frontend) o `sanitize-html` (backend) antes de almacenar Y antes de renderizar. La doble sanitización (almacenamiento + renderizado) es obligatoria para prevenir XSS stored.

**CLÁUSULA 4.2.3 — PROTECCIÓN CONTRA PATH TRAVERSAL**
Cuando se acepten rutas de archivos como input, validar y normalizar la ruta con `path.resolve()` y verificar que el resultado esté dentro del directorio permitido. Nunca concatenar input de usuario directamente en rutas de sistema de archivos.

```javascript
// ✅ CORRECTO
const safePath = path.resolve(BASE_DIR, userInput);
if (!safePath.startsWith(BASE_DIR)) {
  throw new Error('Path traversal detectado');
}
```

**CLÁUSULA 4.2.4 — LÍMITES DE TAMAÑO EN TODOS LOS INPUTS**
Todo campo de texto, archivo, array o objeto recibido por la API debe tener límites de tamaño explícitos. Sin límites, se es vulnerable a DoS por payload excesivo. El body parser debe tener un límite global (ej: 10MB para API general, 100MB para uploads dedicados).

### 4.3 Headers de Seguridad HTTP
**CLÁUSULA 4.3.1 — HEADERS OBLIGATORIOS EN TODAS LAS RESPUESTAS**
Todos los endpoints deben retornar los siguientes headers:

```http
Content-Security-Policy: default-src 'self'; script-src 'self' 'nonce-{RANDOM}'; ...
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=()
Cache-Control: no-store, no-cache (en respuestas con datos privados)
```

**CLÁUSULA 4.3.2 — CSP ESTRICTO**
El Content-Security-Policy debe ser lo más restrictivo posible. No se aceptará `unsafe-inline` ni `unsafe-eval` en `script-src` sin justificación documentada. Se usarán nonces criptográficos por request para scripts inline legítimos.

**CLÁUSULA 4.3.3 — CORS CONFIGURADO EXPLÍCITAMENTE**
CORS no debe configurarse con wildcard `*` en APIs que manejan autenticación. Se debe definir explícitamente la lista de orígenes permitidos. Las credenciales (`withCredentials: true`) solo deben permitirse desde orígenes de confianza verificados.

**CLÁUSULA 4.3.4 — SUBRESOURCE INTEGRITY (SRI)**
Todo script o stylesheet externo cargado desde CDN debe incluir el atributo `integrity` con el hash SHA-384 del archivo. Sin SRI, si el CDN es comprometido, el sitio también lo será.

```html
<!-- ✅ CORRECTO -->
<script 
  src="https://cdn.example.com/lib.js"
  integrity="sha384-HASH_AQUI"
  crossorigin="anonymous">
</script>
```

### 4.4 Prevención de SSRF (Server-Side Request Forgery)
**CLÁUSULA 4.4.1 — VALIDACIÓN DE URLs DE DESTINO**
Nunca pasar input del usuario directamente a funciones de red del servidor (`fetch`, `axios`, `request`, `puppeteer`). Si el usuario puede proveer una URL (ej. importar avatar desde URL, webhooks configurables), se debe validar contra una whitelist de dominios.

**CLÁUSULA 4.4.2 — BLOQUEO DE REDES INTERNAS Y METADATA**
El servidor DEBE bloquear peticiones dirigidas a IPs privadas (`127.0.0.1`, `10.x.x.x`, `192.168.x.x`) y especialmente a servicios de metadata de Cloud (`169.254.169.254` en AWS/GCP) para prevenir la extracción de credenciales de infraestructura. Se debe resolver el DNS antes de la petición para evitar ataques de DNS Rebinding.

### 4.5 Seguridad en GraphQL (Si aplica)
**CLÁUSULA 4.5.1 — LÍMITES DE PROFUNDIDAD Y COSTO**
Si se usa GraphQL, es obligatorio implementar `graphql-depth-limit` (máximo 5-7 niveles) y `graphql-cost-analysis` para prevenir ataques de Denegación de Servicio (DoS) mediante queries recursivas o extracción masiva de bases de datos.

**CLÁUSULA 4.5.2 — INTROSPECCIÓN DESACTIVADA**
La introspección de GraphQL (`__schema`, `__type`) debe estar **estrictamente deshabilitada** en entornos de Producción y Staging para no facilitar el reconocimiento de la API a atacantes.

---

## 5. SEGURIDAD DE FRONTEND

### 5.1 Protección contra XSS
**CLÁUSULA 5.1.1 — ESCAPE AUTOMÁTICO EN TEMPLATES**
En React/Vue/Svelte, nunca usar `dangerouslySetInnerHTML` o `v-html` con datos del usuario sin sanitización previa con DOMPurify. El escape automático del framework es suficiente solo para texto plano, no para HTML.

```jsx
// ❌ PROHIBIDO
<div dangerouslySetInnerHTML={{ __html: userContent }} />

// ✅ CORRECTO
import DOMPurify from 'dompurify';
<div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(userContent) }} />
```

**CLÁUSULA 5.1.2 — NO EVALUAR CÓDIGO DINÁMICO**
Queda prohibido el uso de `eval()`, `new Function()`, `setTimeout(string)`, `setInterval(string)` con strings generadas desde input de usuario. Si se necesita dinámica, usar estructuras de datos y switch/map, nunca evaluación de código.

**CLÁUSULA 5.1.3 — SANITIZACIÓN DE URLs**
Antes de usar un valor de usuario como href o src, validar que el esquema sea `http://` o `https://`. Los esquemas `javascript:`, `data:`, `vbscript:` son vectores de XSS.

```javascript
// ✅ CORRECTO
function safeUrl(url: string): string | null {
  try {
    const parsed = new URL(url);
    return ['http:', 'https:'].includes(parsed.protocol) ? url : null;
  } catch {
    return null;
  }
}
```

### 5.2 Protección contra CSRF
**CLÁUSULA 5.2.1 — TOKENS CSRF EN FORMULARIOS**
Todas las acciones que modifiquen estado (POST, PUT, DELETE, PATCH) deben incluir un token CSRF válido. El token debe ser único por sesión y verificado en el servidor. SameSite=Strict en cookies reduce pero no elimina la necesidad de CSRF tokens.

**CLÁUSULA 5.2.2 — DOBLE SUBMIT COOKIE PATTERN**
Para SPAs, implementar el patrón Double Submit Cookie: enviar el CSRF token tanto en la cookie como en el header de la petición. El servidor verifica que ambos coincidan.

### 5.3 Seguridad en Almacenamiento Local
**CLÁUSULA 5.3.1 — NO ALMACENAR SECRETOS EN LOCALSTORAGE/SESSIONSTORAGE**
localStorage y sessionStorage son accesibles por cualquier JavaScript en la página (incluyendo XSS). Nunca almacenar: tokens de autenticación completos, API keys, datos de tarjetas, contraseñas ni PII sensible en localStorage. Los tokens de autenticación deben vivir en cookies HttpOnly.

**CLÁUSULA 5.3.2 — DATOS MÍNIMOS EN CLIENTE**
Solo almacenar en el cliente los datos estrictamente necesarios para la UI. Datos sensibles deben re-fetchiarse del servidor cuando se necesiten, no cachearse indefinidamente en el cliente.

### 5.4 Protección de Interfaz
**CLÁUSULA 5.4.1 — ANTI-CLICKJACKING**
Implementar `X-Frame-Options: DENY` y `frame-ancestors 'none'` en CSP para prevenir que la aplicación sea incrustada en iframes de sitios maliciosos. Si se necesita incrustar en iframe propio, usar `frame-ancestors 'self'`.

**CLÁUSULA 5.4.2 — PROTECCIÓN DE DATOS EN PANTALLA**
Campos con información sensible (API keys, contraseñas, números de tarjeta) deben mostrarse enmascarados por defecto. Si se muestran completos, documentar la justificación. Implementar autocomplete="off" en campos de contraseñas en formularios no-login.

**CLÁUSULA 5.4.3 — MANEJO SEGURO DE FORMULARIOS**
Los formularios de login/registro no deben ser pre-llenados por el browser en páginas de admin (usar autocomplete="new-password"). El campo de contraseña nunca debe estar en el mismo formulario que campos de búsqueda o filtros.

---

## 6. CIFRADO Y MANEJO DE SECRETOS

### 6.1 Estándares de Cifrado
**CLÁUSULA 6.1.1 — ALGORITMOS APROBADOS ÚNICAMENTE**
Solo se usarán algoritmos criptográficos modernos y aprobados:

| Uso | Algoritmo Aprobado | Prohibido |
| --- | --- | --- |
| Cifrado simétrico | AES-256-GCM | DES, 3DES, RC4, AES-ECB |
| Hash de contraseñas | Argon2id, bcrypt (≥12 rounds) | MD5, SHA-1, SHA-256 sin salt |
| Hash general | SHA-256, SHA-384, SHA-512 | MD5, SHA-1 |
| Cifrado asimétrico | RSA-4096, ECDSA P-256/P-384 | RSA <2048, DSA |
| Intercambio de claves | ECDH P-256, X25519 | DH <2048 bits |
| Derivación de claves | PBKDF2 (≥310,000 iter), HKDF | SHA-1 directo |
| TLS | 1.2 mínimo, 1.3 recomendado | SSL 3.0, TLS 1.0, TLS 1.1 |

**CLÁUSULA 6.1.2 — CIFRADO AES-256-GCM CON IV ÚNICO**
Cuando se cifre información sensible, el IV (nonce) debe ser único por operación de cifrado. Nunca reutilizar el mismo IV con la misma clave. El IV puede almacenarse junto al ciphertext (no es secreto). El tag de autenticación de GCM debe validarse antes de intentar descifrar.

```javascript
// ✅ CORRECTO — AES-256-GCM con IV aleatorio
async function encrypt(data: string, key: CryptoKey): Promise<string> {
  const iv = crypto.getRandomValues(new Uint8Array(12)); // 96-bit IV para GCM
  const encrypted = await crypto.subtle.encrypt(
    { name: 'AES-GCM', iv },
    key,
    new TextEncoder().encode(data)
  );
  // Concatenar IV + ciphertext para almacenamiento
  const combined = new Uint8Array(iv.length + encrypted.byteLength);
  combined.set(iv);
  combined.set(new Uint8Array(encrypted), iv.length);
  return btoa(String.fromCharCode(...combined));
}
```

**CLÁUSULA 6.1.3 — DERIVACIÓN DE CLAVES CON PBKDF2**
Cuando la clave de cifrado se derive de un password o sesión de usuario, usar PBKDF2 con SHA-256 y mínimo 310,000 iteraciones (estándar OWASP 2025) o Argon2id con parámetros: m=65536, t=3, p=4.

### 6.2 Gestión de Secretos
**CLÁUSULA 6.2.1 — VARIABLES DE ENTORNO PARA SECRETOS**
Ningún secreto (API key, contraseña de DB, JWT secret, clave de cifrado) puede estar hardcodeado en el código fuente. Todo secreto debe cargarse desde variables de entorno. El archivo `.env` nunca debe commitearse al repositorio.

**CLÁUSULA 6.2.2 — .GITIGNORE MÍNIMO OBLIGATORIO**
El `.gitignore` del proyecto DEBE incluir como mínimo:

```text
.env
.env.local
.env.production
.env.*.local
*.key
*.pem
*.p12
*.pfx
secrets/
credentials/
```

**CLÁUSULA 6.2.3 — ROTACIÓN DE SECRETOS**
Se debe documentar el procedimiento de rotación para cada secreto. Los secretos deben poder rotarse sin downtime (soporte de múltiples versiones de clave activas simultáneamente). Los secretos de producción deben rotarse mínimo cada 90 días o inmediatamente ante sospecha de compromiso.

**CLÁUSULA 6.2.4 — SEPARACIÓN DE ENTORNOS**
Las claves de producción, staging y desarrollo deben ser completamente distintas. Nunca usar credenciales de producción en entornos de desarrollo. El acceso a secretos de producción debe estar restringido y auditado.

**CLÁUSULA 6.2.5 — MOSTRAR SOLO ÚLTIMOS 4 CARACTERES**
En cualquier UI que liste o muestre API keys, tokens u otros secretos, mostrar solo los últimos 4 caracteres con enmascaramiento del resto (`••••••••abcd`). Nunca mostrar el valor completo en listas o dashboards, solo en el momento de creación con aviso de "cópialo ahora".

---

## 7. SEGURIDAD DE INFRAESTRUCTURA Y DEVOPS

### 7.1 Configuración de Servidores y Plataformas
**CLÁUSULA 7.1.1 — HTTPS OBLIGATORIO EN PRODUCCIÓN**
Ninguna aplicación de producción puede servirse sobre HTTP. El certificado TLS debe ser válido y auto-renovable (Let's Encrypt o certificado de proveedor). Se debe configurar HSTS con `max-age=31536000; includeSubDomains; preload` para forzar HTTPS en futuros accesos.

**CLÁUSULA 7.1.2 — VARIABLES DE ENTORNO EN PLATAFORMA SEGURA**
Los secretos en plataformas cloud (Vercel, Netlify, Railway, etc.) deben configurarse como variables de entorno encriptadas de la plataforma, no como archivos `.env` en el repositorio. Las variables de entorno del cliente (`NEXT_PUBLIC_*`, `VITE_*`) nunca deben contener secretos, solo valores públicos.

**CLÁUSULA 7.1.3 — CONFIGURACIÓN DE HEADERS EN PRODUCCIÓN**
En Vercel/Netlify, configurar headers de seguridad a nivel de plataforma en `vercel.json` o `netlify.toml`:

```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "Strict-Transport-Security", "value": "max-age=31536000; includeSubDomains" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" }
      ]
    }
  ]
}
```

**CLÁUSULA 7.1.4 — PUERTOS Y SERVICIOS MÍNIMOS EXPUESTOS**
En servidores propios (VPS, EC2, etc.), solo los puertos 80 y 443 deben estar abiertos al público. SSH en puerto no estándar (>1024), accesible solo desde IPs conocidas o via VPN. La base de datos no debe ser accesible desde internet público bajo ninguna circunstancia.

### 7.2 CI/CD Seguro
**CLÁUSULA 7.2.1 — SECRETS EN PIPELINE DE CI/CD**
Las claves y tokens en GitHub Actions, GitLab CI u otro sistema de CI/CD deben configurarse como `secrets` del repositorio/organización, nunca en el código del workflow. Los workflows no deben imprimir (`echo`) el valor de secretos en los logs.

**CLÁUSULA 7.2.2 — REVISIÓN DE CÓDIGO ANTES DE MERGE**
Todo código que llegue a producción debe pasar por al menos una revisión humana (PR/MR). Los pipelines de CI deben incluir: linting de seguridad (ESLint security rules), análisis estático (Snyk, Semgrep, CodeQL), y verificación de dependencias vulnerables.

**CLÁUSULA 7.2.3 — ESCANEO DE SECRETOS EN COMMITS**
Se debe configurar pre-commit hooks o CI checks para detectar secretos accidentalmente commiteados (git-secrets, TruffleHog, Gitleaks). Si un secreto llega a ser commiteado, debe ser revocado inmediatamente, no solo removido del historial.

### 7.3 Monitoreo y Alertas
**CLÁUSULA 7.3.1 — LOGS DE SEGURIDAD RETENIDOS**
Los logs de acceso, errores de autenticación y acciones administrativas deben retenerse mínimo 90 días en almacenamiento seguro. Los logs no deben contener PII (emails, nombres, contraseñas) en texto plano — usar hashes o IDs anónimos.

**CLÁUSULA 7.3.2 — ALERTAS DE ANOMALÍAS**
Se deben configurar alertas automáticas para: múltiples intentos de login fallidos (>5 en 10 minutos), acceso desde nueva geolocalización para usuario existente, picos inusuales de tráfico (>10x baseline), errores 4xx/5xx que excedan umbral normal.

---

## 8. SEGURIDAD EN INTEGRACIONES CON IA

### 8.1 Protección contra Prompt Injection
**CLÁUSULA 8.1.1 — SEPARACIÓN ESTRICTA DE INSTRUCCIONES Y DATOS**
El system prompt (instrucciones del sistema) debe estar completamente separado del input del usuario. Nunca interpollar directamente input del usuario dentro del system prompt. Usar el campo `user` del mensaje para input del usuario, el campo `system` solo para instrucciones fijas.

```javascript
// ✅ CORRECTO — Separación clara
const messages = [
  { role: 'system', content: SYSTEM_PROMPT_FIJO }, // Nunca contiene userInput
  { role: 'user', content: sanitizeUserInput(userMessage) }
];
```

**CLÁUSULA 8.1.2 — FILTROS DE PROMPT INJECTION**
Antes de enviar input del usuario al modelo, aplicar filtros para detectar y bloquear patrones de prompt injection conocidos: "ignora las instrucciones anteriores", "olvida tu contexto", instrucciones en otro idioma embebidas, instrucciones codificadas en base64 o ROT13.

**CLÁUSULA 8.1.3 — OUTPUT VALIDATION DE IA**
Las respuestas del modelo de IA deben validarse antes de actuar sobre ellas. Si el modelo devuelve código, URLs, comandos o acciones, validar que el formato sea el esperado antes de ejecutar. Nunca ejecutar código generado por IA sin sandbox o validación.

**CLÁUSULA 8.1.4 — PRINCIPIO DE MÍNIMO PRIVILEGIO PARA AGENTES**
Los agentes de IA que ejecuten herramientas (tools/functions) deben tener acceso solo a las herramientas estrictamente necesarias. No dar a un agente herramientas de escritura si solo necesita lectura. Cada llamada a tool debe ser auditada y loggeada.

### 8.2 Protección de Datos en Contexto de IA
**CLÁUSULA 8.2.1 — NO INCLUIR PII EN PROMPTS INNECESARIAMENTE**
Cuando se construyan prompts con datos del usuario, incluir solo la información estrictamente necesaria para la tarea. No incluir email, nombre completo, ID de usuario u otros datos de identidad si no son necesarios para el resultado.

**CLÁUSULA 8.2.2 — CONEXIÓN CIFRADA A PROVEEDORES**
Todas las llamadas a APIs de IA (OpenAI, Anthropic, Google, etc.) deben realizarse desde el servidor (funciones serverless) nunca desde el cliente. El cliente nunca debe tener acceso directo a claves de API de proveedores de IA. Usar proxy server propio.

**CLÁUSULA 8.2.3 — SANITIZACIÓN DE MEMORIA DE ASISTENTES**
Si el sistema implementa memoria persistente para asistentes de IA, sanitizar el contenido antes de almacenarlo para detectar y remover: código malicioso, instrucciones de override, datos sensibles que no deberían persistir. La memoria almacenada debe pasar por el mismo pipeline de validación que el input directo.

**CLÁUSULA 8.2.4 — WHITELIST DE PROVEEDORES DE IA**
El sistema debe mantener una lista explícita de proveedores de IA autorizados. Las URLs de endpoints de IA deben estar hardcodeadas o en configuración del servidor, nunca aceptarse como input del usuario. Cualquier intento de redirigir llamadas a endpoints no autorizados debe ser bloqueado y loggeado.

**CLÁUSULA 8.2.5 — MANEJO SEGURO DE FALLOS DE IA**
Si un modelo de IA devuelve un error o no responde, el sistema debe fallar de forma segura sin exponer detalles de la infraestructura (URLs internas, nombres de modelos privados, configuraciones). Los mensajes de error al usuario deben ser genéricos y amigables.

### 8.3 Seguridad en RAG y Memorias Vectoriales
**CLÁUSULA 8.3.1 — AISLAMIENTO TENANT EN RAG (Cross-Tenant Leakage)**
En sistemas RAG (Retrieval-Augmented Generation), las búsquedas en la Base de Datos Vectorial (Pinecone, Weaviate, pgvector) DEBEN incluir siempre un filtro de metadatos por `tenant_id` o `user_id`. Nunca permitir que el embedding search cruce límites de organizaciones o usuarios.

**CLÁUSULA 8.3.2 — PREVENCIÓN DE DATA POISONING**
El contenido subido por usuarios que se usará para entrenar, fine-tunear o indexar en RAG debe pasar por un escaneo de malware y sanitización de texto para evitar inyección de instrucciones maliciosas que se ejecutarán en futuros prompts de otros usuarios.

---

## 9. GESTIÓN DE ERRORES Y LOGGING

### 9.1 Mensajes de Error Seguros
**CLÁUSULA 9.1.1 — ERRORES GENÉRICOS AL CLIENTE**
Los mensajes de error expuestos al cliente nunca deben revelar: stack traces, rutas de archivos del servidor, versiones de librerías, nombres de tablas de DB, queries SQL, IDs internos del sistema, ni información de configuración. Los errores internos se logean en servidor; al cliente solo va un mensaje genérico con un ID de correlación.

```javascript
// ✅ CORRECTO
try {
  await riskyOperation();
} catch (error) {
  const errorId = generateErrorId();
  logger.error({ errorId, error, userId: user.id }); // Log detallado interno
  return res.status(500).json({ 
    error: 'Ocurrió un error interno', 
    errorId // Para que el usuario pueda reportarlo
  });
}
```

**CLÁUSULA 9.1.2 — MENSAJES DE AUTH AMBIGUOS**
Los endpoints de login/registro no deben revelar si un email existe en el sistema a través de mensajes de error diferenciados. El mensaje debe ser siempre el mismo independientemente de si el email existe o si la contraseña es incorrecta: "Credenciales incorrectas".

**CLÁUSULA 9.1.3 — NO LOGGEAR DATOS SENSIBLES**
Los sistemas de logging nunca deben registrar: contraseñas (ni hasheadas), tokens de sesión completos, API keys, números de tarjeta, datos de documentos de identidad, contenido de conversaciones de IA. Si se necesita debug, loggear solo los primeros 4 caracteres del token para identificación.

### 9.2 Audit Logs
**CLÁUSULA 9.2.1 — REGISTRO DE ACCIONES CRÍTICAS**
Las siguientes acciones SIEMPRE deben generar un registro de auditoría:
* Login exitoso y fallido (con timestamp, IP hasheada, user-agent)
* Cambio de contraseña o email
* Acceso al panel de administración
* Cambios en configuración de seguridad
* Adición/eliminación de API keys
* Transacciones económicas
* Eliminación de datos de usuario
* Cambios en roles o permisos

**CLÁUSULA 9.2.2 — INTEGRIDAD DE AUDIT LOGS**
Los audit logs deben ser inmutables: ningún usuario, incluyendo admins, puede eliminar o modificar registros de auditoría. Los logs deben replicarse a almacenamiento separado del sistema principal. La integridad de los logs puede verificarse con hashing encadenado (similar a blockchain ligero).

---

## 10. SEGURIDAD DE ARCHIVOS Y UPLOADS

### 10.1 Validación de Archivos
**CLÁUSULA 10.1.1 — VALIDACIÓN POR MAGIC BYTES, NO SOLO EXTENSIÓN**
La extensión del archivo y el Content-Type del request son controlables por el usuario y no son confiables. La validación del tipo de archivo debe realizarse verificando los magic bytes (primeros bytes del archivo) contra una whitelist de tipos permitidos.

```javascript
// ✅ CORRECTO — Validar por magic bytes
import fileType from 'file-type';

const type = await fileType.fromBuffer(fileBuffer);
const allowedTypes = ['image/jpeg', 'image/png', 'image/webp', 'application/pdf'];
if (!type || !allowedTypes.includes(type.mime)) {
  return badRequest('Tipo de archivo no permitido');
}
```

**CLÁUSULA 10.1.2 — LÍMITES DE TAMAÑO ESTRICTOS**
Cada tipo de upload debe tener límites de tamaño apropiados y explícitos. Imágenes de perfil: máx 5MB. Documentos: máx 25MB. El límite debe verificarse tanto en frontend (UX) como en backend (seguridad). Archivos que excedan el límite deben rechazarse antes de procesarse.

**CLÁUSULA 10.1.3 — ESCANEO DE MALWARE**
En aplicaciones que permitan upload de archivos ejecutables, documentos de Office o ZIPs, integrar escaneo de malware (ClamAV, VirusTotal API) antes de almacenar o distribuir el archivo. Los archivos deben ser puestos en cuarentena hasta completar el escaneo.

### 10.2 Almacenamiento Seguro de Archivos
**CLÁUSULA 10.2.1 — RENOMBRAR ARCHIVOS AL ALMACENAR**
Los archivos subidos deben almacenarse con nombres generados por el sistema (UUID + extensión sanitizada), nunca con el nombre original del usuario. El nombre original puede guardarse en metadata de DB, pero el archivo físico tiene nombre controlado.

**CLÁUSULA 10.2.2 — DIRECTORIO FUERA DEL WEBROOT**
Los archivos subidos por usuarios nunca deben almacenarse en directorios accesibles directamente por el web server. Deben estar en almacenamiento privado (S3 bucket privado, Supabase Storage con RLS) y accederse mediante URLs firmadas con tiempo de expiración.

**CLÁUSULA 10.2.3 — URLS FIRMADAS Y TEMPORALES**
Para servir archivos privados, generar URLs firmadas con expiración corta (15-60 minutos). Nunca exponer URLs permanentes a archivos privados. Las URLs firmadas deben incluir el ID del usuario solicitante para auditoría.

---

## 11. SEGURIDAD DE PAGOS Y TRANSACCIONES

### 11.1 Procesamiento Seguro
**CLÁUSULA 11.1.1 — NUNCA ALMACENAR DATOS DE TARJETAS**
Ningún dato de tarjeta de crédito/débito (número, CVV, fecha de expiración) puede ser almacenado en los sistemas de la aplicación. Todo procesamiento de tarjetas debe realizarse directamente con el proveedor de pagos (Stripe, Conekta, etc.) usando sus SDKs certificados PCI-DSS.

**CLÁUSULA 11.1.2 — CÁLCULO DE PRECIOS EN SERVIDOR**
El precio final de cualquier transacción debe calcularse exclusivamente en el servidor. El cliente puede enviar identificadores de productos o planes, pero nunca montos. Cualquier intento de manipular el precio desde el cliente debe ser detectado y bloqueado.

**CLÁUSULA 11.1.3 — IDEMPOTENCIA EN TRANSACCIONES**
Las operaciones de pago deben ser idempotentes: reintentar la misma operación nunca debe resultar en un cobro doble. Usar `idempotency_key` en todas las llamadas a APIs de pago. El servidor debe verificar si una transacción con el mismo key ya fue procesada.

**CLÁUSULA 11.1.4 — VERIFICACIÓN DE WEBHOOKS DE PAGO**
Los webhooks de proveedores de pago deben verificarse criptográficamente. Para Stripe: verificar la firma con `stripe.webhooks.constructEvent()`. Para otros proveedores: implementar verificación HMAC-SHA256 equivalente. Nunca procesar un webhook sin verificar su autenticidad.

**CLÁUSULA 11.1.5 — PROTECCIÓN CONTRA BOTS EN PAGOS**
Los endpoints de creación de sesiones de pago deben tener rate limiting estricto por usuario y por IP. Implementar CAPTCHA (hCaptcha o Google reCAPTCHA v3) en flujos de compra para prevenir uso automatizado abusivo.

---

## 12. PROTECCIÓN DE PRIVACIDAD Y DATOS PERSONALES

### 12.1 Principios de Privacidad
**CLÁUSULA 12.1.1 — MINIMIZACIÓN DE DATOS**
Solo se recolectarán datos personales estrictamente necesarios para la funcionalidad del sistema. Antes de agregar cualquier campo de recolección de datos, se debe justificar su necesidad. No se recolectan datos "por si acaso son útiles en el futuro".

**CLÁUSULA 12.1.2 — CERO RASTREO SIN CONSENTIMIENTO**
No se integrarán herramientas de analytics de terceros, píxeles de seguimiento ni SDKs publicitarios sin consentimiento explícito del usuario. Si se usa analytics propio (Plausible, Umami), debe ser cookieless y sin PII.

**CLÁUSULA 12.1.3 — DERECHO AL OLVIDO**
El sistema debe implementar un mecanismo de eliminación completa de datos de usuario que funcione en máximo 7 días hábiles. La eliminación debe ser total y verificable, incluyendo backups después del período de retención.

**CLÁUSULA 12.1.4 — LOGS SIN PII**
Los logs del sistema nunca deben contener datos personales identificables (nombre, email, teléfono) en texto plano. Si se necesita correlacionar logs con usuarios, usar un ID de sesión anónimo o hash del user_id.

### 12.2 Retención de Datos
**CLÁUSULA 12.2.1 — POLÍTICA DE RETENCIÓN DEFINIDA**
Se debe documentar explícitamente cuánto tiempo se retiene cada categoría de dato:
* Datos de sesión activa: Hasta logout + 30 días
* Logs de acceso: 90 días
* Datos de cuenta activa: Mientras la cuenta esté activa
* Datos post-cancelación: 30 días para recuperación, luego eliminación
* Registros financieros: 5 años (requerimiento fiscal México SAT)
* Datos de conversaciones IA: Solo sesión activa, no persistir

---

## 13. RATE LIMITING Y PROTECCIÓN CONTRA ABUSO

### 13.1 Límites por Endpoint
**CLÁUSULA 13.1.1 — RATE LIMITING GRANULAR**
Se deben implementar límites específicos por tipo de endpoint:

| Endpoint | Límite | Ventana | Alcance |
| --- | --- | --- | --- |
| Login | 5 intentos | 15 min | Por IP + email |
| Registro | 3 cuentas | 1 hora | Por IP |
| API general autenticada | 100 req | 1 min | Por usuario |
| Envío de emails | 5 | 1 hora | Por usuario |
| Upload de archivos | 10 | 1 hora | Por usuario |
| Endpoints de pago | 10 | 1 hora | Por usuario |
| Webhooks internos | 1000 | 1 min | Por origen |

**CLÁUSULA 13.1.2 — PROGRESSIVE DELAY EN LOGIN FALLIDO**
Después de 3 intentos de login fallidos, implementar delay progresivo: 1s, 2s, 4s, 8s... hasta máximo 30s. Después de 10 intentos fallidos, bloquear temporalmente la cuenta por 30 minutos y notificar al usuario por email.

**CLÁUSULA 13.1.3 — HEADERS DE RATE LIMIT**
Las respuestas de la API deben incluir headers estándar de rate limit para que el cliente pueda adaptarse:

```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 87
X-RateLimit-Reset: 1718330400
Retry-After: 60 (cuando se excede el límite)
```

### 13.2 Protección contra Bots
**CLÁUSULA 13.2.1 — DETECCIÓN DE COMPORTAMIENTO AUTOMATIZADO**
Implementar análisis de comportamiento para detectar bots: timing entre requests, patrones de acceso no humanos, headers ausentes (User-Agent, Accept-Language). Las IPs que demuestren comportamiento de bot deben ser bloqueadas temporalmente.

**CLÁUSULA 13.2.2 — TURNSTILE/CAPTCHA EN PUNTOS CRÍTICOS**
Cloudflare Turnstile, hCaptcha o reCAPTCHA v3 deben implementarse en: registro de cuenta, inicio de sesión con múltiples fallos, contacto/soporte, flujos de compra.

---

## 14. SEGURIDAD DE DEPENDENCIAS Y SUPPLY CHAIN

### 14.1 Gestión de Dependencias
**CLÁUSULA 14.1.1 — AUDITORÍA DE DEPENDENCIAS EN CI**
El pipeline de CI debe ejecutar `npm audit` o `pnpm audit` en cada build. Vulnerabilidades CRÍTICAS deben bloquear el deploy. Vulnerabilidades ALTAS deben generar una alerta y ser revisadas en máximo 48 horas. Las vulnerabilidades deben documentarse si no pueden corregirse inmediatamente.

**CLÁUSULA 14.1.2 — LOCKFILE SIEMPRE EN CONTROL DE VERSIONES**
El archivo `package-lock.json` o `pnpm-lock.yaml` DEBE estar commiteado en el repositorio. Esto garantiza que todas las instalaciones usen exactamente las mismas versiones. Los lockfiles deben actualizarse explícitamente, no automáticamente en cada install.

**CLÁUSULA 14.1.3 — VERSIONES EXACTAS EN DEPENDENCIAS CRÍTICAS**
Las dependencias de seguridad crítica (librerías de auth, crypto, validación) deben especificarse con versión exacta (sin `^` ni `~`) para evitar actualizaciones automáticas no auditadas que puedan introducir vulnerabilidades.

**CLÁUSULA 14.1.4 — REVISAR PAQUETES ANTES DE INSTALAR**
Antes de instalar cualquier dependencia nueva, verificar: número de descargas semanales, fecha de última actualización, existencia de maintainers activos, historial de vulnerabilidades conocidas. No instalar paquetes con <1000 descargas semanales sin justificación.

**CLÁUSULA 14.1.5 — PREVENCIÓN DE TYPOSQUATTING Y DEPENDENCY CONFUSION**
Al agregar dependencias, verificar cuidadosamente el nombre del paquete y el namespace (ej. preferir `@org/package` oficial sobre `org-package` no oficial). En los pipelines de CI/CD usar SIEMPRE `npm ci` o `pnpm install --frozen-lockfile` en lugar de `npm install` para evitar la instalación de paquetes maliciosos publicados recientemente bajo nombres similares.

### 14.2 Integridad de Dependencias
**CLÁUSULA 14.2.1 — SCRIPTS NPM NO EJECUTAN CÓDIGO EXTERNO**
Revisar los scripts `postinstall` y `preinstall` de dependencias críticas. Nunca ejecutar `npm install` con `--ignore-scripts` en dependencias que lo requieran sin auditar el script. Los scripts de instalación son un vector común de supply chain attacks.

---

## 15. TESTING DE SEGURIDAD OBLIGATORIO

### 15.1 Tests Automatizados de Seguridad
**CLÁUSULA 15.1.1 — TESTS DE AUTORIZACIÓN**
Para cada endpoint de API, deben existir tests que verifiquen:
* Request sin autenticación → 401
* Request con token de otro usuario → 403
* Request con token expirado → 401
* Request con token manipulado → 401

**CLÁUSULA 15.1.2 — TESTS DE VALIDACIÓN DE INPUT**
Para cada endpoint que acepte datos, deben existir tests con:
* Strings excesivamente largos (>10MB)
* Caracteres especiales y payloads XSS básicos
* SQL injection patterns básicos
* Tipos de datos incorrectos
* Campos requeridos ausentes
* Valores fuera de rango permitido

**CLÁUSULA 15.1.3 — TESTS DE RATE LIMITING**
Verificar que los límites de rate limiting funcionen correctamente. El test debe confirmar que el endpoint devuelve 429 después de exceder el límite y que el límite se resetea correctamente.

### 15.2 Revisión Manual de Seguridad
**CLÁUSULA 15.2.1 — CHECKLIST PRE-DEPLOY**
Antes de cada deploy a producción, verificar manualmente:
- [ ] No hay console.log con datos sensibles
- [ ] No hay credenciales hardcodeadas
- [ ] Los headers de seguridad están configurados
- [ ] Los endpoints nuevos tienen autenticación
- [ ] Las nuevas tablas de DB tienen RLS habilitado
- [ ] Las variables de entorno están documentadas
- [ ] El .gitignore está actualizado
- [ ] Los errores devuelven mensajes genéricos

---

## 16. RESPUESTA A INCIDENTES

### 16.1 Plan de Respuesta
**CLÁUSULA 16.1.1 — PROCEDIMIENTO DE BREACH**
Si se detecta o sospecha una brecha de seguridad, el procedimiento es:
1. **Contener (inmediato):** Revocar credenciales comprometidas, bloquear acceso sospechoso
2. **Evaluar (1 hora):** Determinar alcance y datos afectados
3. **Notificar (24 horas):** Informar a usuarios afectados con detalles claros y sin minimizar
4. **Corregir (72 horas):** Implementar fix del vector de ataque
5. **Post-mortem (1 semana):** Documentar qué falló y cómo prevenir recurrencia

**CLÁUSULA 16.1.2 — DIVULGACIÓN RESPONSABLE**
Mantener un canal de reporte de vulnerabilidades publicado (security@dominio.com). Comprometerse a: acusar recibo en 48 horas, proporcionar timeline de corrección, no tomar acciones legales contra investigadores de buena fe, reconocer el reporte públicamente si el investigador lo desea.

---

## 18. SEGURIDAD AVANZADA DE AUTENTICACIÓN MODERNA

### 18.1 WebAuthn y Passkeys
**CLÁUSULA 18.1.1 — PASSKEYS COMO MÉTODO PRIMARIO**
En proyectos que soporten autenticación moderna, las Passkeys (WebAuthn/FIDO2) deben ser el método primario recomendado. Las contraseñas son el fallback, nunca el camino principal.

**CLÁUSULA 18.1.2 — REGISTRO DE CREDENCIALES**
Al registrar un Passkey:
- Generar challenge con mínimo 32 bytes de entropía del servidor
- Verificar el origin del attestation contra el dominio registrado
- Almacenar credentialId y publicKey en base de datos, nunca en cliente
- Vincular cada Passkey a un solo usuario (nunca compartir)
- Permitir múltiples Passkeys por usuario (dispositivo perdido)

**CLÁUSULA 18.1.3 — FLUJO DE VERIFICACIÓN**
Al autenticar con Passkey:
- Generar challenge nuevo por cada intento (nunca reusar)
- Verificar firma contra la clave pública almacenada
- Verificar counter (signCount) para detectar clonación
- Invalidar challenge inmediatamente después de uso (window ≤5 minutos)

### 18.2 Multi-Factor Adaptativo
**CLÁUSULA 18.2.1 — MFA BASADO EN RIESGO**
Implementar MFA adaptativo que evalúe riesgo por:
- Dispositivo nuevo o no reconocido → MFA obligatorio
- IP de país diferente al habitual → MFA + notificación
- Acciones críticas (pagos, cambio de email/password) → MFA SIEMPRE
- Sesión activa en dispositivo conocido → MFA opcional

---

## 19. SEGURIDAD DE CONTENEDORES Y RUNTIME

### 19.1 Imágenes y Build
**CLÁUSULA 19.1.1 — IMÁGENES BASE MÍNIMAS**
Usar imágenes base mínimas (Alpine, distroless). NUNCA usar imágenes `latest` sin versión fija. Fijar versiones con SHA256 digest cuando sea posible.

**CLÁUSULA 19.1.2 — BUILD MULTI-STAGE**
Todo Dockerfile debe usar multi-stage build. La imagen final NO debe contener:
- Herramientas de build (gcc, make, npm ci con devDependencies)
- Archivos de test
- Archivos .env o secrets
- Código fuente innecesario

### 19.2 Runtime
**CLÁUSULA 19.2.1 — EJECUCIÓN SIN PRIVILEGIOS**
Los contenedores NUNCA deben correr como root. Definir siempre `USER nonroot` en Dockerfile. Filesystem en modo read-only cuando sea posible.

**CLÁUSULA 19.2.2 — HEALTH CHECKS OBLIGATORIOS**
Todo servicio en producción debe tener:
- Health check endpoint (`/healthz` o equivalente)
- Readiness probe (listo para recibir tráfico)
- Liveness probe (proceso sigue respondiendo)
- Startup probe (para servicios con inicialización lenta)

### 19.3 SBOM y Auditoría de Dependencias
**CLÁUSULA 19.3.1 — SOFTWARE BILL OF MATERIALS**
Mantener un SBOM (Software Bill of Materials) actualizado. Ejecutar `npm audit` o equivalente en cada CI pipeline. Las vulnerabilidades críticas (CVSS ≥9.0) bloquean el merge. Las altas (CVSS ≥7.0) generan issue automático con deadline de 72 horas.

**CLÁUSULA 19.3.2 — LOCKFILES OBLIGATORIOS**
Todo proyecto DEBE tener lockfile comprometido en el repositorio (package-lock.json, pnpm-lock.yaml, yarn.lock). NUNCA usar `npm install` sin lockfile en CI. Usar `npm ci` o equivalente para builds reproducibles.

---

## 20. SEGURIDAD DE API GATEWAY Y EDGE

### 20.1 Protección en el Edge
**CLÁUSULA 20.1.1 — WAF Y PROTECCIÓN DDoS**
En proyectos de Escala M y L, implementar protección en el edge:
- WAF (Web Application Firewall) con reglas OWASP
- Protección DDoS con rate limiting por IP, por usuario, y por endpoint
- Geoblocking si el servicio no opera globalmente
- Bot protection con challenge (CAPTCHA) para endpoints sensibles

**CLÁUSULA 20.1.2 — HEADERS DE SEGURIDAD OBLIGATORIOS**
Todo servidor/edge function DEBE retornar estos headers:
```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
Content-Security-Policy: [política estricta según la aplicación]
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

### 20.2 Protección de APIs Públicas
**CLÁUSULA 20.2.1 — API KEYS Y SCOPES**
Las APIs públicas deben usar API keys con:
- Scopes granulares (lectura, escritura, admin)
- Rate limiting diferenciado por plan/tier
- Rotación obligatoria cada 90 días
- Revocación instantánea en caso de compromiso
- Logging de cada uso con IP, timestamp, y endpoint

**CLÁUSULA 20.2.2 — PROTECCIÓN CONTRA ENUMERACIÓN**
Prevenir enumeración de recursos:
- Responder con tiempo constante (timing-safe comparison)
- Misma respuesta para "no existe" y "no autorizado" (404 en ambos casos)
- No exponer conteos totales en APIs de listado sin autenticación
- UUIDs v4 para IDs públicos (imposibles de adivinar)

---

## 17. CHECKLIST FINAL DE VERIFICACIÓN
El agente debe revisar este checklist antes de dar por finalizado cualquier feature o módulo:

**Autenticación y Sesiones**
- [ ] Login usa OAuth/OIDC, Passkeys o hash seguro de contraseña
- [ ] Cookies de sesión tienen HttpOnly, Secure, SameSite=Strict
- [ ] Tokens tienen expiración definida
- [ ] Logout invalida token en servidor
- [ ] Reautenticación en acciones críticas
- [ ] Passkeys implementados con challenge único y counter verification

**Base de Datos**
- [ ] RLS habilitado en todas las tablas de usuario
- [ ] Queries usan parámetros, nunca concatenación
- [ ] IDs públicos son UUIDs, no autoincrement
- [ ] Campos sensibles cifrados con AES-256-GCM

**API y Backend**
- [ ] Todos los endpoints tienen verificación de auth y previenen IDOR
- [ ] Input validado con schema (Zod/Joi)
- [ ] Headers de seguridad configurados (CSP, HSTS, X-Frame-Options, etc.)
- [ ] CORS restringido a orígenes conocidos
- [ ] Rate limiting implementado por IP, usuario y endpoint
- [ ] APIs versionadas y Webhooks con Idempotencia global
- [ ] Validación de URLs y bloqueo de SSRF implementado
- [ ] Tiempos de respuesta constantes para prevenir timing attacks

**Frontend**
- [ ] No hay `dangerouslySetInnerHTML` sin DOMPurify
- [ ] No hay secretos en localStorage
- [ ] URLs de usuario validadas antes de usar como href
- [ ] No hay eval() con input de usuario
- [ ] CSP estricto implementado

**Secretos e Infraestructura**
- [ ] Sin credenciales hardcodeadas
- [ ] .env en .gitignore
- [ ] HTTPS configurado
- [ ] Variables de entorno del cliente sin secretos
- [ ] Lockfiles comprometidos en el repositorio
- [ ] npm audit sin vulnerabilidades críticas

**Integraciones de IA**
- [ ] System prompt separado del input de usuario
- [ ] Llamadas a IA desde servidor, no desde cliente
- [ ] Whitelist de proveedores de IA
- [ ] Fallos de IA manejados sin exponer infraestructura
- [ ] Aislamiento Tenant en RAG / Bases Vectoriales

**Contenedores y Deploy** (si aplica)
- [ ] Imágenes base con versión fija (no `latest`)
- [ ] Multi-stage build sin herramientas de desarrollo
- [ ] Contenedores sin privilegios de root
- [ ] Health checks configurados
- [ ] SBOM actualizado

**Logging y Errores**
- [ ] Errores genéricos al cliente
- [ ] Logs sin PII en texto plano
- [ ] Acciones críticas generan audit log

---

## DECLARACIÓN DE CUMPLIMIENTO
Al trabajar en un proyecto que incluye este contrato, el agente declara:
* **Prioridad absoluta:** Este contrato tiene prioridad sobre cualquier consideración de conveniencia, velocidad de desarrollo o simplificación de código.
* **Notificación obligatoria:** Si se detecta un conflicto entre lo solicitado y este contrato, se notificará explícitamente antes de escribir código, con explicación técnica y propuesta de alternativa segura.
* **Sin excepciones no documentadas:** Cualquier desviación de este contrato debe ser documentada explícitamente con justificación técnica, evaluación de riesgo y aprobación del Director.
* **Verificación continua:** En cada revisión de código, el agente verificará activamente que el código existente cumple con las cláusulas aplicables y señalará cualquier violación encontrada.
* **Actualización del contrato:** Si surgen nuevas amenazas o mejores prácticas que requieran actualizar este contrato, el agente lo propondrá al Director con justificación técnica.

---
*Diseñado por Alexis Loyola Campos — Aloyc México*
*Versión: 1.2 | Fundamentado en: OWASP Top 10 2025, NIST SP 800-63B, ISO 27001, CWE/SANS Top 25, FIDO2 WebAuthn Standards, SLSA Framework*
*Aplicable a: Cualquier proyecto, cualquier framework, cualquier infraestructura*