# 🔒 Política de Seguridad

## Versiones Soportadas

Actualmente se proporcionan actualizaciones de seguridad para las siguientes versiones del framework:

| Versión | Soportada          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

## 🛡️ Reportar una Vulnerabilidad

La seguridad es nuestra prioridad #1. Si descubres una vulnerabilidad de seguridad en este framework, agradecemos enormemente que nos lo informes de manera responsable.

### ⚠️ Por favor NO reportes vulnerabilidades de seguridad en Issues públicos de GitHub

### Proceso de Reporte Responsable

1. **Envía un email** a: **support@aloycmexico.net**
2. **Incluye** en tu reporte:
   - Descripción detallada de la vulnerabilidad
   - Pasos para reproducirla
   - Impacto potencial
   - Si es posible, una propuesta de solución
   - Tu nombre/handle (si deseas ser acreditado)

3. **Espera confirmación** dentro de 48 horas

### Qué esperar

- **Acuse de recibo**: Dentro de 48 horas
- **Evaluación inicial**: Dentro de 5 días hábiles
- **Actualizaciones regulares**: Te mantendremos informado del progreso
- **Resolución**: Trabajaremos para resolver vulnerabilidades críticas en 7 días, altas en 30 días
- **Crédito**: Si lo deseas, serás acreditado públicamente cuando la vulnerabilidad sea resuelta

### Qué NO reportar

- ❌ Issues de calidad de código que no sean vulnerabilidades de seguridad
- ❌ Problemas de rendimiento
- ❌ Sugerencias de nuevas características (usa Issues normales)
- ❌ Vulnerabilidades en dependencias (reportar directamente al maintainer)

## 🔍 Alcance de la Política de Seguridad

Esta política aplica a:

- ✅ Todos los contratos y cláusulas del framework
- ✅ Documentación y ejemplos de código
- ✅ Scripts y herramientas incluidas
- ✅ Templates y generadores

Esta política NO aplica a:

- ❌ Proyectos que usen este framework (son responsables de su propia seguridad)
- ❌ Dependencias de terceros (cada una tiene su propia política)
- ❌ Herramientas de IA compatibles (Cursor, Claude, etc.)

## 🎯 Definición de Vulnerabilidades

Consideramos vulnerabilidades de seguridad:

### Críticas
- Ejemplos de código que introduzcan vulnerabilidades conocidas (SQLi, XSS, etc.)
- Cláusulas que contradigan estándares de seguridad establecidos (OWASP, NIST)
- Documentación que pueda llevar a implementaciones inseguras

### Altas
- Omisión de controles de seguridad importantes
- Ejemplos que no sigan las propias cláusulas del contrato
- Recomendaciones obsoletas o deprecadas

### Medias
- Falta de claridad en cláusulas de seguridad
- Ejemplos incompletos que puedan malinterpretarse
- Referencias a estándares desactualizados

### Bajas
- Typos en documentación de seguridad
- Enlaces rotos a recursos de seguridad
- Formato inconsistente en ejemplos

## 🔧 Proceso de Corrección

1. **Confirmación**: Validamos la vulnerabilidad
2. **Clasificación**: Asignamos severidad (Crítica, Alta, Media, Baja)
3. **Desarrollo**: Creamos el fix en una rama privada
4. **Testing**: Verificamos que el fix resuelve el problema sin introducir nuevos
5. **Release**: Publicamos nueva versión con el fix
6. **Divulgación**: Anunciamos la vulnerabilidad y el fix (con crédito si se desea)
7. **Post-mortem**: Analizamos cómo prevenir vulnerabilidades similares

## 📢 Divulgación Pública

Después de resolver una vulnerabilidad:

1. Publicamos un **Security Advisory** en GitHub
2. Actualizamos el **CHANGELOG.md**
3. Notificamos a través de **GitHub Discussions**
4. Si es crítica, enviamos notificación por email a usuarios suscritos
5. Actualizamos la documentación relevante

### Timeline de Divulgación

- **Críticas**: Inmediatamente después del fix
- **Altas**: 7 días después del fix
- **Medias**: 30 días después del fix
- **Bajas**: En el siguiente release regular

## 🛡️ Mejores Prácticas para Usuarios

Al usar este framework, te recomendamos:

1. **Mantente actualizado**: Usa siempre la última versión
2. **Revisa los advisories**: Suscríbete a notificaciones de seguridad
3. **Valida ejemplos**: Siempre adapta los ejemplos a tu contexto específico
4. **Audita tu implementación**: Usa herramientas de análisis estático
5. **Mantén dependencias actualizadas**: Ejecuta `npm audit` regularmente
6. **Sigue los contratos completamente**: No omitas cláusulas de seguridad
7. **Reporta problemas**: Si encuentras algo inseguro, repórtalo

## 🔐 Herramientas de Seguridad Recomendadas

Para proyectos que usen este framework:

### Análisis Estático
- [Semgrep](https://semgrep.dev/)
- [CodeQL](https://codeql.github.com/)
- [SonarQube](https://www.sonarqube.org/)

### Análisis de Dependencias
- [Snyk](https://snyk.io/)
- [Dependabot](https://github.com/dependabot)
- [npm audit](https://docs.npmjs.com/cli/audit)

### Testing de Seguridad
- [OWASP ZAP](https://www.zaproxy.org/)
- [Burp Suite](https://portswigger.net/burp)
- [Nikto](https://cirt.net/Nikto2)

### Monitoreo
- [GitHub Security Advisories](https://github.com/advisories)
- [CVE Database](https://cve.mitre.org/)
- [NIST NVD](https://nvd.nist.gov/)

## 📚 Recursos de Seguridad

### Estándares que Seguimos
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)
- [ISO 27001](https://www.iso.org/isoiec-27001-information-security.html)
- [CWE/SANS Top 25](https://cwe.mitre.org/top25/)

### Guías de Implementación
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [Google Engineering Practices](https://google.github.io/eng-practices/)
- [Microsoft Security Development Lifecycle](https://www.microsoft.com/en-us/securityengineering/sdl)

## 🤝 Compromiso

Nos comprometemos a:

- ✅ Responder rápidamente a reportes de seguridad
- ✅ Trabajar con investigadores de buena fe
- ✅ No tomar acciones legales contra quienes reporten responsablemente
- ✅ Acreditar públicamente a quienes descubran vulnerabilidades (si lo desean)
- ✅ Mantener transparencia sobre vulnerabilidades encontradas
- ✅ Mejorar continuamente nuestros procesos de seguridad

## 📞 Contacto

Para reportes de seguridad:
- **Email**: support@aloycmexico.net
- **PGP Key**: [Disponible en servidor de claves públicas]
- **Respuesta esperada**: 48 horas

Para preguntas generales de seguridad:
- **GitHub Discussions**: [Categoría de Seguridad](https://github.com/aloycmexico/vibe-coding-contracts/discussions/categories/security)
- **Email**: support@aloycmexico.net

---

**Última actualización**: Junio 2026
**Próxima revisión**: Diciembre 2026

Gracias por ayudar a mantener este framework seguro para todos. 🛡️
