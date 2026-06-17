# ASSETS

Carpeta de recursos visuales y media del proyecto.

## Convenciones

### Naming
- Usar nombres descriptivos en minúsculas con guiones: `hero-mockup.png`, `logo-principal.svg`
- Prefijo por tipo cuando hay muchos assets: `icon-menu.svg`, `img-hero.jpg`, `ref-competencia.png`

### Organización
- Carpeta plana por defecto. Crear subcarpetas solo si el volumen lo justifica.
- Subcarpetas sugeridas cuando sean necesarias:
  - `brand/` — Logos, identidad visual
  - `mockups/` — Diseños UX/UI, wireframes, prototipos
  - `media/` — Imágenes, videos, animaciones para el producto
  - `references/` — Material de inspiración (no para uso directo)

### Declaración
Todo asset que el agente deba conocer DEBE estar declarado en `PLANNING/DESIGN.md` con su tipo de uso:
- **Obligatorio**: Se integra tal cual en el producto.
- **Referencia**: Se usa como guía visual, no se integra directamente.

Assets no declarados en DESIGN.md son ignorados por el agente.

---

*Diseñado por Alexis Loyola Campos — Aloyc México*
