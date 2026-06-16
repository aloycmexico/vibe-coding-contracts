# 🛡️ Framework de Contratos para Vibe Coding con IA

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.2.0-blue.svg)](https://github.com/aloycmexico/vibe-coding-contracts)
[![Anti-Hallucination](https://img.shields.io/badge/anti--hallucination-enforced-red.svg)](./PLANNING/CONTRACTS/CONTRACT_AI_GOVERNANCE.md)

> **El sistema definitivo para desarrollo asistido por IA con calidad enterprise, blindado contra alucinaciones y deuda técnica.**

## 📋 Descripción

Este framework establece un **sistema de gobernanza completo** para proyectos de desarrollo asistido por IA (Cursor, Claude Code, Gemini, Copilot, Windsurf, Cline, etc.). A través de 6 contratos vinculantes, transforma la IA de un "asistente creativo" en un **equipo virtual de ingenieros senior** con responsabilidades claras, protocolos estrictos y mecanismos anti-alucinación.

### ¿Qué problema resuelve?

Cuando programas con IA sin guardrails:

* ❌ Genera código con vulnerabilidades de seguridad
* ❌ Crea interfaces con mala UX y sin accesibilidad
* ❌ Produce "código espagueti" inmantenible
* ❌ Olvida contextos entre sesiones
* ❌ Inventa patrones inconsistentes
* ❌ Alucina funcionalidades no solicitadas

### ¿Qué obtienes con este framework?

* ✅ **Seguridad enterprise**: OWASP Top 10 2025, Zero Trust, RLS, WebAuthn, SBOM
* ✅ **UX/UI profesional**: WCAG AA, 4 estados obligatorios, mobile-first
* ✅ **Arquitectura limpia**: SOLID, Clean Code, patrones de diseño
* ✅ **Testing robusto**: Edge cases, TDD, cobertura obligatoria
* ✅ **Control de estado**: Auto-llenado de PROJECT\_STATE, aprobación explícita
* ✅ **Gobernanza total**: Anti-alucinaciones, coherencia histórica, trazabilidad
* ✅ **Escalas adaptativas**: Flujos S/M/L para proyectos de cualquier tamaño
* ✅ **Economía de tokens**: Carga por secciones, cero desperdicio
* ✅ **Artefacto operativo**: Compilación de PLANNING a secciones ejecutables
* ✅ **10 tipos de proyecto**: E-commerce, fintech, SaaS, marketplace, y más

## 🎯 Casos de Uso

### Ideal para:

* **Startups** que necesitan velocidad sin sacrificar calidad
* **Equipos pequeños** que usan IA como multiplicador de fuerza
* **Freelancers** que entregan proyectos enterprise
* **Empresas** que quieren estandarizar el desarrollo con IA
* **Educadores** que enseñan ingeniería de software moderna

### Compatible con:

* **Frameworks**: Next.js, React, Vue, Svelte, Node.js, y cualquier otro
* **Herramientas IA**: Cursor, Claude Code, GitHub Copilot, Windsurf, Cline, Gemini Code Assist
* **Bases de datos**: Supabase, PostgreSQL, MongoDB, cualquier SQL/NoSQL
* **Plataformas**: Vercel, Netlify, Railway, AWS, GCP, Azure

## 🏗️ Estructura del Framework

```
vibe-coding-contracts/
├── AGENTS.md                        # Punto de entrada universal para agentes
├── .cursorrules                     # Configuración para Cursor
├── CLAUDE.md                        # Configuración para Claude Code
├── .github/
│   └── copilot-instructions.md      # Configuración para GitHub Copilot
│
├── PLANNING/                        # Centro de Comando
│   ├── PLANNING.md                  # Planeación maestro del proyecto
│   ├── ARTEFACT.md                  # Artefacto operativo (compilado desde PLANNING)
│   ├── PROJECT_STATE.md             # Estado operativo actual
│   ├── CONTRACTS/                   # Contratos vinculantes
│   │   ├── CONTRACT_AI_GOVERNANCE.md
│   │   ├── CONTRACT_AI_SECURITY.md
│   │   ├── CONTRACT_AI_ARCHITECTURE.md
│   │   ├── CONTRACT_AI_UI_UX_DESIGN.md
│   │   ├── CONTRACT_AI_TESTING_QA.md
│   │   └── CONTRACT_AI_STATE_ORCHESTRATION.md
│   └── UPDATES/                     # Registro de decisiones y cambios
│       ├── UPDATE V1.md
│       ├── UPDATE V2.md
│       ├── ...
│       └── UPDATE V10.md
│
├── .editorconfig                    # Consistencia de formato
├── .gitignore                       # Archivos excluidos
├── README.md                        # Este archivo
├── LICENSE                          # Licencia MIT
├── CHANGELOG.md                     # Historial de cambios
├── CONTRIBUTING.md                  # Guía de contribución
└── SECURITY.md                      # Política de seguridad
```

> Los archivos `PLANNING.md`, `ARTEFACT.md`, `PROJECT_STATE.md` y los `UPDATE V*.md` se incluyen como **plantillas vacías listas para rellenar**. Cada proyecto los completa con su propia planeación, artefacto operativo, estado y registro de actualizaciones.

## 🚀 Inicio Rápido

### 1. Clona este repositorio

```bash
git clone https://github.com/aloycmexico/vibe-coding-contracts.git
cd vibe-coding-contracts
```

### 2. Copia la estructura a tu proyecto

```bash
# Copia la carpeta PLANNING completa a tu proyecto
cp -r PLANNING /ruta/a/tu/proyecto/

# Copia los archivos de configuración del agente
cp AGENTS.md /ruta/a/tu/proyecto/
cp .cursorrules /ruta/a/tu/proyecto/          # Si usas Cursor
cp CLAUDE.md /ruta/a/tu/proyecto/             # Si usas Claude Code
cp -r .github /ruta/a/tu/proyecto/            # Si usas GitHub Copilot
```

### 3. Personaliza los documentos

```bash
# Define tu proyecto
nano PLANNING/PLANNING.md

# Inicializa el estado
nano PLANNING/PROJECT_STATE.md
```

### 4. Comienza a programar

Invoca al agente con el protocolo estándar:

```
@CONTRACT_AI_GOVERNANCE
@PLANNING
@PROJECT_STATE

Implementar sistema de autenticación con OAuth
```

## 📚 Los 6 Contratos

### 🎼 Contrato Maestro de Gobernanza

**El orquestador supremo** que rige todo el sistema. Define la jerarquía documental, clasificación por escala (S/M/L), economía de tokens, protocolo anti-alucinaciones, y flujo de trabajo adaptativo.

[Leer contrato →](./PLANNING/CONTRACTS/CONTRACT_AI_GOVERNANCE.md)

### 🛡️ Contrato de Seguridad Integral

**160+ cláusulas** de seguridad enterprise: OAuth/OIDC, WebAuthn/Passkeys, RLS, cifrado AES-256-GCM, prevención de XSS/CSRF/SQLi, protección contra prompt injection, seguridad de contenedores, SBOM, y API Gateway.

[Leer contrato →](./PLANNING/CONTRACTS/CONTRACT_AI_SECURITY.md)

### 🎨 Contrato de UX/UI y Accesibilidad

**Regla de los 4 estados** (Loading, Empty, Error, Success), WCAG 2.1 AA, mobile-first, diseño responsive, microinteracciones, y copywriting UX.

[Leer contrato →](./PLANNING/CONTRACTS/CONTRACT_AI_UI_UX_DESIGN.md)

### 🏗️ Contrato de Arquitectura y Clean Code

**SOLID obligatorio**, estructura feature-based, límites de tamaño (200 líneas/componente), prohibición de `any`, patrones de diseño, y nomenclatura estricta.

[Leer contrato →](./PLANNING/CONTRACTS/CONTRACT_AI_ARCHITECTURE.md)

### 🧪 Contrato de Testing y QA

**Matriz de Edge Cases**, estructura AAA, mocking estratégico, testing de accesibilidad, CI/CD gatekeeping, y cobertura obligatoria.

[Leer contrato →](./PLANNING/CONTRACTS/CONTRACT_AI_TESTING_QA.md)

### ⚙️ Contrato de Orquestación de Estado

**Checklist maestro** con aprobación explícita, auto-llenado de PROJECT\_STATE, continuidad multi-sesión, prevención de decisiones unilaterales, y protocolo de inicio/fin de sesión.

[Leer contrato →](./PLANNING/CONTRACTS/CONTRACT_AI_STATE_ORCHESTRATION.md)

## 🔥 Características Destacadas

### Anti-Alucinaciones Reforzado

* 7 reglas de oro que previenen invención de patrones
* Sistema de detección automática de inconsistencias
* Protocolo de aviso de impacto para cambios no autorizados

### Economía de Tokens

* Carga selectiva de contratos según tarea
* Compresión de historial en archivos de estado
* Sistema de referencias en lugar de duplicados

### Trazabilidad Completa

* Cada línea de código vinculada a tarea aprobada
* Commits con referencias a contratos y cláusulas
* Log de decisiones en UPDATES

### Gobernanza Empresarial

* Jerarquía documental clara (6 niveles)
* 3 modos de operación (Manual, Semiautomático, Automático)
* Escalas adaptativas S/M/L con ceremonia proporcional
* Auditoría y reportes de cumplimiento

## 📊 Comparación: Con vs Sin Framework

| Aspecto | Sin Framework | Con Este Framework |
|---------|---------------|-------------------|
| **Seguridad** | Vulnerabilidades comunes | OWASP Top 10 cubierto |
| **UX** | Estados faltantes, mala a11y | 4 estados, WCAG AA |
| **Código** | Espagueti, inconsistente | Clean Code, SOLID |
| **Tests** | Solo happy path | Edge cases completos |
| **Contexto** | Se pierde entre sesiones | Estado persistente |
| **Alucinaciones** | Frecuentes | Bloqueadas por protocolo |
| **Deuda técnica** | Acumulación rápida | Controlada y documentada |

## 🎓 Filosofía

Este framework se basa en tres principios fundamentales:

### 1. **La IA es un ejecutor, no un decisor**

La IA implementa bajo contratos claros. Las decisiones arquitectónicas y de negocio siempre las toma el humano.

### 2. **La velocidad no justifica la deuda técnica**

Preferimos ir más lento con calidad que rápido con código que habrá que reescribir en 3 meses.

### 3. **La transparencia es obligatoria**

Cualquier duda, conflicto o bloqueo debe escalarse inmediatamente. Nunca asumir ni adivinar.

## 🛠️ Herramientas Compatibles

### Editores con Soporte IA

| Herramienta | Archivo de Configuración | Estado |
|-------------|-------------------------|--------|
| **Cursor** | `.cursorrules` | ✅ Soportado |
| **Windsurf** | `AGENTS.md` | ✅ Soportado |
| **Claude Code** | `CLAUDE.md` | ✅ Soportado |
| **GitHub Copilot** | `.github/copilot-instructions.md` | ✅ Soportado |
| **Cline** | `AGENTS.md` | ✅ Soportado |
| **Gemini Code Assist** | `AGENTS.md` | ✅ Soportado |

### Modelos de IA Compatibles

* ✅ Claude 4 / Opus / Sonnet
* ✅ GPT-4o / GPT-4.1
* ✅ Gemini 2.5 Pro / Flash
* ✅ Llama 4
* ✅ Cualquier modelo que pueda seguir instrucciones en markdown

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Este es un proyecto open source y crece con la comunidad.

### Formas de contribuir:

* 🐛 Reportar bugs o inconsistencias en contratos
* 💡 Sugerir nuevas cláusulas o mejoras
* 📝 Mejorar documentación
* 🌍 Traducir a otros idiomas
* 🧪 Compartir casos de uso y experiencias

Lee nuestra [Guía de Contribución](./CONTRIBUTING.md) para más detalles.

## 📄 Licencia

Este proyecto está licenciado bajo la **Licencia MIT** — ver el archivo [LICENSE](./LICENSE) para más detalles.

**Resumen:**

* ✅ Uso comercial permitido
* ✅ Modificación permitida
* ✅ Distribución permitida
* ✅ Uso privado permitido
* ⚠️ Sin garantía
* ℹ️ Debe incluir licencia y copyright

## 👤 Autor

**Alexis Loyola Campos**
*Aloyc México*

* 🌐 Website: [aloycmexico.net](https://www.aloycmexico.net)
* 🐦 X: [@aloycmexico](https://x.com/aloycmexico)
* 🔗 Discord: [@aloycmexico](https://discord.gg/57u6kNc3ch)
* 🧑 Facebook: [@aloycmexico](https://www.facebook.com/aloycmexico)
* 📸 Youtube: [@aloycmexico](https://www.youtube.com/@aloycmexico)
* 📧 Email: support@aloycmexico.net

## 🎛️ Modos de Operación

El framework incluye 3 modos que definen cuánta iniciativa toma el agente:

### 🔧 Modo Manual

El Director controla cada paso. El agente solo ejecuta lo que se le pide explícitamente. Ideal para proyectos regulados o cuando se quiere máximo control.

### ⚖️ Modo Semiautomático

Balance ideal. El agente propone planes, llena PROJECT\_STATE, sugiere la siguiente tarea — pero siempre espera aprobación antes de ejecutar.

### 🚀 Modo Automático Selectivo

Máxima productividad. El agente detecta la siguiente tarea, ejecuta, documenta y entrega. El Director solo aprueba o rechaza. Toda acción sigue bajo los contratos de seguridad y gobernanza.

> Los Modos se combinan con las Escalas (S/M/L) para cubrir cualquier escenario: desde un fix rápido (`S + Manual`) hasta una plataforma enterprise (`L + Semiautomático`).

## 📞 Soporte

¿Necesitas ayuda implementando este framework?

* 📚 **Documentación**: Revisa la carpeta `PLANNING/`
* 💬 **Discusiones**: Usa [GitHub Discussions](https://github.com/aloycmexico/vibe-coding-contracts/discussions)
* 🐛 **Bugs**: Reporta en [Issues](https://github.com/aloycmexico/vibe-coding-contracts/issues)
* 💼 **Consultoría**: Contacta a [Aloyc México](mailto:support@aloycmexico.net)

## ⭐ Muestra tu apoyo

Si este framework te ha sido útil, considera:

* ⭐ Dar una estrella en GitHub
* 🐦 Compartir en X/LinkedIn
* 📝 Escribir un blog post sobre tu experiencia

***

<div align="center">

**Hecho en México por [Alexis Loyola Campos](https://www.aloycmexico.net)**

*Transformando el Vibe Coding de arte caótico a ingeniería disciplinada*

[⬆ Volver arriba](#-framework-de-contratos-para-vibe-coding-con-ia)

</div>
