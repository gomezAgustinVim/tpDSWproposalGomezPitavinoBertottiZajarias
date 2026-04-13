# Tareas pendientes

## Para regularidad

- Sanitización de inputs (express-validator, zod o class-validator). ✅
- CORS controlado, no globalizado. ✅

## Para AD

Ahora mismo estamos parados en una etapa en la cual tenemos implementado el JWT token (autenticación) junto con bcrypt (hashing de las contraseñas). Podemos loguearnos perfectamente cada vez que lo probamos ya sea via curl, postman, o el propio front. Esto nos devuelve un token que expira en 8 horas. Faltaría renovar ese token via rate limiting o alguna cosa así y además permitir autorización y control de rutas.

Plan de ejecución recomendado para backend:

1. Agregar Usuario + Auth + Roles (Auth autenticación roles autorización)
1. Proteger rutas (autorización)
1. Agregar tests (unitario + integración)
1. Completar CRUDs faltantes
1. Swagger
1. README + scripts
1. Deploy

- Autenticación JWT con refresh tokens (expiran, se renuevan). ✅
- Hash de contraseñas con bcrypt o argon2. ✅
- Autorización basada en roles o scopes (admin, cliente, invitado…).
- Rate limiting (por IP, endpoint o token) → express-rate-limit.
- Helmet para cabeceras seguras.
- Logger: usa pino o winston para logs con timestamps y niveles (info, warn, error).

## Proteger rutas

Exacto, es autorización — autenticación es "quién sos" (el login), autorización es "qué podés hacer" (las rutas protegidas). Pero van de la mano y es el siguiente paso lógico.

Antes de escribir el middleware, definamos qué rutas van a requerir qué nivel de acceso. Basándome en el proyecto:

| Ruta                                 | Acceso                    |
| ------------------------------------ | ------------------------- |
| `POST /api/auth/login`               | público                   |
| `POST /api/clientes` (registro)      | público                   |
| `GET /api/muebles`                   | público                   |
| `GET /api/muebles/:id`               | público                   |
| `POST/PUT/PATCH/DELETE /api/muebles` | solo admin                |
| `GET /api/clientes`                  | solo admin                |
| `GET /api/clientes/:id`              | admin o el propio cliente |
| `GET /api/pedidos`                   | solo admin                |
| `GET /api/pedidos/:id`               | admin o el propio cliente |
| `POST /api/pedidos`                  | user autenticado          |

Un pedido es epic o caso de uso por tener valor para el negocio

- Error handler global innecesario para AD
- Conseguirme los clientes del favorito no es necesario (no lo pongo en el populate)
