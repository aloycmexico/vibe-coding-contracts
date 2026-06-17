# CONTRATO DE INPUTS VISUALES Y GESTIÓN DE ASSETS
**Proyecto:** [NOMBRE DEL PROYECTO]
**Versión:** 1.0 | **Fecha:** 16/06/2026 | **Autor:** Alexis Loyola Campos — Aloyc México

## INSTRUCCIONES PARA EL AGENTE
Este contrato define cómo el agente interpreta, prioriza y utiliza inputs visuales del proyecto: imágenes de referencia UX/UI, mockups, assets de marca y media real. El agente NO decide estilo ni layout por cuenta propia cuando existe una referencia visual declarada.

Este contrato es **opcional**. Si el proyecto no incluye inputs visuales, el agente trabaja exclusivamente desde PLANNING.md y los demás contratos. No se carga si no aplica.

---

## 1. JERARQUÍA DE FUENTES

**CLÁUSULA 1.1.1 — ORDEN DE PRIORIDAD**
Cuando el proyecto combina planeación textual e inputs visuales, la jerarquía de autoridad es:

| Prioridad | Fuente | Gobierna |
|-----------|--------|----------|
| 1 (máxima) | `PLANNING.md` | Objetivos, alcance, negocio, restricciones, lógica |
| 2 | `DESIGN.md` | Layout, estilo visual, componentes, densidad, paleta |
| 3 | Imagen principal UX/UI | Referencia dominante de interfaz (cuando está declarada) |
| 4 | Assets obligatorios | Material que DEBE integrarse tal cual |
| 5 | Assets de referencia | Inspiración visual, no para uso directo |

**CLÁUSULA 1.1.2 — PLANNING.md SIEMPRE GOBIERNA EL NEGOCIO**
El diseño visual NO sustituye la planeación. Si PLANNING.md dice "3 columnas" y la imagen muestra 4, PLANNING.md gana. Si PLANNING.md no dice nada sobre columnas y la imagen muestra 4, la imagen guía.

**CLÁUSULA 1.1.3 — DESIGN.md COMO CAPA DE NORMALIZACIÓN**
`DESIGN.md` traduce la intención visual en especificaciones formales. El agente NO interpreta imágenes libremente — lee la normalización documentada en DESIGN.md.

---

## 2. IMAGEN PRINCIPAL UX/UI

**CLÁUSULA 2.1.1 — DECLARACIÓN OBLIGATORIA**
Para que una imagen actúe como referencia dominante, DEBE estar declarada en `DESIGN.md` bajo la sección "REFERENCIA VISUAL PRINCIPAL" con:
- Nombre del archivo y ubicación en `ASSETS/`
- Tipo (mockup, wireframe, screenshot, prototipo)
- Alcance (pantalla completa, componente, flujo)
- Lo que gobierna y lo que NO gobierna

**CLÁUSULA 2.1.2 — LO QUE EL AGENTE EXTRAE DE LA IMAGEN**
Cuando existe una imagen principal declarada, el agente la usa para:
- Layout general y disposición de secciones
- Estilo visual (colores, tipografía, espaciado)
- Densidad de contenido y jerarquía
- Componentes visibles y su organización

**CLÁUSULA 2.1.3 — LO QUE EL AGENTE NO EXTRAE DE LA IMAGEN**
El agente NUNCA extrae de la imagen:
- Lógica de negocio ni reglas de validación
- Textos finales ni copy (a menos que DESIGN.md lo indique)
- Decisiones de seguridad ni arquitectura
- Funcionalidad no descrita en PLANNING.md

---

## 3. CLASIFICACIÓN DE ASSETS

**CLÁUSULA 3.1.1 — TIPOS DE USO**
Todo asset declarado en DESIGN.md tiene exactamente uno de estos tipos:

| Tipo | Significado | Acción del agente |
|------|-------------|-------------------|
| **Obligatorio** | Asset real aprobado para el producto final | Integrar tal cual. No modificar ni sustituir. |
| **Referencia** | Material de inspiración o guía visual | Usar como guía de estilo. No integrar directamente. |

