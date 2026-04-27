# Arquitectura del Sistema SIMS (SaaS Multitenant)

Este documento detalla la arquitectura técnica del **Sistema Inteligente de Movilidad Sostenible (SIMS)**, diseñado bajo un modelo **SaaS (Software as a Service)** multitenant de alta disponibilidad.

## 1. Visión General
SIMS utiliza una arquitectura de microservicios híbrida. El núcleo de negocio reside en una aplicación PHP/Laravel, mientras que la telemetría de alta frecuencia es gestionada por un servicio especializado en Python/FastAPI.

## 2. Estrategia Multitenant: Aislamiento por Esquemas
SIMS implementa un aislamiento físico a nivel de base de datos utilizando **Esquemas de PostgreSQL**.

### Capas de Datos:
- **Esquema `public` (Landlord):**
  - Tabla `tenants`: Registro de organizaciones, sus planes de Stripe y configuraciones de branding.
  - Tabla `domains`: Asociación de dominios/subdominios personalizados a cada tenant.
- **Esquemas `tenant_{id}` (Inquilinos):**
  - Cada organización dispone de un esquema aislado generado dinámicamente.
  - Contiene: `users`, `vehicles`, `bookings`, `tickets`, `roles` y `permissions`.

## 3. Flujo de Identificación de Contexto (Frontend)
El frontend (Vue 3) resuelve el tenant actual mediante una jerarquía de prioridades:
1.  **URL Query Parameter:** `?tenant=slug` (ej. `https://app.sims.com/login?tenant=acme`).
2.  **Subdominio:** Extracción del subdominio en entornos de producción (ej. `acme.fleetly.com`).
3.  **LocalStorage:** Persistencia del `current_tenant` para mantener la sesión durante recargas.

### Inyección de Identidad (X-Tenant Header)
Todas las peticiones a la API desde rutas de inquilino (`/admin`, `/app`) inyectan automáticamente la cabecera `X-Tenant` mediante un interceptor de Axios.

## 4. Stack Tecnológico
| Capa | Tecnología | Función |
|------|------------|---------|
| **Frontend** | Vue 3 + Vite + TypeScript | SPA reactiva con soporte multitenant. |
| **Backend API** | Laravel 12 + PHP 8.2 | Lógica de negocio, RBAC y gestión de esquemas. |
| **IoT Server** | FastAPI + Python 3.11 | Microservicio de telemetría vía WebSockets. |
| **Bases de Datos** | PostgreSQL 16 + MongoDB Atlas | Datos relacionales (Negocio) + NoSQL (Telemetría). |
| **Infraestructura** | Render (API/IoT) + Vercel (Frontend) | Despliegue CI/CD automatizado. |

## 5. Integración IoT y Telemetría
El sistema IoT desacopla la identidad del hardware de la identidad del negocio:
- **FastAPI:** Gestiona `hardware_id` y almacena telemetría cruda en MongoDB.
- **Laravel:** Vincula el `hardware_id` a un vehículo dentro del esquema de un tenant específico.
- **Seguridad:** Laravel actúa como proxy; solo los usuarios autorizados de un tenant pueden consultar la telemetría de sus propios dispositivos mediante peticiones firmadas al microservicio IoT.

---
*Última actualización: Abril 2026 - Sprint 6 (Chaos & Delivery)*
