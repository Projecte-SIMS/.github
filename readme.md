# SIMS – Sistema Intel·ligent de Mobilitat Sostenible  
**Versión:** Sprint 5 – First Deployment  
**Fecha:** 2026-03-03  
**Última revisión:** 2026-03-03

---

## Descripción General

SIMS es una plataforma integral para la gestión y monitorización de movilidad sostenible (carsharing eléctrico). Integra sensores IoT, un backend robusto y un frontend web para usuarios y administradores.

---

## Documentación por Componente

| Componente | README | Documentación Detallada |
|------------|--------|-------------------------|
| **Backend (Laravel)** | [project-sims-backend/README.md](project-sims-backend/README.md) | [project-sims-backend/docs/](project-sims-backend/docs/) |
| **Frontend (Vue)** | [project-sims-frontend/README.md](project-sims-frontend/README.md) | [project-sims-frontend/docs/](project-sims-frontend/docs/) |
| **IoT (Raspberry Pi)** | [Raspberry_py/README.md](Raspberry_py/README.md) | [Raspberry_py/ESTADO_SUBSISTEMA_IOT.md](Raspberry_py/ESTADO_SUBSISTEMA_IOT.md) |

---

## Arquitectura General

```
┌─────────────────┐     WebSocket      ┌─────────────────┐
│  Raspberry Pi   │ ◄───────────────► │  FastAPI Server │◄──── MongoDB Atlas
│    (Agentes)    │    Telemetría      │   (Puerto 8001) │
└─────────────────┘    + Comandos      └────────┬────────┘
                                                │
                                                │ HTTP REST + API Key
                                                │
┌─────────────────┐      API REST      ┌────────▼────────┐
│  Vue Frontend   │ ◄───────────────► │  Laravel Backend │──── PostgreSQL
│  (Puerto 5173)  │                    │   (Puerto 8000)  │
└─────────────────┘                    └─────────────────┘
```

---

## Stack Tecnológico

| Componente | Tecnología | Versión |
|------------|------------|---------|
| Backend | Laravel (PHP) | 12.x / 8.2+ |
| Frontend | Vue + TypeScript | 3.5.26 / 5.9.3 |
| CSS | TailwindCSS | 4.1.18 |
| Mapas | Leaflet | 1.9.4 |
| IoT Server | FastAPI (Python) | 3.9+ |
| BD Relacional | PostgreSQL | 15 |
| BD NoSQL | MongoDB Atlas | - |
| Auth | Laravel Sanctum | 4.2 |
| RBAC | Spatie Permission | 6.24 |

---

## Estado del Proyecto

### ✅ Completado (100%)

| Funcionalidad | Backend | Frontend | IoT |
|---------------|---------|----------|-----|
| Autenticación (login/registro) | ✅ | ✅ | - |
| Sistema RBAC (3 roles, 15 permisos) | ✅ | ✅ | - |
| CRUD Usuarios | ✅ | ✅ | - |
| CRUD Vehículos | ✅ | ✅ | - |
| CRUD Roles/Permisos | ✅ | ✅ | - |
| Sistema de Reservas | ✅ | ✅ | - |
| Sistema de Tickets | ✅ | ✅ | - |
| Chatbot con IA | ✅ | ✅ | - |
| Mapas con Leaflet | ✅ | ✅ | - |
| Mapa público sin auth | ✅ | ✅ | - |
| Control IoT (on/off) | ✅ | ✅ | ✅ |
| Telemetría GPS | ✅ | ✅ | ✅ |
| Rate Limiting | ✅ | - | - |
| Tests automatizados | ✅ (51+) | - | - |
| Docker | ✅ | ✅ | ✅ |

### ⚠️ Pendiente / Mejoras

| Tarea | Prioridad |
|-------|-----------|
| Laravel Telescope | Media |
| Sentry (error tracking) | Media |
| SSL/TLS para WebSocket | Media |
| OpenAPI/Swagger | Baja |
| Tests E2E Frontend | Baja |

---

## Inicio Rápido

### Backend
```bash
cd project-sims-backend
cp .env.example .env
docker compose up -d --build
docker compose exec app composer install
docker compose exec app php artisan key:generate
docker compose exec app php artisan migrate --seed
```

### Frontend
```bash
cd project-sims-frontend
npm install
npm run dev
```

### IoT Server
```bash
cd Raspberry_py
cp .env.example server/.env
docker-compose up --build
```

---

## Roles del Sistema

| Rol | Permisos | Descripción |
|-----|----------|-------------|
| **Admin** | Todos | Acceso completo al sistema |
| **Client** | vehicles.view, tickets.*, reservations.* | Usuario final |
| **Maintenance** | vehicles.view, vehicles.manage | Personal técnico |

---

## Endpoints Principales

| Tipo | Cantidad | Documentación |
|------|----------|---------------|
| Públicos | 4 | login, register, health, public map |
| Cliente | 25+ | perfil, vehículos, reservas, tickets, chatbot, IoT |
| Admin | 30+ | CRUD completo, comandos IoT |

Ver detalles en: [project-sims-backend/docs/API_ENDPOINTS.md](project-sims-backend/docs/API_ENDPOINTS.md)

---

## Componentes Verificados

**Backend (Laravel 12.x):**
- 11 controladores
- 7 modelos
- 5 policies
- 4 form requests
- 1 service (VehicleLocationService)
- 8 seeders
- 51+ tests

**Frontend (Vue 3.5.26):**
- 6 módulos
- 30+ páginas
- 15+ componentes
- 2 layouts
- 2 servicios API

**IoT (FastAPI):**
- 1 servidor WebSocket/REST
- 1 agente Raspberry Pi
- 6 endpoints
- Telemetría GPS, motor, batería

---

## Licencia

EUPL v1.2 (European Union Public Licence)

---

**Equipo de Desarrollo SIMS**  
*Última actualización: 2026-03-03*

