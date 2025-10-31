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

- Las categorías se pueden mostrar como una sola vista en /muebles con un
  filtrado? o seria mas conveniente mostrar distintas paginas por categoria ej
  muebles/sillas, muebles/camas

1. Cuando entre al carrito del front, tengo que poder agregar items que usen la id de un mueble, esto me permite seleccionar la cantidad
2. Los items del carrito se guardan en un local storage
3. El pedido se crea, se le añaden los items (le llega el carrito completo)
4. En este punto, el pedido ya tiene un array de items con su estado y todos los atributos

El siguiente esquema detalla cómo le llegan los items al pedido.

Recordamos que no trabajamos con monorepo.
