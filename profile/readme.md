# SIMS – Sistema Inteligente de Mobilitat Sostenible (SaaS Edition)

**Versión:** Sprint 6 – Chaos & Delivery (Multitenant Architecture)  
**Fecha:** Abril 2026  
**Licencia:** EUPL v1.2

---

## 🚀 Arquitectura de Despliegue Unificada (Docker)

El ecosistema SIMS se orquesta mediante **Docker Compose**, permitiendo levantar el núcleo SaaS, la base de datos multitenant y el servidor IoT con un único flujo de trabajo.

### Inicio Rápido (Entorno Local)
```bash
# 1. Levantar contenedores
docker compose up -d --build

# 2. Inicializar Landlord (Base de datos central)
docker exec sims-backend php artisan migrate --seed

# 3. Crear el tenant de prueba (Demo)
docker exec sims-backend php artisan db:seed --class=CentralSeeder
```

### Servicios y Puertos
| Servicio | Contenedor | Puerto Local | Descripción |
|----------|------------|--------------|-------------|
| **Frontend** | `sims-frontend` | [5173](http://localhost:5173) | Vue 3 + UserWay (Multitenant Aware) |
| **Backend** | `sims-backend` | [8000](http://localhost:8000) | Laravel 12 API (Multitenant Core) |
| **Base de Datos**| `sims-db` | 5432 | PostgreSQL 16 (Aislamiento por Esquemas) |
| **IoT Server** | `sims-iot-server` | [8001](http://localhost:8001) | FastAPI (Telemetría MongoDB) |

---

## 📂 Documentación Técnica Detallada

| Documento | Contenido |
|-----------|-----------|
| [**Manual de Despliegue**](./docs/despliegue.md) | Guía completa de instalación y variables .env. |
| [**Arquitectura SaaS**](./docs/arquitectura.md) | Detalles sobre aislamiento de esquemas y flujo de identificación. |
| [**Manual de Usuario**](./docs/manual_usuario.md) | Guía por roles: SuperAdmin, Tenant Admin y Cliente. |
| [**Accesibilidad (WCAG 2.1)**](./docs/accesibilidad.md) | Implementación de UserWay y auditoría de accesibilidad. |
| [**Subsistema IoT**](./docs/iot.md) | Telemetría en tiempo real y comandos remotos. |

---

## 🏗️ Stack Tecnológico

| Componente | Tecnología | Versión | Rol |
|------------|------------|---------|-----|
| **Backend** | Laravel (PHP) | 12.x / 8.2+ | API Multitenant & Billing (Stripe) |
| **Frontend** | Vue + TypeScript | 3.5.x | UI Reactiva & Personalización Dinámica |
| **IoT Server** | FastAPI (Python) | 3.11+ | Ingesta de Telemetría (MongoDB Atlas) |
| **Pagos** | Stripe API | 2024+ | Gestión de suscripciones y facturación |
| **Accesibilidad**| UserWay Widget | v4.0 | Cumplimiento WCAG 2.1 Nivel AA |

---

## 📊 Estado del Proyecto (Sprint 6: Chaos & Delivery)

### ✅ Completado (100%)

| Funcionalidad | Backend | Frontend | IoT |
|---------------|---------|----------|-----|
| **Arquitectura Multitenant** | ✅ | ✅ | ✅ |
| **Aislamiento de Datos (Schemas)**| ✅ | ✅ | ✅ |
| **Suscripciones Stripe** | ✅ | ✅ | - |
| **Branding Dinámico** | ✅ | ✅ | - |
| **Accesibilidad (UserWay)** | ✅ | ✅ | - |
| **Telemetría Multitenant** | ✅ | ✅ | ✅ |
| **Comandos IoT Firmados** | ✅ | ✅ | ✅ |
| **Tests de Aislamiento** | ✅ | - | - |

---

## 🔐 Roles y Seguridad

| Rol | Alcance | Descripción |
|-----|---------|-------------|
| **SuperAdmin** | Global | Gestión de Tenants, Planes y Facturación Global. |
| **Admin** | Organización | Control de flota propia, Usuarios locales y Branding. |
| **Client** | Personal | Reserva y uso de vehículos de su organización. |
| **Maintenance** | Técnico | Salud de flota y logs de errores IoT. |

---

## 📝 Análisis de Cumplimiento Sprint 6

### 1. Infraestructura SaaS
- [x] Aislamiento de datos mediante esquemas PostgreSQL implementado.
- [x] Identificación de inquilino por cabecera `X-Tenant` y parámetro URL.
- [x] Gestión de dominios y subdominios personalizados.

### 2. Facturación e Identidad
- [x] Integración de Stripe Checkout y Portal de Cliente.
- [x] Sincronización de pagos mediante Webhooks.
- [x] Inyección dinámica de logotipos y colores corporativos.

### 3. Accesibilidad y Calidad
- [x] Integración funcional del widget UserWay en el Frontend.
- [x] Cumplimiento de estándares WCAG 2.1 AA en flujos críticos.
- [x] Cobertura de tests para validación de cambio de esquema.

---

## Licencia
Licenciado bajo la **EUPL v1.2** (European Union Public Licence).

**SIMS Core Team**  
*Última actualización: Abril 2026*
