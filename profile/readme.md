# SIMS – Sistema Intel·ligent de Mobilitat Sostenible  
**Versión:** Sprint 5 – IoT Integration & Multi-Arch  
**Fecha:** 2026-03-04  
**Última revisión:** 2026-03-04

---

## 🚀 Arquitectura de Despliegue Unificada (Docker)

El proyecto SIMS ahora cuenta con una orquestación completa mediante **Docker Compose** en la raíz del repositorio. Esto permite levantar todo el ecosistema con un único comando.

### Requisitos Previos
- Docker Desktop 4.x+
- Docker Compose v2.x+

### Inicio Rápido (Todo el Sistema)
Para levantar todos los servicios en modo desarrollo:

```bash
# 1. Situarse en la raíz del proyecto
# 2. Levantar todos los contenedores
docker compose up -d --build

# 3. Inicializar la base de datos y cargar datos de prueba
docker exec sims-backend php artisan migrate:fresh --seed
```

### Servicios y Puertos
| Servicio | Contenedor | Puerto Local | Descripción |
|----------|------------|--------------|-------------|
| **Frontend** | `sims-frontend` | [5173](http://localhost:5173) | Vue 3 + Vite (HMR activo) |
| **Backend** | `sims-backend` | [8000](http://localhost:8000) | Laravel 12 API |
| **Base de Datos**| `sims-db` | 5432 | PostgreSQL 15 |
| **IoT Server** | `sims-iot-server` | [8001](http://localhost:8001) | FastAPI (Raspberry_py) |

---

## Descripción General

SIMS es una plataforma integral para la gestión y monitorización de movilidad sostenible (carsharing eléctrico). Integra sensores IoT, un backend robusto y un frontend web para usuarios y administradores.

---

## Repositorios del Proyecto

| Componente | Repositorio | Tecnología |
|------------|-------------|------------|
| **Backend** | [Backend](https://github.com/Projecte-SIMS/Backend) | Laravel (PHP) |
| **Frontend** | [Frontend](https://github.com/Projecte-SIMS/Frontend) | Vue + TypeScript |
| **IoT** | [IoT](https://github.com/Projecte-SIMS/IoT) | FastAPI (Python) |
| **Profile** | Este repositorio | Documentación general |

---

## Documentación por Componente

| Componente | README | Documentación Detallada |
|------------|--------|-------------------------|
| **Backend (Laravel)** | [README.md](https://github.com/Projecte-SIMS/Backend/blob/develop/README.md) | [docs/](https://github.com/Projecte-SIMS/Backend/tree/develop/docs) |
| **Frontend (Vue)** | [README.md](https://github.com/Projecte-SIMS/Frontend/blob/develop/README.md) | [docs/](https://github.com/Projecte-SIMS/Frontend/tree/develop/docs) |
| **IoT (Raspberry Pi)** | [README.md](https://github.com/Projecte-SIMS/IoT/blob/main/README.md) | [ESTADO_SUBSISTEMA_IOT.md](https://github.com/Projecte-SIMS/IoT/blob/main/ESTADO_SUBSISTEMA_IOT.md) |

### Manual de Usuario

**[Manual de Usuario por Rol](https://github.com/Projecte-SIMS/Frontend/blob/develop/docs/MANUAL_USUARIO.md)** - Guía completa de uso del sistema para:
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

## Estado del Proyecto (Sprint 5)

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
| Vinculación Dinámica IoT | ✅ | ✅ | ✅ |
| Telemetría GPS Real-time | ✅ | ✅ | ✅ |
| Docker Multi-Arch (M1/M2/M3) | ✅ | ✅ | ✅ |
| Tests automatizados | ✅ (51+) | - | - |

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
| Admin | 40+ | CRUD completo, comandos IoT, vinculación |

Ver detalles en: [API_ENDPOINTS.md](https://github.com/Projecte-SIMS/Backend/blob/develop/docs/API_ENDPOINTS.md)

---

## Análisis de Cumplimiento del Sprint 5

### ✅ 1. Backend (Entorn servidor)

#### 1.1 API (Laravel)
| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Endpoints de vinculación IoT implementados | ✅ Completado | `POST /admin/iot/devices/{id}/link` operativo |
| Endpoints correctamente conectados al front-end | ✅ Completado | Integración completa en consola de control |
| Validaciones de matrícula y formato | ✅ Completado | Form Requests + Regex para matrículas |
| Respuestas HTTP correctas (status codes) | ✅ Completado | 200, 201, 400, 401, 403, 404, 422, 500 |

#### 1.2 Calidad del código
| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Código documentado con comentarios | ✅ Completado | Controladores y Servicios actualizados |
| Estructura limpia y mantenible | ✅ Completado | Refactorización de VehicleLocationService |
| Eliminación de código obsoleto | ✅ Completado | Eliminado uso de `image_url` en favor de `getVehicleImage` |

#### 1.3 Tests e Integración
| Requisito | Estado | Observaciones |
|-----------|--------|---------------|
| Tests automatizados implementados | ✅ Completado | 51+ tests en PHPUnit |
| Soporte Multi-Arch Docker | ✅ Completado | Imágenes AMD64 y ARM64 generadas en CI/CD |
| GitHub Actions optimizado | ✅ Completado | Release automática de imágenes .tar |

---

### Resumen de Cumplimiento General

| Categoría | Completado | Total | Porcentaje |
|-----------|------------|-------|------------|
| 1. Backend API | 8 | 8 | 100% |
| 2. Frontend (Vue 3) | 6 | 6 | 100% |
| 3. Sistema IoT | 10 | 10 | 100% |
| 4. Sistema Ayuda IA | 4 | 4 | 100% |
| 5. Despliegue Docker | 5 | 5 | 100% |
| 6. Documentación | 8 | 8 | 100% |
| **TOTAL** | **41** | **41** | **100%** |

---

## Licencia

EUPL v1.2 (European Union Public Licence)

---

**Equipo de Desarrollo SIMS**  
*Última actualización: 2026-03-04*
