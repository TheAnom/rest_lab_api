# REST Lab API

Proyecto Jeferson, ruby.

## Instalación y Configuración

1. Clonar el repositorio:
```bash
git clone <url-del-repositorio>
cd rest_lab_api
```

2. Instalar dependencias:
```bash
bundle install
```

3. Configurar la base de datos:
```bash
bin/rails db:migrate
bin/rails db:seed
```

4. Iniciar el servidor:
```bash
bin/rails server
```

La API estará disponible en `http://localhost:3000`

## Endpoints Implementados

### Listar todos los artículos
- **GET** `/api/v1/articles`
- **Respuesta exitosa (200):**
```json
[
  {
    "id": 1,
    "title": "Primer artículo",
    "body": "Contenido de ejemplo suficiente para validar.",
    "created_at": "2025-11-07T02:17:28.660Z",
    "updated_at": "2025-11-07T02:17:28.660Z"
  },
  {
    "id": 2,
    "title": "Segundo artículo", 
    "body": "Otro contenido de ejemplo con más de diez caracteres.",
    "created_at": "2025-11-07T02:17:28.665Z",
    "updated_at": "2025-11-07T02:17:28.665Z"
  }
]
```

### Obtener un artículo específico
- **GET** `/api/v1/articles/:id`
- **Respuesta exitosa (200):**
```json
{
  "id": 1,
  "title": "Primer artículo",
  "body": "Contenido de ejemplo suficiente para validar.",
  "created_at": "2025-11-07T02:17:28.660Z",
  "updated_at": "2025-11-07T02:17:28.660Z"
}
```

### Crear un nuevo artículo
- **POST** `/api/v1/articles`
- **Headers:** `Content-Type: application/json`
- **Body:**
```json
{
  "article": {
    "title": "Nuevo artículo",
    "body": "Contenido de al menos 10 caracteres para validar"
  }
}
```
- **Respuesta exitosa (201):**
```json
{
  "id": 3,
  "title": "Nuevo artículo",
  "body": "Contenido de al menos 10 caracteres para validar",
  "created_at": "2025-11-07T02:18:48.852Z",
  "updated_at": "2025-11-07T02:18:48.852Z"
}
```

### Actualizar un artículo
- **PATCH/PUT** `/api/v1/articles/:id`
- **Headers:** `Content-Type: application/json`
- **Body:**
```json
{
  "article": {
    "title": "Artículo actualizado",
    "body": "Contenido actualizado con más de diez caracteres"
  }
}
```
- **Respuesta exitosa (200):**
```json
{
  "id": 1,
  "title": "Artículo actualizado",
  "body": "Contenido actualizado con más de diez caracteres",
  "created_at": "2025-11-07T02:17:28.660Z",
  "updated_at": "2025-11-07T02:19:00.003Z"
}
```

### Eliminar un artículo
- **DELETE** `/api/v1/articles/:id`
- **Respuesta exitosa (204):** Sin contenido

## Validaciones

El modelo `Article` incluye las siguientes validaciones:

- `title`: Requerido (no puede estar vacío)
- `body`: Requerido y debe tener al menos 10 caracteres

### Respuesta de error de validación (422):
```json
{
  "title": ["can't be blank"],
  "body": ["is too short (minimum is 10 characters)"]
}
```

## Ejemplos de uso con curl

### Listar artículos:
```bash
curl -X GET http://localhost:3000/api/v1/articles
```

### Crear artículo:
```bash
curl -X POST http://localhost:3000/api/v1/articles \
  -H "Content-Type: application/json" \
  -d '{"article": {"title": "Nuevo", "body": "Contenido de al menos 10 caracteres"}}'
```

### Obtener artículo específico:
```bash
curl -X GET http://localhost:3000/api/v1/articles/1
```

### Actualizar artículo:
```bash
curl -X PATCH http://localhost:3000/api/v1/articles/1 \
  -H "Content-Type: application/json" \
  -d '{"article": {"title": "Actualizado", "body": "Nuevo contenido actualizado"}}'
```

### Eliminar artículo:
```bash
curl -X DELETE http://localhost:3000/api/v1/articles/1
```

## Página de prueba AJAX

Visita `http://localhost:3000/test.html` para ver una página de prueba que consume la API usando JavaScript fetch y muestra la lista de artículos.

## Estructura del proyecto

```
app/
├── controllers/
│   └── api/
│       └── v1/
│           └── articles_controller.rb  # Controlador CRUD
├── models/
│   └── article.rb                      # Modelo con validaciones
config/
├── routes.rb                           # Configuración de rutas API
db/
├── migrate/
│   └── create_articles.rb              # Migración de la tabla
├── seeds.rb                            # Datos de prueba
public/
└── test.html                           # Página de prueba AJAX
```

