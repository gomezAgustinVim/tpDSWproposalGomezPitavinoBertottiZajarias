# Back

1. Chequear que los origenes de cors anden bien
1. linea_pedido_id aparece como atributo null en muebles desde la base de datos. Cómo se trata esto?
1. Si yo creo un material que tenga id 8 y despues lo borro. Agregando los
   materiales que restan más adelante y un mueble referencia a un material como
   el 8, pero ahora ese mismo material tiene id 9, qué se puede hacer para
   encontrar el material?
1. Es una restricción estupida que un mueble no requiera si o si pertenecer a un
   material y/o una categoria?
1. Cómo integrar snowflake id (es necesario reemplazar el base entity con su id?)

## Tareas pendientes para el backend

- Sanitización de inputs (express-validator, zod o class-validator).
- Autenticación JWT con refresh tokens (expiran, se renuevan).
- Autorización basada en roles o scopes (admin, cliente, invitado…).
- Hash de contraseñas con bcrypt o argon2.
- Rate limiting (por IP, endpoint o token) → express-rate-limit.
- Helmet para cabeceras seguras.
- CORS controlado, no globalizado.

- Logger: usa pino o winston para logs con timestamps y niveles (info, warn, error).
- Rate limiting: con express-rate-limit.
- Helmet y CORS configurado por dominio.
- Validación de input con zod o class-validator.
- Swagger/OpenAPI para documentar automáticamente tus endpoints.

| Aspecto      | Mejora clave                                  |
| ------------ | --------------------------------------------- |
| Sanitización | Reemplazar por DTO o validación con `zod`     |
| Errores      | Middleware global + `asyncHandler`            |
| Populate     | Controlar niveles para no sobrecargar queries |
| Respuestas   | Estandarizar formato JSON                     |
| Extra        | Logger + Helmet + Swagger para docs           |

Si querés, puedo generarte una plantilla base en TypeScript con Express + MikroORM + manejo global de errores + validación Zod, adaptada exactamente a tu estructura (cliente.controller.ts, cliente.routes.ts, etc.), para que la copies directo a tu proyecto. ¿Querés que te la arme?

Un pedido es epic o caso de uso por tener valor para el negocio

### Baja prioridad

2. Reconsiderar relaciones con linea pedido:
   - oneToMany desde mueble (con pedidos), manyToOne desde pedido (con muebles)
3. HistorialCompras será eliminado, por lo menos por ahora. Posiblemente luego será implementado, es decir que no se eliminará en concepto:
   - Es un caso de uso para ver el histórico de pedidos (filtrar por pedido)

## Extras de excelencia

- Pagos o transacciones: usar transacciones ACID del ORM (em.transactional).
- Cache con Redis para endpoints intensivos.
- Pagos y colas → RabbitMQ, Kafka o BullMQ.
- Internacionalización (i18n) si tenés front multi-lenguaje.
- Soft deletes (@Property({ onDelete: "soft" }) o flag activo = false).
- Auditoría / timestamps automáticos con @Property({ onCreate, onUpdate }).
