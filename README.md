# CampusHub Backend (Node.js)

Este es el servidor del proyecto CampusHub, desarrollado con **Node.js**, **Express** y **MySQL**. Proporciona una API RESTful para la gestión de usuarios, proyectos y catálogos educativos.

## Tecnologías Utilizadas

- **Node.js**: Entorno de ejecución para el servidor.
- **Express**: Framework web para la creación de la API.
- **MySQL**: Base de datos relacional (gestionada con la librería `mysql2`).
- **Bcrypt**: Para el cifrado seguro de contraseñas.
- **UUID**: Generación de tokens únicos para sesiones de usuario.
- **Cors**: Manejo de políticas de origen cruzado para la comunicación con el frontend.
- **Dotenv**: Gestión de variables de entorno.

## Estructura del Proyecto

```text
NODE/
├── .env                # Variables de entorno (puerto, credenciales BD, etc.)
├── db.js               # Configuración inicial del pool de conexiones
├── server.js           # Punto de entrada principal del servidor
├── package.json        # Dependencias y scripts del proyecto
└── src/
    ├── controllers/    # Lógica de control para cada entidad
    ├── db/             # Gestión detallada del pool de conexiones
    ├── middleware/     # Middlewares (ej. autenticación)
    ├── models/         # Consultas SQL organizadas por modelos de datos
    ├── routes/         # Definición de endpoints de la API
    ├── sql/            # Esquema de la base de datos (schema.sql)
    └── utils/          # Funciones de utilidad (ej. hashing)
```

## Configuración e Instalación

1. **Instalar dependencias**:
   Desde la carpeta `NODE`, ejecuta:

   ```bash
   npm install
   ```

2. **Configurar base de datos**:

   - Asegúrate de tener un servidor MySQL funcionando (ej. XAMPP).
   - Crea la base de datos (por defecto `proyecto_integrado`).
   - Importa el archivo SQL ubicado en `src/sql/schema.sql`.

3. **Variables de Entorno**:
   Crea o edita el archivo `.env` en la raíz de la carpeta `NODE` con el siguiente formato:
   ```env
   PORT=3000
   DB_HOST=localhost
   DB_USER=root
   DB_PASS=
   DB_NAME=proyecto_integrado
   JWT_SECRET=tu_secreto_aqui
   ```

## Ejecución del Servidor

- **Producción**:
  ```bash
  npm start
  ```
- **Desarrollo (con recarga automática)**:
  ```bash
  npm run dev
  ```

## Endpoints Principales

### Usuarios

- `POST /api/users/register`: Registro de nuevos usuarios.
- `POST /api/users/login`: Autenticación y obtención de token.

### Proyectos

- `GET /api/projects`: Listado público de proyectos.
- `POST /api/projects`: Creación de proyecto (requiere token).
- `PUT /api/projects/:id`: Edición de proyecto (requiere token y ser miembro).

### Relaciones y Catálogos

- `GET /api/relations/users/:tokken/projects`: Ver proyectos de un usuario.
- `GET /api/centros`, `GET /api/titulos`, etc.: Listado de catálogos educativos.
- `POST /api/relations/assign-project`: Vincular usuario a proyecto.

---

**Nota**: Todas las rutas protegidas requieren el encabezado `Authorization: Bearer <token>`.
