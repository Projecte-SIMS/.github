# Registro de Decisiones Arquitectónicas (ADR)

Este documento registra las decisiones técnicas críticas tomadas durante el desarrollo de SIMS Sprint 6.

## ADR 001: Aislamiento por Esquemas de PostgreSQL
*   **Estado:** Aceptado
*   **Contexto:** Necesitamos gestionar múltiples organizaciones garantizando que los datos no se mezclen.
*   **Decisión:** Usar esquemas (`tenant_1`, `tenant_2`) en lugar de bases de datos físicas separadas.
*   **Consecuencia:** Simplifica el mantenimiento y reduce costes en hosting, manteniendo un aislamiento fuerte.

## ADR 002: Identificación de Tenant vía X-Tenant Header
*   **Estado:** Aceptado
*   **Contexto:** La API debe saber a qué esquema conectarse en cada petición.
*   **Decisión:** Exigir la cabecera `X-Tenant` en todas las peticiones a rutas de inquilino.
*   **Consecuencia:** Permite una identificación rápida y cacheable en el middleware.

## ADR 003: Almacenamiento de Telemetría en MongoDB
*   **Estado:** Aceptado
*   **Contexto:** Los datos de GPS llegan cada pocos segundos desde múltiples vehículos.
*   **Decisión:** Usar MongoDB para telemetría y PostgreSQL para negocio.
*   **Consecuencia:** Evita la degradación del rendimiento de la DB relacional por inserciones masivas.

## ADR 004: Implementación de Accesibilidad WCAG 2.1 AA
*   **Estado:** Aceptado
*   **Contexto:** El sistema debe ser usable por personas con discapacidad para cumplir normativas.
*   **Decisión:** Implementar HTML semántico, control de foco mediante HeadlessUI y el widget de UserWay.
*   **Consecuencia:** Mejora la usabilidad general y cumple con estándares legales europeos.

## ADR 005: Integración de Stripe Checkout (Server-side)
*   **Estado:** Aceptado
*   **Contexto:** Necesitamos un sistema de cobro seguro para el modelo SaaS.
*   **Decisión:** Delegar la captura de tarjetas a Stripe Checkout mediante sesiones generadas en el backend.
*   **Consecuencia:** Cumplimiento PCI-DSS automático y reducción de responsabilidad legal sobre datos bancarios.

---
*Última actualización: Abril 2026*
