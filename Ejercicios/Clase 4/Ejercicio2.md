Entidades y Atributos

**USUARIO**
- id_usuario (PK)
- nombre
- email
- telefono

**CLIENTE** (subtipo de USUARIO)
- id_cliente (PK, FK a USUARIO)
- fecha_registro
- nivel_fidelidad

**VENDEDOR** (subtipo de USUARIO)
- id_vendedor (PK, FK a USUARIO)
- reputacion
- fecha_alta

**CATEGORIA**
- id_categoria (PK)
- nombre
- id_categoria_padre (FK, nullable para categorías raíz)

**PRODUCTO**
- id_producto (PK)
- id_vendedor (FK)
- nombre
- descripcion
- id_categoria (FK)

**VARIANTE_PRODUCTO**
- id_variante (PK)
- id_producto (FK)
- talla
- color
- sku

**ALMACEN**
- id_almacen (PK)
- id_vendedor (FK)
- nombre
- direccion

**INVENTARIO**
- id_inventario (PK)
- id_almacen (FK)
- id_variante (FK)
- cantidad_disponible
- cantidad_reservada

**PEDIDO**
- id_pedido (PK)
- id_cliente (FK)
- fecha_creacion
- estado_pedido

**LINEA_PEDIDO**
- id_linea (PK)
- id_pedido (FK)
- id_variante (FK)
- cantidad
- precio_unitario

**ENVIO (Shipment)**
- id_envio (PK)
- id_pedido (FK)
- estado_envio
- fecha_envio

**PAGO**
- id_pago (PK)
- id_pedido (FK)
- monto
- metodo_pago
- estado_pago

**REEMBOLSO**
- id_reembolso (PK)
- id_pago (FK)
- monto_devuelto
- motivo

**DEVOLUCION**
- id_devolucion (PK)
- id_linea (FK)
- motivo
- estado

**PROMOCION**
- id_promocion (PK)
- nombre
- tipo_aplicacion (por_producto, por_categoria, por_pedido)
- porcentaje_descuento
- fecha_inicio
- fecha_fin

**RESEÑA**
- id_resena (PK)
- id_cliente (FK)
- id_producto (FK)
- calificacion
- comentario

**HISTORIAL_PRECIO**
- id_historial (PK)
- id_variante (FK)
- precio
- fecha_inicio
- fecha_fin

**LOG_AUDITORIA**
- id_log (PK)
- entidad_afectada
- id_entidad
- usuario_responsable
- fecha
- descripcion

---

# 🔗 Relaciones y Cardinalidades (bidireccionales)

- **Usuario–Cliente:** Usuario puede ser cliente (1:1 opcional), Cliente es un usuario (1:1)  
- **Usuario–Vendedor:** Usuario puede ser vendedor (1:1 opcional), Vendedor es un usuario (1:1)  
- **Vendedor–Producto:** Vendedor publica productos (1:N), Producto pertenece a un vendedor (N:1)  
- **Producto–Variante:** Producto tiene variantes (1:N), Variante pertenece a producto (N:1)  
- **Producto–Categoría:** Producto pertenece a categoría (N:1), Categoría agrupa productos (1:N)  
- **Categoría–Categoría:** Categoría padre contiene subcategorías (1:N), Subcategoría pertenece a categoría padre (N:1)  
- **Variante–Inventario:** Variante tiene registros de inventario (1:N), Inventario corresponde a variante (N:1)  
- **Almacén–Inventario:** Almacén gestiona inventario (1:N), Inventario pertenece a almacén (N:1)  
- **Vendedor–Almacén:** Vendedor tiene almacenes (1:N), Almacén pertenece a un vendedor (N:1)  
- **Cliente–Pedido:** Cliente realiza pedidos (1:N), Pedido pertenece a cliente (N:1)  
- **Pedido–LíneaPedido:** Pedido contiene líneas (1:N), Línea pertenece a pedido (N:1)  
- **Variante–LíneaPedido:** Variante puede aparecer en varias líneas (1:N), Línea se refiere a una variante (N:1)  
- **Pedido–Envío:** Pedido puede generar varios envíos (1:N), Envío pertenece a pedido (N:1)  
- **Pedido–Pago:** Pedido puede tener varios pagos (1:N), Pago pertenece a pedido (N:1)  
- **Pago–Reembolso:** Pago genera reembolsos (1:N), Reembolso pertenece a pago (N:1)  
- **LíneaPedido–Devolución:** Línea puede ser devuelta (0..N), Devolución corresponde a línea (N:1)  
- **Promoción–Producto:** Promoción aplica a productos (M:N), Producto tiene promociones aplicables (M:N)  
- **Cliente–Reseña:** Cliente escribe reseñas (1:N), Reseña pertenece a cliente (N:1)  
- **Producto–Reseña:** Producto recibe reseñas (1:N), Reseña corresponde a producto (N:1)  
- **Variante–HistorialPrecio:** Variante registra historial (1:N), Historial corresponde a variante (N:1) 