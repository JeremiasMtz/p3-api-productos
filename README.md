# P2 · API REST de productos (Node.js + Express)

Programación Web · Grupo 4X7B · Unidad 5 Cómputo en la nube y servicios

**Equipo:** JEREMIAS MARTINEZ MARTINEZ - KAROL GONZALEZ CHAIREZ

## Descripción

Servicio web que administra un catálogo de productos con las cuatro operaciones CRUD.
Responde en JSON y usa los códigos de estado HTTP correctos. Los datos se guardan en
memoria, así que se reinician cada vez que se reinicia el servidor.

Cada producto tiene esta forma:

```json
{ "id": 1, "nombre": "Teclado", "precio": 350, "stock": 10 }
```

## Instalación y uso

Requiere Node.js 18 o superior.

```bash
npm install
npm start        # o: npm run dev (se reinicia solo al guardar cambios)
```

El servidor queda en `http://localhost:3000`. Al abrir esa dirección responde
`{"mensaje":"API de productos funcionando"}`.

## Rutas de la API

| Método | Ruta                | Acción      | Respuesta correcta     | Posibles errores |
|--------|---------------------|-------------|------------------------|------------------|
| GET    | /api/productos      | Listar todos| 200 + arreglo          | —                |
| GET    | /api/productos/:id  | Ver uno     | 200 + objeto           | 404              |
| POST   | /api/productos      | Crear       | 201 + objeto creado    | 400              |
| PUT    | /api/productos/:id  | Actualizar  | 200 + objeto actualizado | 400, 404       |
| DELETE | /api/productos/:id  | Eliminar    | 204 sin contenido      | 404              |

Extra: `GET /api/productos?buscar=tec` filtra los productos por nombre.

### Validación (POST y PUT)

- `nombre`: texto obligatorio.
- `precio`: número mayor o igual a 0.
- `stock`: entero mayor o igual a 0.

Si algo no cumple, responde `400` con la lista de errores.

## Ejemplo

Petición:

```http
POST /api/productos
Content-Type: application/json

{ "nombre": "Monitor", "precio": 2500, "stock": 5 }
```

Respuesta `201 Created`:

```json
{ "id": 3, "nombre": "Monitor", "precio": 2500, "stock": 5 }
```

Ejemplo de error, con `{ "nombre": "", "precio": -1 }`, respuesta `400 Bad Request`:

```json
{
  "errores": [
    "nombre es obligatorio",
    "precio debe ser un número positivo",
    "stock debe ser un entero positivo"
  ]
}
```

## Pruebas

En este repositorio está la colección de Postman `P2_Productos.postman_collection.json`
con las 8 peticiones de prueba y su código de estado esperado.
