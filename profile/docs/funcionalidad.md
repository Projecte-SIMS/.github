# Especificaciones Funcionales (Sprint 6)

SIMS ha evolucionado de un prototipo monousuario a una plataforma SaaS multitenant completa. Este documento detalla las funcionalidades disponibles en la versión Beta actual.

## 1. Núcleo SaaS y Multitenancy
- **Onboarding de Inquilinos:** Registro automatizado de empresas con creación instantánea de base de datos aislada.
- **Gestión de Dominios:** Soporte para múltiples dominios y subdominios por inquilino.
- **Personalización (Branding):** Cada inquilino puede configurar su logotipo, colores corporativos y tipografía desde el panel de administración.

## 2. Gestión de Flota e IoT
- **Mapa en Tiempo Real:** Visualización de vehículos con telemetría en vivo (GPS, batería, estado de bloqueo).
- **Control Remoto:** Apertura y cierre de puertas vía WebSockets desde el dashboard administrativo.
- **Inventario de Vehículos:** Gestión completa de unidades, modelos y estados de mantenimiento.

## 3. Sistema de Pagos (Stripe)
- **Suscripciones de Tenant:** Planes Pro y Enterprise con cobro recurrente.
- **Portal de Facturación:** Los inquilinos pueden gestionar sus métodos de pago y descargar facturas directamente desde la plataforma (vía Stripe Customer Portal).
- **Control de Acceso por Facturación:** Suspensión automática de servicios en caso de impago detectado vía Webhooks.

## 4. Usuarios y Roles
- **SuperAdmin (Landlord):** Control total sobre todos los inquilinos, estadísticas globales y gestión de planes.
- **Admin de Inquilino:** Gestión de su propia flota, usuarios y configuración de empresa.
- **Usuario Final:** Acceso a la aplicación móvil/web para reserva y uso de vehículos.

## 5. Integraciones Completadas
- **Identidad Corporativa:** Integración del manual de estilo de Fleetly en el diseño base.
- **Notificaciones:** Sistema de alertas para eventos críticos (baja batería, vehículo fuera de zona autorizada).

---
*Última actualización: Abril 2026*
