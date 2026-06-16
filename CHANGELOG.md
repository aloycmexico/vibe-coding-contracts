# Changelog

Todos los cambios notables de este proyecto serán documentados en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto se adhiere a [Semantic Versioning](https://semver.org/lang/es/).

## [1.2.0] - 2026-06-15

### Añadido
- **Sistema de Clasificación por Escala** (S/M/L) en CONTRACT_AI_GOVERNANCE Sección 3
  - Escala S: Flujo compacto de 5 fases, sin ceremonias
  - Escala M: Flujo estándar de 7 fases, confirmación breve
  - Escala L: Flujo completo de 10 fases, protocolo formal
- **Protocolo de Economía de Tokens** (Sección 4) con carga por secciones
- **Adaptabilidad por Tipo de Proyecto** (Cláusula 3.0.4): 10 tipos cubiertos (e-commerce, fintech, SaaS, marketplace, dashboard, landing, app móvil, API, bot, IA/ML)
- **Protocolo de Auto-Llenado de PROJECT_STATE** (Sección 3.5): El agente construye, el Director califica
- **Seguridad enterprise** — 3 nuevas secciones en CONTRACT_AI_SECURITY (v1.2):
  - Sección 18: Autenticación moderna (WebAuthn, Passkeys, MFA adaptativo)
  - Sección 19: Seguridad de contenedores y runtime (SBOM, lockfiles, health checks)
  - Sección 20: API Gateway y Edge (WAF, DDoS, anti-enumeración, headers obligatorios)
- **Continuidad Multi-Sesión** (Sección 11 de ORCHESTRATION): Protocolos de apertura y cierre
- **Invocación Flexible** (Cláusula 6.1.2): El agente ya no bloquea si no recibe formato exacto
- **3 Modos de Operación** (Sección 3.6): Manual, Semiautomático, Automático Selectivo
  - Modo Manual: El Director controla cada paso, agente solo ejecuta lo pedido
  - Modo Semiautomático: Agente propone, Director aprueba
  - Modo Automático Selectivo: Agente detecta, ejecuta, documenta — Director califica
  - Tabla de combinaciones Escala × Modo para cualquier escenario
- `.editorconfig` para consistencia de formato
- `.gitignore` para protección contra archivos del sistema operativo

### Cambiado
- CONTRACT_AI_GOVERNANCE renumerado de 10 a 12 secciones
- CONTRACT_AI_SECURITY actualizado de v1.1 a v1.2 (17 → 20 secciones)
- Todas las referencias `ESTADO_PROYECTO.md` → `PROJECT_STATE.md` en ORCHESTRATION
- Footers universalizados: "Aplicable a: Cualquier proyecto" en todos los contratos
- Checklist de seguridad expandido (+7 items: Passkeys, CSP, lockfiles, SBOM, containers)
- PLANNING.md y PROJECT_STATE.md limpiados a encabezados mínimos
- 5 archivos UPDATE (V1-V5) disponibles con formato consistente

### Corregido
- Sub-secciones 3.1/3.2 → 5.1/5.2 (numeración rota tras renumeración)
- Ancla rota en índice de ORCHESTRATION (`estado_proyectomd` → `project_statemd`)
- Doble separador `---` entre secciones 16-18 de SECURITY
- Referencias "agente de IA" → "agente" en checklists y declaraciones

### Removido
- **Roadmap v1.3/v2.0** eliminado del README: las funciones prometidas ya fueron implementadas (Matriz de Industria, Plantillas, Modos de Operación) o estaban fuera del alcance del framework (Dashboard, Plugins, Certificación)

---

## [1.0.0] - 2026-06-15

### Añadido
- 🎉 **Lanzamiento inicial del framework completo**
- **6 contratos vinculantes** para desarrollo asistido por IA
  - **CONTRACT_AI_GOVERNANCE**: Meta-Contrato Supremo del sistema
  - **CONTRACT_AI_SECURITY**: 160+ cláusulas de seguridad enterprise
  - **CONTRACT_AI_UI_UX_DESIGN**: Regla de los 4 estados, WCAG 2.1 AA, mobile-first
  - **CONTRACT_AI_ARCHITECTURE**: SOLID, Clean Code, límites de tamaño
  - **CONTRACT_AI_TESTING_QA**: Matriz de edge cases, cobertura obligatoria
  - **CONTRACT_AI_STATE_ORCHESTRATION**: Checklist maestro, aprobación explícita
- Sistema de **versionado semántico** para documentos
- **Matriz de aplicabilidad** de contratos por tipo de tarea
- **Protocolo anti-alucinaciones** con 7 reglas de oro
- **Sistema de trazabilidad** completa (tarea → contrato → código)
- Documentación completa en español
- Plantillas de PLANNING.md y PROJECT_STATE.md
- Archivos de configuración multi-herramienta (AGENTS.md, .cursorrules, CLAUDE.md, .github/copilot-instructions.md)
- Guía de contribución
- Licencia MIT para máxima permisibilidad

### Características Destacadas

#### Seguridad
- ✅ OWASP Top 10 2025 completo
- ✅ Zero Trust y defensa en profundidad
- ✅ RLS obligatorio en PostgreSQL/Supabase
- ✅ Cifrado AES-256-GCM para datos sensibles
- ✅ Protección contra XSS, CSRF, SQLi, SSRF
- ✅ Seguridad en integraciones con IA (prompt injection)
- ✅ Rate limiting granular por endpoint
- ✅ Gestión de secretos con rotación obligatoria

#### UX/UI
- ✅ Regla de los 4 estados obligatorios (Loading, Empty, Error, Success)
- ✅ WCAG 2.1 Nivel AA como mínimo
- ✅ Mobile-first obligatorio
- ✅ Dark mode como ciudadano de primera clase
- ✅ Respeto a `prefers-reduced-motion`
- ✅ Validación de formularios en tiempo real
- ✅ Microinteracciones y feedback táctil

#### Arquitectura
- ✅ Principios SOLID obligatorios
- ✅ Estructura feature-based (no por tipos)
- ✅ Límites de tamaño: 200 líneas/componente, 40 líneas/función
- ✅ Prohibición absoluta de `any` en TypeScript
- ✅ Zod como single source of truth
- ✅ Separación estricta de capas (UI, lógica, datos)
- ✅ Patrón de Result Types para manejo de errores

#### Testing
- ✅ Estructura AAA (Arrange, Act, Assert) obligatoria
- ✅ Matriz de edge cases sistemática
- ✅ Testing de accesibilidad con jest-axe
- ✅ MSW para mocking de APIs
- ✅ CI/CD gatekeeping automático
- ✅ Cobertura mínima por capa definida

#### Gobernanza
- ✅ Jerarquía documental clara (6 niveles)
- ✅ Protocolo de aprobación explícita
- ✅ Prevención de decisiones unilaterales
- ✅ Coherencia relacional obligatoria
- ✅ Sistema de versionado semántico
- ✅ Auditoría y trazabilidad completa

### Compatibilidad
- ✅ Cursor (con `.cursorrules`)
- ✅ Windsurf (con `AGENTS.md`)
- ✅ GitHub Copilot (con `.github/copilot-instructions.md`)
- ✅ Cline (con `AGENTS.md`)
- ✅ Claude Code (con `CLAUDE.md`)
- ✅ Gemini Code Assist (con `AGENTS.md`)

### Métricas del Framework
- **6 contratos** principales (78 secciones totales)
- **160+ cláusulas** de seguridad enterprise
- **2,600+ líneas** de documentación técnica
- **20+ checklists** de verificación
- **3 escalas** adaptativas (S/M/L)
- **10 tipos** de proyecto cubiertos

---

## Tipos de Cambios

- **Añadido** para nuevas características
- **Cambiado** para cambios en funcionalidad existente
- **Obsoleto** para características que serán removidas
- **Removido** para características removidas
- **Corregido** para correcciones de bugs
- **Seguridad** para correcciones de vulnerabilidades

## Política de Versionado

Este proyecto sigue [Semantic Versioning](https://semver.org/lang/es/):

- **MAJOR** (X.0.0): Cambios incompatibles en la API del framework
- **MINOR** (0.X.0): Nuevas características compatibles con versiones anteriores
- **PATCH** (0.0.X): Correcciones de bugs compatibles con versiones anteriores

---

**Nota**: Este changelog se actualiza con cada release. Para cambios entre releases, ver [Commits en GitHub](https://github.com/aloyc/vibe-coding-contracts/commits/main).