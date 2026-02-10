# Tareas pendientes

## Para regularidad

- Sanitización de inputs (express-validator, zod o class-validator). ✅
- CORS controlado, no globalizado. ✅

## Para AD

Plan de ejecución recomendado para backend:

1. Agregar Usuario + Auth + Roles
1. Proteger rutas
1. Agregar tests (unitario + integración)
1. Completar CRUDs faltantes
1. Swagger
1. README + scripts
1. Deploy

- Autenticación JWT con refresh tokens (expiran, se renuevan).
- Autorización basada en roles o scopes (admin, cliente, invitado…).
- Hash de contraseñas con bcrypt o argon2.
- Rate limiting (por IP, endpoint o token) → express-rate-limit.
- Helmet para cabeceras seguras.
- Logger: usa pino o winston para logs con timestamps y niveles (info, warn, error).

| Aspecto      | Mejora clave                                     |
| ------------ | ------------------------------------------------ |
| Sanitización | Reemplazar por DTO o validación con `zod` ✅     |
| Errores      | Middleware global + `asyncHandler` ✅            |
| Populate     | Controlar niveles para no sobrecargar queries ✅ |
| Respuestas   | Estandarizar formato JSON ✅                     |
| Extra        | Logger + Helmet + Swagger para docs              |

Un pedido es epic o caso de uso por tener valor para el negocio

- Error handler global innecesario para AD
- Conseguirme los clientes del favorito no es necesario (no lo pongo en el populate)
