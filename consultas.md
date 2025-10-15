# Back

5. Modelar pago como CUU?
6. Crear seeder con mikroORM (o desactivar el drop schema)

- Error handler global innecesario para AD
- Conseguirme los clientes del favorito no es necesario (no lo pongo en el populate)

## Tareas pendientes para el backend

- Sanitización de inputs (express-validator, zod o class-validator). ✅
- CORS controlado, no globalizado. ✅

## Para AD

- Autenticación JWT con refresh tokens (expiran, se renuevan).
- Autorización basada en roles o scopes (admin, cliente, invitado…).
- Hash de contraseñas con bcrypt o argon2.
- Rate limiting (por IP, endpoint o token) → express-rate-limit.
- Helmet para cabeceras seguras.
- Logger: usa pino o winston para logs con timestamps y niveles (info, warn, error).

| Aspecto      | Mejora clave                                  |
| ------------ | --------------------------------------------- |
| Sanitización | Reemplazar por DTO o validación con `zod` ✅  |
| Errores      | Middleware global + `asyncHandler` ✅         |
| Populate     | Controlar niveles para no sobrecargar queries |
| Respuestas   | Estandarizar formato JSON                     |
| Extra        | Logger + Helmet + Swagger para docs           |

Un pedido es epic o caso de uso por tener valor para el negocio

# Front

1. Poner todas categorias por igual, sin distinción de categoria padre o hija
1. Hacerlo mobile-first
