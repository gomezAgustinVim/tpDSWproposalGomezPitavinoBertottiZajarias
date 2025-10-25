# Back

- Necesitamos dos casos de uso terminados:
  - Hacer gestión de pago
  - Gestión de estado de pedido

El carrito tiene que ser un local storage para todos los items del Frontend que
llegue como una unidad al pedido

- Asociarlo con sus pedidos (crear pedidos)
  - Hacer que cuando creo mi primer item, se cree el pedido asociado con el
    cliente correspondiente
  - O si es mejor, hacer que crear el pedido me cree al item inmediatamente
- Gestionar los estados de pedidos

Todas las rutas parecen funcionar, pero el pedido no se crea porque:

```json
"message": "El carrito está vacío."
```

Así que se debe solucionar este problema

# Front