**CLÁUSULA 3.1.2 — ASSETS NO DECLARADOS**
Si un archivo existe en `ASSETS/` pero no está listado en DESIGN.md, el agente lo ignora. No lo integra, no lo referencia, no asume su propósito.

**CLÁUSULA 3.1.3 — ASSETS FALTANTES**
Si DESIGN.md declara un asset pero el archivo no existe en `ASSETS/`, el agente:
1. Registra `[🚨 ASSET FALTANTE: nombre-del-archivo]` en PROJECT_STATE.md
2. Continúa con el trabajo que no depende de ese asset
3. NO genera un sustituto sin autorización del Director

---

## 4. RESOLUCIÓN DE CONFLICTOS

**CLÁUSULA 4.1.1 — CONFLICTO ENTRE PLANNING Y DISEÑO**
Si la imagen o DESIGN.md contradice PLANNING.md:
1. El agente registra `[🚨 CONFLICTO VISUAL]` en PROJECT_STATE.md
2. Describe la contradicción específica
3. Propone cuál fuente debería prevalecer
4. Espera resolución del Director antes de ejecutar la parte conflictiva
5. Continúa con las partes del trabajo que no están en conflicto

**CLÁUSULA 4.1.2 — MÚLTIPLES REFERENCIAS VISUALES**
Si hay más de una imagen de referencia:
- Solo UNA puede ser declarada como "Referencia Visual Principal" en DESIGN.md
- Las demás son assets de tipo "Referencia"
- Si hay ambigüedad, el agente pregunta antes de elegir

**CLÁUSULA 4.1.3 — DISEÑO SIN DESIGN.md**
Si el proyecto tiene imágenes en ASSETS/ pero no tiene DESIGN.md:
- El agente trata todas las imágenes como material de referencia general
- No asume ninguna como dominante
- Sugiere al Director crear DESIGN.md para formalizar la intención visual

---

## 5. INTEGRACIÓN CON EL FLUJO EXISTENTE

**CLÁUSULA 5.1.1 — FLUJO AMPLIADO**
```
PLANNING.md (humano)
    → DESIGN.md (humano o agente normaliza)
        → ARTEFACT.md (agente compila planeación + diseño)
            → Ejecución por sección (agente ejecuta)
                → PROJECT_STATE.md (agente actualiza)
```

**CLÁUSULA 5.1.2 — ARTEFACT INTEGRA DISEÑO**
Cuando existe DESIGN.md, el agente DEBE referenciar las decisiones visuales en las secciones relevantes del ARTEFACT. Formato:
```
### Referencia visual
**Imagen principal:** ASSETS/[nombre]
**Assets obligatorios:** [lista]
**Estilo declarado:** [resumen de DESIGN.md]
```

**CLÁUSULA 5.1.3 — RETRO-COMPATIBILIDAD**
Si el proyecto NO tiene DESIGN.md ni ASSETS/:
- Este contrato no se carga
- El flujo funciona exactamente igual que antes
- No hay cambio de comportamiento para proyectos solo textuales

---

## 6. CHECKLIST DE INPUTS VISUALES

### Antes de ejecutar una sección con componentes UI
- [ ] ¿Existe DESIGN.md? Si sí, leerlo completo
- [ ] ¿Hay imagen principal declarada? Si sí, usarla como referencia dominante
- [ ] ¿Hay assets obligatorios? Si sí, verificar que existen en ASSETS/
- [ ] ¿Hay conflictos entre PLANNING.md y el diseño? Si sí, registrar y escalar

### Durante la ejecución
- [ ] El layout sigue la referencia visual declarada
- [ ] Los assets obligatorios están integrados sin modificación
- [ ] Los assets de referencia guían el estilo pero no están copiados
- [ ] No se inventan elementos visuales que no están en ninguna fuente

### Después de la ejecución
- [ ] PROJECT_STATE.md actualizado con assets integrados
- [ ] Conflictos visuales resueltos o escalados
- [ ] ARTEFACT.md refleja las decisiones visuales tomadas

---

**Aplicable a:** Cualquier proyecto con inputs visuales (mockups, wireframes, brand assets, media)
**No aplica si:** El proyecto es 100% textual, API pura, CLI, o backend sin interfaz

---

*Diseñado por Alexis Loyola Campos — Aloyc México*
