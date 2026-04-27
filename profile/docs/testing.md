# Estrategia de Testing y Calidad

El proyecto SIMS sigue un enfoque de "Chaos & Delivery" en el Sprint 6, priorizando la estabilidad del sistema bajo carga y la validación de la arquitectura multitenant.

## 1. Automatización de Pruebas (Backend)
Usamos **PHPUnit** para asegurar que la lógica de aislamiento de esquemas funciona correctamente.

### Tipos de Tests:
- **Unitarios:** Validación de cálculos de facturación, validación de datos de telemetría y lógica de modelos.
- **Funcionales (Feature):** Pruebas de endpoints API asegurando que el middleware `tenant.init` cambia correctamente al esquema solicitado.
- **Aislamiento:** Tests que verifican que los datos del Inquilino A no son visibles desde el contexto del Inquilino B.

```bash
# Ejecutar suite de pruebas
docker compose exec backend php artisan test
```

## 2. Testing de Frontend
- **Component Testing:** Validación de componentes Vue 3 de forma aislada.
- **E2E (End-to-End):** Pruebas de flujo de login multitenant (identificación de tenant -> login -> dashboard).
- **Accesibilidad:** Auditorías automatizadas con Lighthouse y validación manual de navegación por teclado.

## 3. CI/CD (GitHub Actions)
El repositorio utiliza workflows automatizados para cada push y pull request:

- **Lint & Style:** Ejecución de `Laravel Pint` (backend) y `ESLint` (frontend) para mantener la consistencia del código.
- **Build & Test:** Ejecución automática de la suite de tests en un entorno Docker efímero.
- **Auto-Deploy:** Si los tests pasan, se despliega automáticamente en Vercel (Frontend) y Render (Backend).

## 4. Auditoría de Seguridad
- **Sanitización de Esquemas:** Validación estricta del nombre del esquema para evitar inyecciones SQL en comandos de sistema.
- **Rate Limiting:** Aplicado por IP y por Tenant para evitar ataques de denegación de servicio.
- **Protección de Rutas:** Middleware `tenant.auth` que verifica la validez del token Sanctum dentro del esquema actual.

## 5. Resultados del Testing de Sprint 6
- **Bugs Corregidos:**
    - Error en el cambio de esquema bajo alta concurrencia.
    - Fuga de tokens de sesión entre dominios de tenant.
    - Fallo en el cálculo de MRR en el dashboard central.
- **Mejoras de Usabilidad:**
    - Feedback inmediato en el registro de nuevos vehículos.
    - Dashboard de administrador más ligero mediante carga perezosa (lazy loading) de gráficos.

---
*Última actualización: Abril 2026*
