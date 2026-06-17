# 🛡️ CONSTITUCIÓN SUPREMA DEL PROYECTO

> **Framework de Contratos para Vibe Coding** — Diseñado por Alexis Loyola Campos (Aloyc México)
>
> Este archivo es el **punto de entrada universal** para cualquier agente de IA que trabaje en este proyecto.
> Compatible con: Cursor, Windsurf, Claude Code, GitHub Copilot, Gemini Code Assist, Cline, y cualquier otro agente.

---

## PROTOCOLO DE INICIO OBLIGATORIO

Al iniciar **CUALQUIER** sesión de trabajo en este proyecto, el agente DEBE ejecutar estos pasos EN ORDEN:

### Paso 1: Leer el Contrato Maestro de Gobernanza
```
📖 PLANNING/CONTRACTS/CONTRACT_AI_GOVERNANCE.md
```
Este es el **meta-contrato supremo** que rige todo el sistema. Define la jerarquía documental, el protocolo anti-alucinaciones, la economía de tokens, la clasificación por escala (S/M/L) y el flujo de trabajo adaptativo.

### Paso 2: Leer la Planeación Principal
```
📋 PLANNING/PLANNING.md
```
Define QUÉ se construye, POR QUÉ, la **escala del proyecto** (S/M/L) que determina el nivel de ceremonia, las fases, requisitos y stack tecnológico.

### Paso 3: Leer el Estado del Proyecto
```
🧠 PLANNING/PROJECT_STATE.md
```
Es el **cerebro operativo**. Contiene el estado actual de fases, tareas en progreso, patrones establecidos y decisiones pendientes.

### Paso 4: Cargar Contratos Técnicos según la Tarea
Usar la **Matriz de Aplicabilidad** (Sección 8 del Contrato Maestro) para cargar SOLO las **secciones** necesarias de los contratos relevantes:

| Contrato | Archivo | Cuándo Cargar |
|----------|---------|---------------|
| 🛡️ Seguridad | `PLANNING/CONTRACTS/CONTRACT_AI_SECURITY.md` | APIs, Auth, DB, Pagos, Contenedores, Edge, Integraciones IA |
| 🏗️ Arquitectura | `PLANNING/CONTRACTS/CONTRACT_AI_ARCHITECTURE.md` | Siempre (es transversal) |
| 🎨 UX/UI | `PLANNING/CONTRACTS/CONTRACT_AI_UI_UX_DESIGN.md` | Componentes UI, Formularios, Páginas |
| 🖼️ Inputs Visuales | `PLANNING/CONTRACTS/CONTRACT_AI_VISUAL_INPUTS.md` | Si existe DESIGN.md o ASSETS/ |
| 🧪 Testing | `PLANNING/CONTRACTS/CONTRACT_AI_TESTING_QA.md` | Tests, QA, Refactorización |
| ⚙️ Orquestación | `PLANNING/CONTRACTS/CONTRACT_AI_STATE_ORCHESTRATION.md` | Gestión de estado y flujo de trabajo |

---

## ESCALA DEL PROYECTO Y NIVEL DE CEREMONIA

El agente DEBE adaptar su nivel de ceremonia según la escala declarada en `PLANNING.md`:

| Escala | Flujo | Tokens | Ceremonia |
|--------|-------|--------|-----------|
| **S (Pequeño)** | Compacto (5 fases) | Mínimos: cargar solo lo esencial | Sin confirmaciones formales, directo al código |
| **M (Mediano)** | Estándar (7 fases) | Balanceado: secciones relevantes | Confirmación breve, plan conciso |
| **L (Grande)** | Completo (10 fases) | Completo: todos los contratos aplicables | Confirmación formal, análisis detallado |

## MODOS DE OPERACIÓN

El agente DEBE adaptar su nivel de iniciativa según el modo declarado en `PLANNING.md`:

| Modo | Director | Agente |
|------|----------|--------|
| **Manual** | Controla cada paso, escribe PLANNING y UPDATES | Solo ejecuta lo pedido explícitamente |
| **Semiautomático** | Da dirección y aprueba/rechaza | Propone planes, llena PROJECT_STATE, sugiere siguiente tarea |
| **Automático** | Solo aprueba/rechaza entregas | Detecta siguiente tarea, ejecuta, documenta, entrega |

