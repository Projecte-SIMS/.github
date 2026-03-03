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
| **Backend (Laravel)** | [../project-sims-backend/README.md](../project-sims-backend/README.md) | [../project-sims-backend/docs/](../project-sims-backend/docs/) |
| **Frontend (Vue)** | [../project-sims-frontend/README.md](../project-sims-frontend/README.md) | [../project-sims-frontend/docs/](../project-sims-frontend/docs/) |
| **IoT (Raspberry Pi)** | [../Raspberry_py/README.md](../Raspberry_py/README.md) | [../Raspberry_py/ESTADO_SUBSISTEMA_IOT.md](../Raspberry_py/ESTADO_SUBSISTEMA_IOT.md) |

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
| Frontend | Vue + TypeScript | 3.5.x / 5.x |
| CSS | TailwindCSS | 4.x |
| Mapas | Leaflet | 1.9.4 |
| IoT Server | FastAPI (Python) | 3.9+ |
| BD Relacional | PostgreSQL | 15 |
| BD NoSQL | MongoDB Atlas | - |
| Auth | Laravel Sanctum | 4.x |
| RBAC | Spatie Permission | 6.x |

---

## Estado del Proyecto

### ✅ Completado (100%)

| Funcionalidad | Backend | Frontend | IoT |
|---------------|---------|----------|-----|
| Autenticación (login/registro) | ✅ | ✅ | - |
| Sistema RBAC (3 roles, 15+ permisos) | ✅ | ✅ | - |
| CRUD Usuarios | ✅ | ✅ | - |
| CRUD Vehículos | ✅ | ✅ | - |
| CRUD Roles/Permisos | ✅ | ✅ | - |
| Sistema de Reservas | ✅ | ✅ | - |
| Sistema de Tickets | ✅ | ✅ | - |
| Chatbot con IA (Gemini) | ✅ | ✅ | - |
| Mapas con Leaflet | ✅ | ✅ | - |
| Mapa público sin auth | ✅ | ✅ | - |
| Control IoT (on/off) | ✅ | ✅ | ✅ |
| Telemetría GPS | ✅ | ✅ | ✅ |
| Rate Limiting | ✅ | - | - |
| Tests automatizados | ✅ (14+) | - | - |
| Docker | ✅ | ✅ | ✅ |
| Landing page pública | ✅ | - | - |
| Imágenes por modelo de vehículo | ✅ | ✅ | - |
| Distancia a ubicación del usuario | - | ✅ | - |

### ⚠️ Pendiente / Mejoras Futuras

| Tarea | Prioridad | Descripción |
|-------|-----------|-------------|
| Laravel Telescope | Media | Monitorización de requests y queries |
| Sentry | Media | Error tracking en producción |
| SSL/TLS WebSocket | Media | Seguridad en comunicación IoT |
| OpenAPI/Swagger | Baja | Documentación interactiva de API |
| Tests E2E Frontend | Baja | Tests con Cypress o Playwright |
| PWA | Baja | Aplicación web progresiva |

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
| Públicos | 4 | login, register, public map, landing |
| Cliente | 25+ | perfil, vehículos, reservas, tickets, chatbot |
| Admin | 30+ | CRUD completo, comandos IoT, health checks |

Ver detalles en: [../project-sims-backend/docs/API_ENDPOINTS.md](../project-sims-backend/docs/API_ENDPOINTS.md)

---

## Componentes Verificados

**Backend (Laravel 12.x):**
- 12 controladores (8 principales + 4 API)
- 7 modelos (User, Vehicle, Rental, Ticket, TicketMessage, Role, Permission)
- 5 policies
- 4 form requests
- 1 service (VehicleLocationService)
- 6 seeders
- 14+ tests

**Frontend (Vue 3.x):**
- 6 módulos (admin, auth, bookings, common, map, tickets)
- 58 componentes Vue
- 2 layouts (AdminLayout, AuthLayout)
- 2 servicios API (api.ts, authService.ts)
- Composables (useMap, useGeolocation)

**IoT (FastAPI):**
- 1 servidor WebSocket/REST (main.py)
- 1 agente Raspberry Pi
- 5 endpoints
- Telemetría: GPS, motor, batería

---

## Ubicación de Archivos Importantes

```
SIMS_SPRINT4/
├── profile/
│   └── readme.md              # Este archivo
├── project-sims-backend/
│   ├── README.md              # Documentación backend
│   ├── docs/                  # Docs detalladas
│   │   └── API_ENDPOINTS.md   # Referencia de endpoints
│   ├── public/logo.png        # Logo del proyecto
│   └── .env                   # Configuración
├── project-sims-frontend/
│   ├── README.md              # Documentación frontend
│   ├── docs/                  # Docs detalladas
│   └── public/logo.png        # Logo del proyecto
└── Raspberry_py/
    ├── README.md              # Documentación IoT
    ├── ESTADO_SUBSISTEMA_IOT.md # Estado detallado
    ├── server/                # Servidor FastAPI
    └── agent/                 # Agente Raspberry Pi
```

---

## Licencia

EUPL v1.2 (European Union Public Licence)

---

**Equipo de Desarrollo SIMS**  
*Última actualización: 2026-03-03*

