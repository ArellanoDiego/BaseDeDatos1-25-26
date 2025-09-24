# Entidades y Atributos

## USUARIO
- id_usuario (PK)
- nombre
- email
- teléfono

## CLIENTE *(subtipo de Usuario)*
- id_cliente (PK, FK a Usuario)
- fecha_registro
- nivel_fidelidad

## VENDEDOR *(subtipo de Usuario)*
- id_vendedor (PK, FK a Usuario)
- reputación
- fecha_alta

## CATEGORÍA
- id_categoria (PK)
- nombre
- id_categoria_padre (FK, opcional para categorías raíz)

## PRODUCTO
- id_producto (PK)
- id_vendedor (FK)
- nombre
- descripción
- id_categoria (FK)

## VARIANTE_PRODUCTO
- id_variante (PK)
- id_producto (FK)
- talla
- color
- sku

## ALMACÉN
- id_almacen (PK)
- id_vendedor (FK)
- nombre
- dirección

## INVENTARIO
- id_inventario (PK)
- id_almacen (FK)
- id_variante (FK)
- cantidad_disponible
- cantidad_reservada

## PEDIDO
- id_pedido (PK)
- id_cliente (FK)
- fecha_creación
- estado_pedido

## LÍNEA_PEDIDO
- id_linea (PK)
- id_pedido (FK)
- id_variante (FK)
- cantidad
- precio_unitario

## ENVÍO
- id_envio (PK)
- id_pedido (FK)
- estado_envio
- fecha_envio

## PAGO
- id_pago (PK)
- id_pedido (FK)
- monto
- método_pago
- estado_pago

## REEMBOLSO
- id_reembolso (PK)
- id_pago (FK)
- monto_devuelto
- motivo

## DEVOLUCIÓN
- id_devolucion (PK)
- id_linea (FK)
- motivo
- estado

## PROMOCIÓN
- id_promocion (PK)
- nombre
- tipo_aplicacion (por_producto, por_categoria, por_pedido)
- porcentaje_descuento
- fecha_inicio / fecha_fin

## RESEÑA
- id_resena (PK)
- id_cliente (FK)
- id_producto (FK)
- calificación
- comentario

## HISTORIAL_PRECIO
- id_historial (PK)
- id_variante (FK)
- precio
- fecha_inicio
- fecha_fin

## LOG_AUDITORÍA
- id_log (PK)
- entidad_afectada
- id_entidad
- usuario_responsable
- fecha
- descripción

---

# Relaciones y Cardinalidades

- **Usuario–Cliente:** Un usuario puede ser cliente (1:1 opcional); todo cliente es un usuario (1:1).  
- **Usuario–Vendedor:** Un usuario puede ser vendedor (1:1 opcional); todo vendedor es un usuario (1:1).  
- **Vendedor–Producto:** Un vendedor publica varios productos (1:N); cada producto pertenece a un vendedor (N:1).  
- **Producto–Variante:** Un producto puede tener varias variantes (1:N); cada variante corresponde a un producto (N:1).  
- **Producto–Categoría:** Cada producto pertenece a una categoría (N:1); una categoría agrupa varios productos (1:N).  
- **Categoría–Categoría:** Una categoría padre puede contener subcategorías (1:N); cada subcategoría tiene una categoría padre (N:1).  
- **Variante–Inventario:** Una variante puede tener múltiples registros de inventario (1:N); cada registro se asocia a una variante (N:1).  
- **Almacén–Inventario:** Un almacén gestiona distintos inventarios (1:N); cada inventario pertenece a un almacén (N:1).  
- **Vendedor–Almacén:** Un vendedor puede tener varios almacenes (1:N); cada almacén pertenece a un vendedor (N:1).  
- **Cliente–Pedido:** Un cliente puede realizar varios pedidos (1:N); cada pedido pertenece a un cliente (N:1).  
- **Pedido–LíneaPedido:** Un pedido contiene varias líneas (1:N); cada línea pertenece a un pedido (N:1).  
- **Variante–LíneaPedido:** Una variante puede aparecer en distintas líneas de pedido (1:N); cada línea hace referencia a una variante (N:1).  
- **Pedido–Envío:** Un pedido puede generar múltiples envíos (1:N); cada envío pertenece a un pedido (N:1).  
- **Pedido–Pago:** Un pedido puede tener varios pagos (1:N); cada pago corresponde a un pedido (N:1).  
- **Pago–Reembolso:** Un pago puede originar varios reembolsos (1:N); cada reembolso se vincula a un pago (N:1).  
- **LíneaPedido–Devolución:** Una línea puede ser devuelta (0..N); cada devolución corresponde a una línea (N:1).  
- **Promoción–Producto:** Una promoción puede aplicarse a varios productos (M:N); cada producto puede tener varias promociones asociadas (M:N).  
- **Cliente–Reseña:** Un cliente puede escribir varias reseñas (1:N); cada reseña pertenece a un cliente (N:1).  
- **Producto–Reseña:** Un producto puede recibir muchas reseñas (1:N); cada reseña está asociada a un producto (N:1).  
- **Variante–HistorialPrecio:** Una variante puede registrar múltiples precios a lo largo del tiempo (1:N); cada historial corresponde a una variante (N:1).  
