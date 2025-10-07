# Back

1. Cómo integrar snowflake id (es necesario reemplazar el base entity con su id?)
1. Debería meter el createdAt?
1. Chequear que los origenes de cors anden bien
1. Consultar sobre el modelado de atributos que sean relaciones en el DER y sobre cómo traducirlas a many to many o one to many, y qué implicaría hacerlo para el ORM.
1. Pedido no es CRUD, pero hace falta codificarlo con la capa MVC incluyendo el controller, repository, routes, etc?
1. Por qué no pude usar getReference en update de cliente?
1. Cómo manejo los populates? También hay para el descuento y cualquier otro atributo que se repita varias veces en entidad cliente?

## Tareas pendientes para el backend

1. Implementar CRUD favoritos:
   - Hacer desde clientes un array de favoritos (sin fechaAgregado)
2. Reconsiderar relaciones con linea pedido:
   - oneToMany desde mueble (con pedidos), manyToOne desde pedido (con muebles)
3. HistorialCompras será eliminado, por lo menos por ahora. Posiblemente luego será implementado, es decir que no se eliminará en concepto:
   - Es un caso de uso para ver el histórico de pedidos (filtrar por pedido)

Un pedido es epic o caso de uso por tener valor para el negocio
