# P3 · Desplegar y asegurar la API en la nube

Programación Web · Grupo 4X7B · Unidad 5 Cómputo en la nube y servicios

**Equipo:** JEREMIAS MARTINEZ MARTINEZ - KAROL GONZALEZ CHAIREZ

## Descripción

API REST de productos (Node.js + Express) desplegada en Render y protegida con
variables de entorno, CORS restringido y un token para las rutas de escritura.
Es la continuación de la P2.

## URL pública

- API: https://TU-API.onrender.com/api/productos
- Página que la consume: https://USUARIO.github.io/p3-frontend/

> En el plan gratuito de Render el servicio se duerme; la primera petición
> puede tardar cerca de un minuto.

## Endpoints

| Método | Ruta | Token (x-api-key) | Descripción |
|--------|------|-------------------|-------------|
| GET | /api/productos | No | Lista los productos |
| GET | /api/productos/:id | No | Consulta un producto |
| POST | /api/productos | Sí | Crea un producto |
| PUT | /api/productos/:id | Sí | Actualiza un producto |
| DELETE | /api/productos/:id | Sí | Elimina un producto |

## Seguridad

1. **Variables de entorno:** las credenciales viven en `.env` (no se sube a GitHub)
   y en Render, en la sección *Environment Variables*.
2. **CORS:** solo los orígenes listados en `ORIGEN_PERMITIDO` pueden consumir la API desde un navegador.
3. **Token:** las rutas POST, PUT y DELETE exigen el header `x-api-key`; sin él
   o con uno incorrecto responden `401`.

## Variables de entorno

Copia `.env.example` como `.env` y llena los valores:

```
API_KEY=
ORIGEN_PERMITIDO=
```

## Ejecutar en local

```
npm install
npm run dev
```

El servidor queda en http://localhost:3000

## Pruebas realizadas (Postman)

| # | Petición | Header x-api-key | Resultado |
|---|----------|------------------|-----------|
| 1 | GET /api/productos | Sin header | 200 |
| 2 | POST /api/productos | Sin header | 401 |
| 3 | POST /api/productos | Clave incorrecta | 401 |
| 4 | POST /api/productos | Clave correcta | 201 |
| 5 | DELETE /api/productos/1 | Clave correcta | 204 |

## Tecnologías

Node.js, Express, cors, dotenv, Render.
