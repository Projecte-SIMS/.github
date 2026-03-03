# SIMS – Sistema Intel·ligent de Mobilitat Sostenible  
**Versión:** Sprint 4 – First Deployment  
**Fecha:** 2026-03-03  
**Última revisión:** 2026-03-03

---

## Descripción General

SIMS es una plataforma integral para la gestión y monitorización de movilidad sostenible (carsharing eléctrico). Integra sensores IoT, un backend robusto y un frontend web para usuarios y administradores.

---

## 🗂️ Repositorios del Proyecto

| Componente | Repositorio | Tecnología |
|------------|-------------|------------|
| **Backend** | [Backend](https://github.com/Projecte-SIMS/Backend) | Laravel (PHP) |
| **Frontend** | [Frontend](https://github.com/Projecte-SIMS/Frontend) | Vue + TypeScript |
| **IoT** | [IoT](https://github.com/Projecte-SIMS/IoT) | FastAPI (Python) |
| **Profile** | Este repositorio | Documentación general |

---

## 📚 Documentación por Componente

| Componente | README | Documentación Detallada |
|------------|--------|-------------------------|
| **Backend (Laravel)** | [README.md](https://github.com/Projecte-SIMS/Backend/blob/main/README.md) | [docs/](https://github.com/Projecte-SIMS/Backend/tree/main/docs) |
| **Frontend (Vue)** | [README.md](https://github.com/Projecte-SIMS/Frontend/blob/main/README.md) | [docs/](https://github.com/Projecte-SIMS/Frontend/tree/main/docs) |
| **IoT (Raspberry Pi)** | [README.md](https://github.com/Projecte-SIMS/IoT/blob/main/README.md) | [ESTADO_SUBSISTEMA_IOT.md](https://github.com/Projecte-SIMS/IoT/blob/main/ESTADO_SUBSISTEMA_IOT.md) |

### 📖 Manual de Usuario

**[Manual de Usuario por Rol](https://github.com/Projecte-SIMS/Frontend/blob/main/docs/MANUAL_USUARIO.md)** - Guía completa de uso del sistema para:
- Usuarios (Clientes)
- Administradores
- Personal de Mantenimiento

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

Ver detalles en: [API_ENDPOINTS.md](https://github.com/Projecte-SIMS/Backend/blob/main/docs/API_ENDPOINTS.md)

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
# En cada repositorio:

Backend/
├── README.md              # Documentación backend
├── docs/                  # Docs detalladas
│   └── API_ENDPOINTS.md   # Referencia de endpoints
├── public/logo.png        # Logo del proyecto
└── .env                   # Configuración

Frontend/
├── README.md              # Documentación frontend
├── docs/                  # Docs detalladas
│   └── MANUAL_USUARIO.md  # Manual por rol
└── public/logo.png        # Logo del proyecto

IoT/
├── README.md              # Documentación IoT
├── ESTADO_SUBSISTEMA_IOT.md # Estado detallado
├── server/                # Servidor FastAPI
└── agent/                 # Agente Raspberry Pi
```

---

## 📋 Análisis de Cumplimiento del Sprint

### ✅ 1. Backend (Entorn servidor)

#### 1.1 API (Laravel)
| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Endpoints necesarios completamente implementados | ✅ Completado | 60+ endpoints (públicos, cliente, admin) |
| Endpoints correctamente conectados al front-end | ✅ Completado | Integración completa con Vue |
| Validaciones implementadas | ✅ Completado | Form Requests + validaciones inline |
| Respuestas HTTP correctas (status codes) | ✅ Completado | 200, 201, 400, 401, 403, 404, 422, 500 |
| Manejo de errores controlado | ✅ Completado | Try-catch + respuestas JSON estructuradas |

#### 1.2 Calidad del código
| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Código documentado con comentarios | ✅ Completado | Comentarios en controladores y servicios |
| Estructura limpia y mantenible | ✅ Completado | MVC + Services + Policies |
| Refactorización realizada | ✅ Completado | VehicleLocationService extraído |
| Eliminación de código duplicado | ✅ Completado | Seeders y migraciones limpiados |

#### 1.3 Tests
| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Tests automatizados implementados | ✅ Completado | 14+ tests en PHPUnit |
| Tests unitarios | ✅ Completado | AuthControllerTest, VehicleControllerTest, etc. |
| Tests de integración | ✅ Completado | Tests de API completos |
| Tests ejecutándose sin errores | ✅ Completado | `php artisan test` pasa |

#### 1.4 Debug y monitorización
| Herramienta | Estado | Uso |
|-------------|--------|-----|
| **Xdebug** | ⚠️ Disponible | Depuración paso a paso en PHP |
| **Laravel Telescope** | ❌ Pendiente | Monitorización de requests/queries |
| **Sentry** | ❌ Pendiente | Error tracking en producción |
| **Chrome DevTools** | ✅ En uso | Depuración de red y consola |
| **Laravel TestTools** | ✅ En uso | Extensión Chrome para testing API |

**Justificación de herramientas:**
- **Xdebug**: Herramienta esencial para depuración de PHP, permite breakpoints y inspección de variables
- **Chrome DevTools**: Imprescindible para depurar llamadas API y errores de frontend
- **Laravel TestTools**: Facilita probar endpoints directamente desde el navegador
- **Telescope/Sentry**: Pendientes para producción, no críticos en desarrollo

---

### ✅ 2. Frontend

| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Integración completa con la API | ✅ Completado | axios + interceptores + manejo de tokens |
| Manejo correcto de errores del backend | ✅ Completado | Toast notifications + mensajes específicos |
| Interfaz usable y coherente | ✅ Completado | TailwindCSS + tema oscuro profesional |
| Flujo funcional completo por tipo de usuario | ✅ Completado | Client, Admin, Maintenance |

---

### ✅ 3. Sistema de ayuda (Chatbot RAG)

| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Chatbot tipo RAG implementado | ✅ Completado | Integrado con API Gemini |
| Alimentado con documentación propia | ✅ Completado | Contexto del sistema SIMS en cada consulta |
| Utilizando API de IA | ✅ Completado | Google Gemini API |
| Respuestas según el rol | ✅ Completado | El contexto incluye rol del usuario |

**Roles cubiertos:**
| Rol | Ayuda contextual | Estado |
|-----|------------------|--------|
| Admin (SuperAdmin) | ✅ | Acceso a todas las funcionalidades |
| Client (Usuario final) | ✅ | Reservas, vehículos, tickets |
| Maintenance (Worker) | ✅ | Gestión de vehículos |

**Funcionalidades del chatbot:**
- Responde preguntas sobre el sistema SIMS
- Ayuda con reservas y gestión de vehículos
- Proporciona información de tickets y soporte
- Interfaz conversacional en `/chatbot`

---

### ✅ 4. Despliegue

| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Aplicación desplegada | ⚠️ Preparada | Docker Compose configurado |
| Backend accesible | ✅ Local | Puerto 8000 + landing page pública |
| Base de datos configurada | ✅ Completado | PostgreSQL + MongoDB Atlas |
| Variables de entorno definidas | ✅ Completado | .env.example documentado |
| Funcionando fuera de local | ⚠️ Pendiente | Requiere servidor de producción |

**Docker disponible para:**
- Backend Laravel: `docker-compose.yml`
- Frontend Vue: Configuración lista
- IoT FastAPI: `docker-compose.yml` con MongoDB

---

### ✅ 5. Documentación

| Requisito | Estado | Ubicación |
|-----------|--------|-----------|
| Explicación de arquitectura | ✅ Completado | Este README + diagramas |
| Explicación del modelo de BD | ✅ Completado | [DATABASE.md](https://github.com/Projecte-SIMS/Backend/blob/main/docs/DATABASE.md) |
| Explicación de endpoints | ✅ Completado | [API_ENDPOINTS.md](https://github.com/Projecte-SIMS/Backend/blob/main/docs/API_ENDPOINTS.md) |
| Justificación técnica | ✅ Completado | READMEs de cada repositorio |
| Explicación del sistema de IA | ✅ Completado | ChatbotController documentado |
| Explicación de testing/debugging | ✅ Completado | Sección 1.4 de este documento |
| Manual básico de uso por rol | ✅ Completado | [MANUAL_USUARIO.md](https://github.com/Projecte-SIMS/Frontend/blob/main/docs/MANUAL_USUARIO.md) |

---

### 📊 Resumen de Cumplimiento

| Categoría | Completado | Total | Porcentaje |
|-----------|------------|-------|------------|
| 1. Backend API | 5 | 5 | 100% |
| 1. Backend Calidad | 4 | 4 | 100% |
| 1. Backend Tests | 4 | 4 | 100% |
| 1. Backend Debug | 3 | 5 | 60% |
| 2. Frontend | 4 | 4 | 100% |
| 3. Sistema Ayuda | 4 | 4 | 100% |
| 4. Despliegue | 4 | 5 | 80% |
| 5. Documentación | 7 | 7 | 100% |
| **TOTAL** | **35** | **38** | **92%** |

### ❌ Tareas Pendientes

| Tarea | Prioridad | Estimación | Descripción |
|-------|-----------|------------|-------------|
| Laravel Telescope | Media | 2h | Instalar y configurar monitorización |
| Sentry | Media | 2h | Integrar error tracking |
| Despliegue producción | Alta | 4h | Subir a servidor real accesible |

### ✅ Funcionalidades Extra Implementadas

| Funcionalidad | Descripción |
|---------------|-------------|
| Landing page pública | Página de bienvenida con tema oscuro profesional |
| Imágenes por modelo de vehículo | Tesla, Nissan, Renault, BMW, Volkswagen |
| Distancia a ubicación del usuario | Cálculo real de distancia GPS |
| Mapa centrado en ubicación | Geolocalización del usuario |
| Sistema de tickets completo | Creación, mensajes, estados |
| Rate limiting | Protección contra abuso de API |
| RBAC completo | 3 roles con 15+ permisos |

---

## Licencia

EUPL v1.2 (European Union Public Licence)

---

**Equipo de Desarrollo SIMS**  
*Última actualización: 2026-03-03*