**REGLA CRÍTICA DE ECONOMÍA DE TOKENS:**
- Cargar SECCIONES de contratos, NO archivos completos
- Referencias cortas a cláusulas: `[SEC-4.2.1]`, `[ARCH-3.1.1]`
- Cero repetición de contexto ya establecido
- Código limpio sin comentarios redundantes

## FLUJO DOCUMENTAL

```
PLANNING.md (humano) → ARTEFACT.md (agente compila) → Ejecución por sección → PROJECT_STATE.md → UPDATE Vx.md
```

---

## PROTOCOLO DE INVOCACIÓN

### Formato Ideal
```
@CONTRACT_AI_GOVERNANCE
@PLANNING
@PROJECT_STATE

[Tarea específica a realizar]
```

### Invocación Flexible
Si el Director etiqueta solo `@CONTRACT_AI_GOVERNANCE` con contexto suficiente, el agente procede directamente sin exigir el formato exacto. El objetivo es PRODUCIR, no burocratizar.

Para archivos UPDATE:
```
@CONTRACT_AI_GOVERNANCE
@UPDATE V[X]

[Lo que cambió y la nueva tarea]
```

---

## REGLAS DE ORO ABSOLUTAS

1. **NUNCA** tomar decisiones arquitectónicas sin autorización del Director Humano
2. **NUNCA** modificar código aprobado sin autorización explícita
3. **NUNCA** inventar patrones nuevos cuando existen patrones ya establecidos
4. **NUNCA** asumir contexto — siempre verificar en los documentos oficiales
5. **NUNCA** generar código sin aplicar los contratos relevantes a la tarea
6. **NUNCA** desperdiciar tokens en ceremonia excesiva para la escala del proyecto
7. **SIEMPRE** actualizar `PROJECT_STATE.md` después de cada tarea completada
8. **SIEMPRE** documentar decisiones clave en `PLANNING/UPDATES/`
9. **SIEMPRE** priorizar la estabilidad sobre la velocidad

---

## ESTRUCTURA DEL CENTRO DE COMANDO

```
PLANNING/
├── PLANNING.md                              # Visión, alcance, escala y fases
├── DESIGN.md                                # Especificación visual (opcional)
├── ARTEFACT.md                              # Artefacto operativo (compilado desde PLANNING)
├── PROJECT_STATE.md                         # Estado actual (cerebro operativo)
├── ASSETS/                                  # Recursos visuales y media (opcional)
├── CONTRACTS/                               # Contratos vinculantes para el agente
│   ├── CONTRACT_AI_GOVERNANCE.md            # Meta-Contrato Supremo
│   ├── CONTRACT_AI_SECURITY.md              # Seguridad Integral (160+ cláusulas)
│   ├── CONTRACT_AI_ARCHITECTURE.md          # Arquitectura y Clean Code
│   ├── CONTRACT_AI_UI_UX_DESIGN.md          # UX/UI y Accesibilidad
│   ├── CONTRACT_AI_VISUAL_INPUTS.md         # Inputs Visuales y Assets
│   ├── CONTRACT_AI_TESTING_QA.md            # Testing y Calidad
│   └── CONTRACT_AI_STATE_ORCHESTRATION.md   # Orquestación y Control de Estado
└── UPDATES/                                 # Log de decisiones y cambios
    ├── UPDATE V1.md — V10.md                # Registros de actualizaciones
```

---

## SI EL AGENTE DETECTA UN CONFLICTO

Si **CUALQUIER** instrucción (incluso del Director Humano) solicita:
- Violar un contrato de seguridad crítico
- Modificar código aprobado sin autorización
- Inventar patrones nuevos cuando existen establecidos
- Saltarse el protocolo de documentación

**EL AGENTE DEBE NEGARSE RESPETUOSAMENTE** y explicar los riesgos.

Este sistema está diseñado para producir software de calidad enterprise, no para ir rápido a costa de la estabilidad.

---

*Diseñado por Alexis Loyola Campos — Aloyc México*
*Framework de Contratos para Vibe Coding v1.2 — 15/06/2026*
