# Manual de Usuario SIMS (Experiencia Multitenant)

Este manual guía a los diferentes perfiles de usuario a través de la plataforma SIMS en su despliegue SaaS.

## 1. Acceso y Roles
SIMS utiliza una autenticación aislada por organización. Asegúrese de acceder mediante el enlace proporcionado por su administrador (ej. `app.fleetly.com/?tenant=demo`).

### Roles del Sistema:
| Rol | Descripción | Alcance |
|-----|-------------|---------|
| **SuperAdmin** | Administrador global del SaaS (Landlord) | Gestión de empresas, planes y facturación global. |
| **Tenant Admin** | Administrador de la organización | Gestión de flota propia, usuarios locales y branding. |
| **Client** | Usuario final (Conductor) | Reserva, uso y control de vehículos de su organización. |
| **Maintenance** | Personal técnico | Acceso a datos de salud de flota y registros de errores. |

## 2. Manual para el Cliente (Usuario Final)
### Reservas y Viajes:
1.  **Localización:** Use el mapa interactivo para encontrar vehículos cercanos. Los marcadores verdes indican disponibilidad.
2.  **Reserva:** Seleccione un vehículo y confirme la reserva. Dispone de **10 minutos** para iniciar el viaje antes de la cancelación automática.
3.  **Control del Vehículo:** Una vez activado, acceda al panel de control para:
    - Ver velocidad y estado de batería en tiempo real.
    - Ejecutar comandos de apertura/cierre (sujeto a cobertura IoT).
4.  **Finalización:** Estacione en una zona autorizada y pulse "Terminar Viaje". El sistema calculará el importe final según su plan.

## 3. Manual para el Administrador de Organización
### Gestión de Flota:
- **Panel de Control:** Resumen visual del estado de la flota (disponibles, en uso, fuera de línea).
- **Inventario:** Alta y baja de vehículos vinculados a dispositivos IoT.
- **Auditoría:** Consulta de registros de comandos y trayectorias históricas.

### Soporte y Tickets:
- Gestión de incidencias reportadas por los usuarios.
- Chatbot de ayuda contextual para resolución rápida de dudas.

## 4. Branding y Personalización
Desde el menú de configuración, los administradores de nivel "Pro" o "Enterprise" pueden:
- Subir el logotipo corporativo.
- Ajustar colores primarios de la interfaz para alinearlos con su identidad de marca.
- Configurar dominios personalizados (ej. `movilidad.tuayuntamiento.es`).

---
*Para soporte técnico avanzado, contacte con el equipo central de SIMS.*
