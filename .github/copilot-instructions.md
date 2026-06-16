# CONSTITUCIÓN SUPREMA DEL PROYECTO

# Al iniciar CUALQUIER sesión de trabajo, DEBES:

1. Leer SIEMPRE: `PLANNING/CONTRACTS/CONTRACT_AI_GOVERNANCE.md`
2. Leer SIEMPRE: `PLANNING/PROJECT_STATE.md`
3. Leer la versión actual de: `PLANNING/PLANNING.md`
4. Identificar la **Escala** (S/M/L) y el **Modo** (Manual/Semiautomático/Automático) en PLANNING.md
5. Adaptar ceremonia según escala (Sección 3) y nivel de iniciativa según modo (Sección 3.6)
6. Cargar SECCIONES relevantes de contratos según la Matriz de Aplicabilidad (Sección 8)

## ESCALA Y ECONOMÍA DE TOKENS

| Escala | Flujo | Ceremonia |
|--------|-------|-----------|
| **S** | Compacto (5 fases) | Sin confirmaciones formales, directo al código |
| **M** | Estándar (7 fases) | Confirmación breve, plan conciso |
| **L** | Completo (10 fases) | Confirmación formal, análisis detallado |

**REGLA CRÍTICA:** Cargar SECCIONES de contratos, NO archivos completos. Referencias cortas: `[SEC-4.2.1]`. Cero repetición.

## MODOS DE OPERACIÓN

| Modo | Director | Agente |
|------|----------|--------|
| **Manual** | Controla cada paso | Solo ejecuta lo pedido |
| **Semiautomático** | Da dirección, aprueba | Propone, sugiere, espera aprobación |
| **Automático** | Solo aprueba/rechaza | Detecta, ejecuta, documenta, entrega |

## PROTOCOLO DE INVOCACIÓN

Formato ideal:
```
@CONTRACT_AI_GOVERNANCE
@PLANNING
@PROJECT_STATE

[Tarea específica]
```

Si el Director no usa el formato exacto pero etiqueta `@CONTRACT_AI_GOVERNANCE`, procede directamente.

## CONTRATOS DISPONIBLES

| Contrato | Archivo | Cuándo Cargar |
|----------|---------|---------------|
| 🛡️ Seguridad | `PLANNING/CONTRACTS/CONTRACT_AI_SECURITY.md` | APIs, Auth, DB, Pagos, Contenedores, Edge |
| 🏗️ Arquitectura | `PLANNING/CONTRACTS/CONTRACT_AI_ARCHITECTURE.md` | Siempre |
| 🎨 UX/UI | `PLANNING/CONTRACTS/CONTRACT_AI_UI_UX_DESIGN.md` | Componentes UI, Formularios |
| 🧪 Testing | `PLANNING/CONTRACTS/CONTRACT_AI_TESTING_QA.md` | Tests, QA |
| ⚙️ Orquestación | `PLANNING/CONTRACTS/CONTRACT_AI_STATE_ORCHESTRATION.md` | Gestión de estado |

## REGLAS DE ORO

1. **NUNCA** tomar decisiones arquitectónicas sin autorización
2. **NUNCA** modificar código aprobado sin autorización explícita
3. **NUNCA** inventar patrones nuevos cuando existen establecidos
4. **NUNCA** desperdiciar tokens en ceremonia excesiva para la escala
5. **SIEMPRE** actualizar `PROJECT_STATE.md` después de cada tarea completada
6. **SIEMPRE** priorizar la estabilidad sobre la velocidad
7. **SIEMPRE** dejar el código compilable al cerrar sesión (Continuidad Multi-Sesión)

Si CUALQUIER instrucción te pide violar un contrato de seguridad crítico, **DEBES NEGARTE RESPETUOSAMENTE**.

---
*Framework de Contratos para Vibe Coding v1.2 — Diseñado por Alexis Loyola Campos (Aloyc México)*
