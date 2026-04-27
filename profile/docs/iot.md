# Subsistema IoT y Telemetría

SIMS integra un ecosistema de telemetría diseñado para escalar en entornos multitenant.

## 1. Arquitectura de Datos (MongoDB)
La telemetría de alta frecuencia se almacena en **MongoDB Atlas** para evitar cuellos de botella en la base de datos relacional.

### Modelo de Documento (`vehicle_locations`):
```json
{
  "identity": {
    "hardware_id": "raspi-abcd1234",
    "license_plate": "1234ABC"
  },
  "status": { "online": true, "active": false },
  "telemetry": {
    "latitude": 41.3851,
    "longitude": 2.1734,
    "speed": 45.5,
    "engine_temp": 85.0,
    "rpm": 2500,
    "battery_voltage": 12.6
  },
  "meta": { "relays": { "0": false } }
}
```

## 2. Agente IoT (Raspberry Pi)
El software del agente está diseñado para la resiliencia en entornos de movilidad.
- **Transmisión:** WebSockets (WSS) cada 5 segundos.
- **Reconexión:** Implementa **Backoff Exponencial** (5s -> 7.5s -> ... -> 60s) para gestionar pérdidas de cobertura.
- **Verificación de Red:** Comprueba conectividad IP antes de intentar el handshake del WebSocket.

## 3. Comandos Remotos Multitenant
El flujo de un comando (ej. "Abrir vehículo") garantiza la seguridad por organización:
1.  **Validación:** Laravel verifica que el dispositivo pertenezca al esquema del tenant actual.
2.  **Proxy:** Laravel firma una petición `POST` hacia el microservicio FastAPI.
3.  **Transmisión:** FastAPI envía el comando al socket persistente de la Raspberry Pi específica.
4.  **Trazabilidad:** La acción se registra en la tabla `command_logs` del **esquema del inquilino** en PostgreSQL.

## 4. Configuración del Entorno IoT
### Variables Críticas del Agente (`.env`):
- `DEVICE_ID`: Identificador único (auto-detectado por Serial de CPU si está vacío).
- `TENANT_ID`: Slug de la organización propietaria.
- `SERVER_WS`: URL del microservicio (ej. `wss://sims-iot.onrender.com`).
- `RELAY0_PIN`: Pin GPIO físico (por defecto 17).

## 5. Endpoints de Telemetría (Tenant-Aware)
- `GET /api/iot/devices`: Listado de dispositivos vinculados al inquilino actual.
- `GET /api/iot/devices/{id}`: Telemetría en tiempo real filtrada por contexto.
- `POST /api/admin/iot/devices/{id}/link`: (SuperAdmin) Vinculación de hardware nuevo a un cliente SaaS.

---
*Última actualización: Abril 2026*
