# Manual de Accesibilidad (WCAG 2.1 AA)

SIMS está comprometido con la inclusión digital. Este documento detalla las medidas adoptadas para garantizar que la plataforma sea accesible para todos los usuarios.

## 1. Estándares de Cumplimiento
El proyecto sigue las pautas **WCAG 2.1 Nivel AA**. Las auditorías se realizan mediante:
- **Lighthouse Accessibility Score:** Objetivo > 95/100.
- **WAVE Web Accessibility Tool:** Para detección de errores de contraste y etiquetas.
- **Navegación por Teclado:** Validación manual de todos los flujos críticos.

## 2. Integración de UserWay
Se ha implementado el widget de accesibilidad de **UserWay** para proporcionar herramientas adicionales a los usuarios:
- **Ajuste de Contraste:** Modos de alto contraste y monocromo.
- **Lector de Pantalla Integrado:** Para facilitar la lectura de contenido dinámico.
- **Tamaño de Texto:** Control granular sobre la tipografía de la aplicación.
- **Resaltado de Enlaces:** Mejora visual de los elementos interactivos.

## 3. Medidas Técnicas Implementadas
- **HTML Semántico:** Uso riguroso de `<header>`, `<main>`, `<footer>`, `<nav>`, `<section>`.
- **Atributos ARIA:** Etiquetas descriptivas en botones iconográficos y estados de carga.
- **Gestión de Foco:** Implementación de "Focus Traps" en modales para evitar que el usuario se pierda al navegar por teclado.
- **Descripciones Alternativas:** Los mapas de flota incluyen una vista de lista alternativa accesible para lectores de pantalla.

## 4. Resultados de la Evaluación (Sprint 6)
| Módulo | Puntuación Lighthouse | Estado |
|--------|----------------------|--------|
| Landing Page | 98 | ✅ Pass |
| Dashboard Administrador | 92 | ⚠️ Mejora en contraste de gráficos |
| Panel de Usuario | 96 | ✅ Pass |
| Onboarding de Tenant | 100 | ✅ Pass |

## 5. Próximos Pasos
- Mejorar el soporte para navegación por voz en el panel de telemetría.
- Implementar atajos de teclado globales para acciones frecuentes (reserva rápida, cerrar sesión).

---
*Última actualización: Abril 2026*
