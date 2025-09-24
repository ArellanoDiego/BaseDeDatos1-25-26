# 📋 1. Lista Predefinida de Requisitos

1. El sistema debe gestionar eventos con nombre, descripción, lugar y fechas.  
2. Cada evento puede tener múltiples sesiones en distintas fechas/horas.  
3. Las sesiones pueden ser con asientos numerados o de capacidad general.  
4. Cada sesión ofrece diferentes tipos de tickets (General, VIP, Early-bird, etc.) con precio y cantidad máxima.  
5. Los clientes pueden comprar uno o varios tickets por sesión.  
6. Cada ticket es único y tiene estados: reservado, pagado, cancelado, usado.  
7. Los pagos de tickets deben registrarse con método de pago, monto y estado.  
8. Los tickets pueden tener descuentos aplicados mediante códigos/promocodes.  
9. Se debe permitir la gestión de reembolsos totales o parciales con comisión.  
10. Los asistentes realizan check-in con sus tickets (una sola vez).  
11. Los clientes pueden dejar reseñas después de asistir a un evento.  
12. Se necesitan reportes:  
   - Ocupación por sesión  
   - Ingresos por evento  
   - Tickets vendidos por tipo  

---

# 🗂️ 2. Identificación de Entidades

- **EVENTO**  
- **SESION**  
- **TIPO_TICKET**  
- **ASIENTO**  
- **CLIENTE**  
- **TICKET**  
- **PAGO**  
- **REEMBOLSO**  
- **DESCUENTO**  
- **CHECKIN**  
- **RESEÑA**  

---

# 🔗 3. Identificación de Relaciones

- **Evento–Sesión**: 1:N  
- **Sesión–TipoTicket**: 1:N  
- **Sesión–Asiento**: 1:N (opcional)  
- **Sesión–Ticket**: 1:N  
- **Cliente–Ticket**: 1:N  
- **Ticket–Pago**: 1:1  
- **Pago–Reembolso**: 1:N  
- **Ticket–Descuento**: N:1 (opcional)  
- **Ticket–Checkin**: 1:1 (opcional)  
- **Cliente–Reseña**: 1:N  
- **Evento–Reseña**: 1:N  

---

# 📑 4. Identificación de Atributos

### EVENTO
- id_evento (PK)  
- nombre  
- descripcion  
- lugar  
- fecha_inicio  
- fecha_fin  

### SESION
- id_sesion (PK)  
- id_evento (FK)  
- fecha  
- hora  
- capacidad (opcional si no numerada)  

### TIPO_TICKET
- id_tipo_ticket (PK)  
- id_sesion (FK)  
- nombre_tipo  
- precio  
- cantidad_max  

### ASIENTO
- id_asiento (PK)  
- id_sesion (FK)  
- fila  
- numero  
- estado (disponible, ocupado)  

### CLIENTE
- id_cliente (PK)  
- nombre  
- email  
- telefono  

### TICKET
- id_ticket (PK)  
- id_cliente (FK)  
- id_sesion (FK)  
- id_tipo_ticket (FK)  
- id_asiento (FK, nullable)  
- estado (reservado, pagado, cancelado, usado)  

### PAGO
- id_pago (PK)  
- id_ticket (FK)  
- monto_pagado  
- fecha_pago  
- metodo_pago  
- estado_pago (completado, reembolsado parcial, reembolsado total)  

### REEMBOLSO
- id_reembolso (PK)  
- id_pago (FK)  
- monto_devuelto  
- fecha_reembolso  
- motivo  
- porcentaje_comision  

### DESCUENTO
- id_descuento (PK)  
- codigo  
- porcentaje  
- valido_desde  
- valido_hasta  

### CHECKIN
- id_checkin (PK)  
- id_ticket (FK)  
- fecha_checkin  
- validado_por  

### RESEÑA
- id_resena (PK)  
- id_cliente (FK)  
- id_evento (FK)  
- calificacion  
- comentario  
- fecha_resena  

---
    