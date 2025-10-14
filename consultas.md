# Back

1. item_id aparece como atributo null en muebles desde la base de datos. Cómo se trata esto?
2. Opcion 2: Mueble es un N:M con Pedido y la tabla intermedia se llama items
   (Items sigue creado pero con many to one para cada lado de la relacion)
3. Consultas sobre las relaciones de items, pedidos y muebles y sobre cómo manejarlas
4. Relaciones de favoritos en general, como manejar rutas de CRUD dependiente
5. Si yo creo un material que tenga id 8 y despues lo borro. Agregando los
   materiales que restan más adelante y un mueble referencia a un material como
   el 8, pero ahora ese mismo material tiene id 9, qué se puede hacer para
   encontrar el material?
6. Modelar pago como CUU?
7. Crear seeder con mikroORM (o desactivar el drop schema)

## Tareas pendientes para el backend

- Sanitización de inputs (express-validator, zod o class-validator). ✅
- CORS controlado, no globalizado. ✅
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
