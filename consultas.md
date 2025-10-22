# Back

- Error handler global innecesario para AD
- Conseguirme los clientes del favorito no es necesario (no lo pongo en el populate)

- Necesitamos dos casos de uso terminados:
  - Hacer gestión de pago
  - Gestión de estado de pedido

Ahora que ya agregué que el item se pueda crear con su subtotal ya precalculado
en su controller, necesito:

- Asociarlo con sus pedidos (crear pedidos)
  - Hacer que cuando creo mi primer item, se cree el pedido asociado con el
    cliente correspondiente
  - O si es mejor, hacer que crear el pedido me cree al item inmediatamente
- Hacer que se actualice el subtotal cuando actualice la cantidad del pedido
- Gestionar los estados de pedidos
- A lo mejor puedo mostrar un array con las claves de los items desde el pedido

Todas las rutas parecen funcionar, pero el pedido no se crea porque:

```json
"message": "El carrito está vacío."
```

Así que se debe solucionar este problema

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

| Aspecto      | Mejora clave                                     |
| ------------ | ------------------------------------------------ |
| Sanitización | Reemplazar por DTO o validación con `zod` ✅     |
| Errores      | Middleware global + `asyncHandler` ✅            |
| Populate     | Controlar niveles para no sobrecargar queries ✅ |
| Respuestas   | Estandarizar formato JSON ✅                     |
| Extra        | Logger + Helmet + Swagger para docs              |

Un pedido es epic o caso de uso por tener valor para el negocio

# Front

1. Poner todas categorias por igual, sin distinción de categoria padre o hija
1. Hacerlo mobile-first
