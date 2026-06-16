# 🤝 Guía de Contribución

¡Gracias por tu interés en contribuir al Framework de Contratos para Vibe Coding! Este proyecto crece gracias a la comunidad y valoramos enormemente cada aporte.

## 📋 Tabla de Contenidos

- [Cómo Contribuir](#-cómo-contribuir)
- [Tipos de Contribuciones](#-tipos-de-contribuciones)
- [Proceso de Pull Requests](#-proceso-de-pull-requests)
- [Estándares de Calidad](#-estándares-de-calidad)
- [Reportar Problemas](#-reportar-problemas)

---

## 🎯 Cómo Contribuir

### 1. Fork el Repositorio

```bash
gh repo fork aloyc/vibe-coding-contracts
```

### 2. Crea una Rama

```bash
git checkout -b feature/nombre-descriptivo
```

### 3. Haz tus Cambios

Sigue los [Estándares de Calidad](#-estándares-de-calidad) descritos abajo.

### 4. Commit con Mensaje Descriptivo

```bash
git commit -m "feat(contracts): agregar cláusula de seguridad para WebSockets"
```

### 5. Push y Pull Request

```bash
git push origin feature/nombre-descriptivo
```

---

## 📝 Tipos de Contribuciones

### Contratos y Cláusulas
- Sugerir nuevas cláusulas para contratos existentes
- Proponer nuevos contratos especializados (ej. contratos por industria)
- Actualizar cláusulas con mejores prácticas más recientes

### Documentación
- Corregir errores tipográficos o de formato
- Mejorar ejemplos de código
- Traducir a otros idiomas

### Plantillas
- Crear templates de proyecto para stacks específicos
- Mejorar las plantillas existentes de PLANNING.md y PROJECT_STATE.md

### Bugs y Mejoras
- Reportar inconsistencias entre contratos
- Sugerir mejoras de usabilidad del framework

---

## 🔄 Proceso de Pull Requests

1. **Describe claramente** qué cambias y por qué
2. **Referencia** la cláusula o contrato que modificas
3. **Verifica** que tu cambio no contradice otros contratos
4. **Asegúrate** de que el markdown se renderiza correctamente

---

## ✅ Estándares de Calidad

- Los contratos deben estar en **español** (contenido) con **nombres de archivo en inglés**
- Las cláusulas deben seguir el formato: `**CLÁUSULA X.Y.Z — NOMBRE EN MAYÚSCULAS**`
- Los ejemplos de código deben mostrar **❌ PROHIBIDO** y **✅ CORRECTO**
- Toda cláusula debe ser **accionable** (el agente puede verificar su cumplimiento)

---

## 🐛 Reportar Problemas

Usa [GitHub Issues](https://github.com/aloyc/vibe-coding-contracts/issues) con:
- Descripción clara del problema
- Contrato y cláusula afectada (si aplica)
- Propuesta de solución (opcional)

---

*Diseñado por Alexis Loyola Campos — Aloyc México*