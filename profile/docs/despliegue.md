# Manual de Despliegue y Configuración

Este manual describe los pasos necesarios para levantar el ecosistema SIMS completo en entornos locales y de producción.

## 1. Requisitos Previos
- **Docker & Docker Compose** (Recomendado)
- **PHP 8.2+** (Para desarrollo local sin Docker)
- **Node.js 20+** (Para frontend)
- **PostgreSQL 15** (Con soporte de esquemas)
- **MongoDB** (Para telemetría)

## 2. Levantamiento con Docker (Recomendado)
El proyecto usa el `docker-compose.yml` de la raíz para levantar backend, frontend y bases de datos.
Los compose históricos se movieron a `docs/legacy/docker-compose/`.

```bash
# 1. Clonar el repositorio y entrar en la raíz
cd SIMS_SPRINT4

# 2. Levantar contenedores
docker compose up -d --build

# 3. Configurar Backend
docker exec sims-backend composer install
docker exec sims-backend php artisan key:generate
docker exec sims-backend php artisan migrate --seed # Migra el Landlord (Central)

# 4. Configurar Frontend
cd project-sims-frontend
npm install
npm run dev
```

## 3. Configuración de Variables de Entorno (.env)

### Backend (`project-sims-backend/.env`)
```env
DB_CONNECTION=pgsql
DB_HOST=db
DB_PORT=5432
DB_DATABASE=sims_central
DB_USERNAME=admin
DB_PASSWORD=secret

STRIPE_KEY=pk_test_...
STRIPE_SECRET=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

### Frontend (`project-sims-frontend/.env`)
```env
VITE_API_URL=http://localhost:8000/api
VITE_CENTRAL_DOMAIN=localhost:5173
```

## 4. Gestión de Inquilinos (Tenants)
Para crear el inquilino inicial de prueba (demo):

```bash
# Ejecutar el seeder central (Landlord)
docker exec sims-backend php artisan db:seed --class=CentralSeeder
```

Este comando:
1. Crea la entrada en la tabla `tenants` (ID: `demo`).
2. Crea el esquema `tenant_demo` en PostgreSQL.
3. El paquete `stancl/tenancy` dispara automáticamente la creación del esquema y las migraciones necesarias.

Para ejecutar migraciones en todos los inquilinos existentes:
```bash
docker exec sims-backend php artisan tenants:migrate
```

## 5. Despliegue en Producción
- **Frontend:** Desplegado en **Vercel** (Conexión automática con GitHub).
- **Backend:** Desplegado en **Render** (Usando `Dockerfile` y PostgreSQL gestionado).
- **IoT Server:** Desplegado en **Render** (Conexión a MongoDB Atlas).

---
*Última actualización: Abril 2026*
