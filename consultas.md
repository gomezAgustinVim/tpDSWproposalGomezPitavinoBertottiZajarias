# Back

1. item_id aparece como atributo null en muebles desde la base de datos. Cómo se trata esto?
1. Si yo creo un material que tenga id 8 y despues lo borro. Agregando los
   materiales que restan más adelante y un mueble referencia a un material como
   el 8, pero ahora ese mismo material tiene id 9, qué se puede hacer para
   encontrar el material?
1. Es una restricción estupida que un mueble no requiera si o si pertenecer a un
   material y/o una categoria?
1. Un amigo dejó definido en el frontend a dormitorio como una categoria padre,
   la cual contiene subcategorias dentro. Modelar esto implicaría crear una
   jerarquía en la base de datos, o bien simplemente mostrar categorias "hijas"
   agrupadas bajo una categoria "padre", pero solo visualmente.
1. Modelar pago como CUU?
1. Cómo integrar snowflake id (es necesario reemplazar el base entity con su id?)

## Tareas pendientes para el backend

- Sanitización de inputs (express-validator, zod o class-validator). ✅
- Autenticación JWT con refresh tokens (expiran, se renuevan).
- Autorización basada en roles o scopes (admin, cliente, invitado…).
- Hash de contraseñas con bcrypt o argon2.
- Rate limiting (por IP, endpoint o token) → express-rate-limit.
- Helmet para cabeceras seguras.
- CORS controlado, no globalizado. ✅
- Logger: usa pino o winston para logs con timestamps y niveles (info, warn, error).

| Aspecto      | Mejora clave                                  |
| ------------ | --------------------------------------------- |
| Sanitización | Reemplazar por DTO o validación con `zod` ✅  |
| Errores      | Middleware global + `asyncHandler` ✅         |
| Populate     | Controlar niveles para no sobrecargar queries |
| Respuestas   | Estandarizar formato JSON                     |
| Extra        | Logger + Helmet + Swagger para docs           |

Un pedido es epic o caso de uso por tener valor para el negocio

### Baja prioridad

2. Reconsiderar relaciones con linea pedido:
   - oneToMany desde mueble (con pedidos), manyToOne desde pedido (con muebles)
3. HistorialCompras será eliminado, por lo menos por ahora. Posiblemente luego será implementado, es decir que no se eliminará en concepto:
   - Es un caso de uso para ver el histórico de pedidos (filtrar por pedido)

# Front
