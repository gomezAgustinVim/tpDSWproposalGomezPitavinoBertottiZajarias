# Back

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

# Front
