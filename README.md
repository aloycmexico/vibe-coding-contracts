# 🛡️ Framework de Contratos para Vibe Coding con IA

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.2.0-blue.svg)](https://github.com/aloycmexico/vibe-coding-contracts)
[![Anti-Hallucination](https://img.shields.io/badge/anti--hallucination-enforced-red.svg)](./PLANNING/CONTRACTS/CONTRACT_AI_GOVERNANCE.md)

> **El sistema definitivo para desarrollo asistido por IA con calidad enterprise, blindado contra alucinaciones y deuda técnica.**

## 📋 Descripción

Este framework establece un **sistema de gobernanza completo** para proyectos de desarrollo asistido por IA. A través de 7 contratos vinculantes, transforma cualquier agente capaz de leer markdown — sin importar proveedor, modelo o precio — en un **equipo virtual de ingenieros senior** con responsabilidades claras, protocolos estrictos y mecanismos anti-alucinación.

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
* ✅ **Inputs visuales**: Soporte formal para mockups, assets y referencias UX/UI
* ✅ **10 tipos de proyecto**: E-commerce, fintech, SaaS, marketplace, y más

## 🎯 Casos de Uso

### Ideal para:

* **Startups** que necesitan velocidad sin sacrificar calidad
* **Equipos pequeños** que usan IA como multiplicador de fuerza
* **Freelancers** que entregan proyectos enterprise
* **Empresas** que quieren estandarizar el desarrollo con IA
* **Educadores** que enseñan ingeniería de software moderna

### Compatibilidad

**Herramientas de desarrollo con IA:**
Cursor, Claude Code, GitHub Copilot, Windsurf, Cline, Antigravity, Gemini Code Assist, Gemini CLI, Codex CLI, Aider, Continue, y cualquier herramienta capaz de leer markdown y operar sobre un repositorio.

**Modelos y proveedores:**
Claude (Anthropic), GPT (OpenAI), Gemini (Google), DeepSeek, Qwen, Mistral, Llama, y cualquier modelo actual o futuro con capacidad de seguir instrucciones estructuradas.

**Requisitos mínimos del agente:**
* Lectura de archivos markdown
* Seguimiento de instrucciones multi-paso
* Capacidad de operar por secciones o contexto completo

> Los modelos frontier aprovechan mejor contextos amplios y tareas complejas. Los modelos más pequeños u open-weight son suficientes para cambios puntuales, iteraciones acotadas o proyectos de baja complejidad. El framework se adapta al nivel de agente disponible sin perder estructura.

**Stack técnico:**
* **Frameworks**: Next.js, React, Vue, Svelte, Node.js, y cualquier otro
* **Bases de datos**: Supabase, PostgreSQL, MongoDB, cualquier SQL/NoSQL
* **Plataformas**: Vercel, Netlify, Railway, AWS, GCP, Azure

## 🔗 Recursos y API Keys

Para obtener acceso a los modelos y herramientas compatibles con este framework:

### Proveedores de modelos
| Proveedor | Modelos principales | Obtener API Key |
|-----------|-------------------|-----------------|
| Anthropic | Claude | [console.anthropic.com](https://console.anthropic.com) |
| OpenAI | GPT, Codex, o1 | [platform.openai.com](https://platform.openai.com) |
| Google | Gemini | [aistudio.google.com](https://aistudio.google.com) |
| DeepSeek | DeepSeek-V3, R1 | [platform.deepseek.com](https://platform.deepseek.com) |
| Mistral | Mistral, Codestral | [console.mistral.ai](https://console.mistral.ai) |
| Alibaba | Qwen | [dashscope.aliyun.com](https://dashscope.aliyun.com) |
| Meta | Llama (vía proveedores) | [llama.developer.meta.com](https://llama.developer.meta.com) |
| NVIDIA | Nemotron, NIM | [build.nvidia.com](https://build.nvidia.com) |

### Herramientas y agentes
| Herramienta | Descripción | Acceso |
|-------------|-------------|--------|
| Cursor | Editor IA con agente integrado | [cursor.com](https://cursor.com) |
| Claude Code | Agente CLI de Anthropic | [claude.ai/code](https://claude.ai/code) |
| GitHub Copilot | Asistente IA en VS Code / GitHub | [github.com/features/copilot](https://github.com/features/copilot) |
| Windsurf | Editor IA de Codeium | [codeium.com/windsurf](https://codeium.com/windsurf) |
| Antigravity | Plataforma multi-agente | [antigravity.dev](https://antigravity.dev) |
| Cline | Agente IA open source para VS Code | [github.com/cline/cline](https://github.com/cline/cline) |
| Aider | Agente CLI para Git | [aider.chat](https://aider.chat) |
| Continue | Extensión IA open source | [continue.dev](https://continue.dev) |
| Gemini CLI | CLI de Google con Gemini | [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) |

### Comparativa y benchmarks actualizados
> Los modelos evolucionan constantemente. Para comparar capacidades, benchmarks y precios actualizados consulta:
> - [Artificial Analysis](https://artificialanalysis.ai) — calidad, velocidad y precio por modelo
> - [LMSYS Chatbot Arena](https://lmsys.org) — ranking por votación humana
> - [OpenRouter](https://openrouter.ai/models) — precios y disponibilidad en tiempo real

## 🏗️ Estructura del Framework

```text
vibe-coding-contracts/
├── AGENTS.md
├── .cursorrules
├── CLAUDE.md
├── .github/
│   └── copilot-instructions.md
├── PLANNING/
│   ├── PLANNING.md
│   ├── DESIGN.md
│   ├── ARTEFACT.md
│   ├── PROJECT_STATE.md
│   ├── ASSETS/
│   ├── CONTRACTS/
│   │   ├── CONTRACT_AI_GOVERNANCE.md
│   │   ├── CONTRACT_AI_SECURITY.md
│   │   ├── CONTRACT_AI_ARCHITECTURE.md
│   │   ├── CONTRACT_AI_UI_UX_DESIGN.md
│   │   ├── CONTRACT_AI_VISUAL_INPUTS.md
│   │   ├── CONTRACT_AI_TESTING_QA.md
│   │   └── CONTRACT_AI_STATE_ORCHESTRATION.md
│   └── UPDATES/
│       ├── UPDATE V1.md
│       ├── UPDATE V2.md
│       ├── ...
│       └── UPDATE V10.md
├── .editorconfig
├── .gitignore
├── README.md
├── LICENSE
├── CHANGELOG.md
├── CONTRIBUTING.md
└── SECURITY.md
```

> Los archivos `PLANNING.md`, `ARTEFACT.md`, `PROJECT_STATE.md` y los `UPDATE V*.md`
> se incluyen como plantilla base intencionalmente vacía para que cada proyecto
> los rellene con su propia planeación, sin arrastrar contenido de ejemplo innecesario.
> `DESIGN.md` y `ASSETS/` son opcionales: úsalos solo si tu proyecto requiere
> inputs visuales, logos, media o referencias de diseño UI/UX.

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

## 📚 Los 7 Contratos

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

### 🖼️ Contrato de Inputs Visuales

**Gestión de referencias visuales y assets**: jerarquía formal entre planeación textual y diseño visual, clasificación de assets (obligatorio/referencia), resolución de conflictos visual-textual, e integración con ARTEFACT.

[Leer contrato →](./PLANNING/CONTRACTS/CONTRACT_AI_VISUAL_INPUTS.md)

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
