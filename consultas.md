# Back

1. Chequear que los origenes de cors anden bien
1. Cómo integrar snowflake id (es necesario reemplazar el base entity con su id?)

## Tareas pendientes para el backend

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
