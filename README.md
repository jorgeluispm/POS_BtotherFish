# 🐟 Brother's Fish POS — Sistema Punto de Venta Unificado

Sistema integral Punto de Venta (POS) diseñado para la gestión de ventas, control de inventario, turnos de caja chica y auditoría multi-sucursal. Desarrollado con **NestJS v11** en el backend, un frontend liviano en **Vanilla JavaScript** integrado mediante archivos estáticos, y persistencia de datos en **PostgreSQL (Supabase)**.

---

## 🚀 Arquitectura del Proyecto

El proyecto utiliza una arquitectura **monolítica unificada**: el servidor de NestJS no solo expone la API REST sino que también sirve los activos estáticos del cliente web a través de `@nestjs/serve-static`, permitiendo el despliegue en un único puerto/dominio.

BF/
├── backend/
│   ├── public/                 # Frontend Estático
│   │   ├── assets/
│   │   │   ├── css/            # Estilos de la aplicación
│   │   │   ├── img/            # Recursos visuales
│   │   │   └── js/
│   │   │       ├── api.js      # Cliente HTTP centralizado
│   │   │       └── script.js   # Lógica e interacción del cliente
│   │   └── index.html          # Interfaz principal
│   ├── src/                    # Backend NestJS
│   │   ├── audit/              # Registro de trazabilidad y auditoría
│   │   ├── auth/               # Autenticación JWT y control de acceso
│   │   ├── branches/           # Gestión de sucursales
│   │   ├── cash-register/      # Apertura/cierre de caja y movimientos
│   │   ├── categories/         # Catálogo de categorías
│   │   ├── products/           # Productos y variantes
│   │   ├── reports/            # Generación de reportes
│   │   ├── sales/              # Procesamiento de ventas y pedidos
│   │   ├── users/              # Gestión de usuarios y roles
│   │   ├── app.module.ts       # Módulo principal de la aplicación
│   │   └── main.ts             # Punto de entrada de la aplicación
│   └── tsconfig.json           # Configuración del compilador TypeScript


---

## 🛠️ Tecnologías Utilizadas

- **Backend:** Node.js, NestJS (v11), TypeScript.
- **Base de Datos & ORM:** PostgreSQL (Supabase Pooler), TypeORM.
- **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+ Modules).
- **Servidor Estático:** `@nestjs/serve-static`.
- **Seguridad & Validación:** JWT (JSON Web Tokens), `class-validator`, `class-transformer` (ValidationPipe global).

---

## 🔑 Credenciales de Prueba & Claves de Acceso

Para realizar pruebas de la aplicación en entorno local, puedes utilizar los siguientes usuarios y claves de autorización:

| Usuario | Rol / Permisos | Contraseña |
| :--- | :--- | :--- |
| `root` | Administrador / Acceso Total | `AdminPassword123!` |
| `cajero_real` | Cajero / Operación POS | `AdminPassword123!` |

* **PIN de Operaciones Sensibles (+Nuevo Artículo):** `9216`

---

## 📋 Funcionalidades Principales

1. **Autenticación y Sesiones:**
   - Inicio de sesión seguro mediante Tokens JWT.
   - Manejo de roles de usuario y asignación a sucursales.

2. **Gestión de Caja Chica (`Cash Shifts`):**
   - Apertura y cierre de turnos de caja por sucursal.
   - Registro de transacciones/gastos menores durante el turno.
   - Arqueo y cálculo de diferencias en el cierre de turno.

3. **Catálogo de Productos:**
   - Estructura jerárquica de Categorías, Productos y Variantes de producto.
   - Consultas de inventario optimizadas.

4. **Procesamiento de Ventas (`Sales`):**
   - Creación de pedidos y procesamiento de ventas en tiempo real.
   - Soporte para borradores de órdenes (`drafts`).
   - Pagos divididos (*split payments*) y múltiples métodos de pago (`CASH`, `CARD`, etc.).
   - Anulación de órdenes con motivo registrado para auditoría.

---

## ⚙️ Configuración del Entorno

Crea un archivo `.env` dentro del directorio `backend/` con las siguientes variables de entorno:

```env
PORT=3000

# Configuración de Base de Datos (Supabase / PostgreSQL)
DB_HOST=tu-supabase-db-host.supabase.co
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=tu_contraseña_segura
DB_NAME=postgres

# Seguridad JWT
JWT_SECRET=tu_secreto_jwt_super_seguro

📦 Instalación y Ejecución Local
1. Clonar el repositorio e instalar dependencias
Bash
git clone [https://github.com/jorgeluispm/POS_BtotherFish.git](https://github.com/jorgeluispm/POS_BtotherFish.git)
cd BF/backend
npm install
2. Compilar el proyecto
Bash
npm run build
3. Iniciar el servidor en modo desarrollo
Bash
npm run start:dev
4. Acceder a la aplicación
Abre tu navegador e ingresa a:

Plaintext
http://localhost:3000
🔒 Parámetros de Seguridad
Consultas Parametrizadas: Toda interacción con la base de datos se realiza a través de TypeORM para evitar inyecciones SQL.

SSL / TLS: Conexión segura a Supabase mediante SSL/TLS con soporte SNI.

Variables Sensibles: Archivos .env excluidos del control de versiones mediante .gitignore.