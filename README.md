# ERP PazPrints

ERP para un taller de **serigrafía**. Es la versión inicial, hecha para mostrar el flujo de trabajo y recibir comentarios.

## Cómo abrirlo

- **Local:** abre `app/index.html` en el navegador (Chrome, Edge o Firefox). No necesita instalación ni internet.
- **En línea:** el workflow `.github/workflows/pages.yml` publica la carpeta `app/` en GitHub Pages cada vez que hay cambios en `main`.
  - Hay que activarlo una vez: **Settings → Pages → Build and deployment → Source: GitHub Actions**.

En la pantalla de inicio está el botón **"Cargar datos de ejemplo"** para ver el sistema con información de prueba.

## Módulos

| Módulo | Qué hace |
|---|---|
| Inicio | Indicadores: pedidos en curso, atrasados, ingresos y gastos del mes, deudas y stock bajo |
| Clientes | Registro con DNI/RUC, teléfono y deuda de cada cliente. Se pueden eliminar; sus cotizaciones y pedidos se conservan con su nombre |
| Cotizaciones | Cotización simple en 3 pasos: cliente y fechas (inicio y entrega) → servicios (descripción, cantidad y precio por unidad con todo incluido) → total. Cliente nuevo desde la misma pantalla, envío por WhatsApp, impresión o PDF y opción de eliminar |
| Pedidos | Tablero por estados: Pendiente → Diseño → Pantallas → Estampado → Listo → Entregado. Se pueden eliminar, con opción de devolver las prendas al inventario y borrar los pagos |
| Inventario | Prendas (color/talla) e insumos (tintas, emulsión, mallas), con alertas de stock mínimo |
| Caja y pagos | Adelantos y saldos (Efectivo, Yape, Plin, transferencia o tarjeta), gastos y resultado del mes |
| Configuración | Datos de la empresa, adelanto e IGV, respaldo y restauración en JSON |

### Mensajes de WhatsApp

- **Cotización:** el botón *Guardar y enviar por WhatsApp* (o 📲 en la lista) arma el mensaje con cada servicio, el total, el adelanto y las fechas de inicio y entrega. El mensaje se puede editar antes de enviarlo. Al enviarlo, la cotización pasa a *Enviada*.
- **Pedido listo:** al mover un pedido a *Listo* se abre el aviso para el cliente, con el saldo pendiente y dónde recogerlo. También se puede enviar desde el tablero o desde el detalle del pedido, y queda registrado que se avisó.
- Se usa el enlace `wa.me`. Los números peruanos de 9 dígitos reciben automáticamente el prefijo 51.

### Reglas automáticas

- Al aprobar una cotización (*El cliente aceptó: crear pedido*) se crea el pedido con las fechas de inicio y entrega elegidas en la cotización.
- Al pasar un pedido a **Estampado** se descuentan las prendas del inventario.
- Al registrar una compra de insumos con costo, se crea el gasto en caja y se actualiza el costo unitario.

## Limitaciones del prototipo

- Los datos se guardan **en el navegador** (localStorage). Cada computadora tiene sus propios datos. Usa *Configuración → Descargar respaldo* para no perder información.
- No hay usuarios ni contraseñas, ni facturación electrónica SUNAT.
