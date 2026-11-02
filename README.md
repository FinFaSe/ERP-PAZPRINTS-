# ERP PazPrints · Prototipo v0.2

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
| Clientes | Registro con DNI/RUC, teléfono y deuda de cada cliente |
| Cotizaciones | Cotizador de serigrafía en 3 pasos (cliente y fechas → prendas → total). Cliente nuevo desde la misma pantalla, envío por WhatsApp, impresión o PDF y opción de eliminar |
| Pedidos / Producción | Tablero por estados: Pendiente → Diseño → Pantallas → Estampado → Listo → Entregado |
| Inventario | Prendas (color/talla) e insumos (tintas, emulsión, mallas), con alertas de stock mínimo |
| Caja y pagos | Adelantos y saldos (Efectivo, Yape, Plin, transferencia o tarjeta), gastos y resultado del mes |
| Configuración | Datos de la empresa, precios, respaldo y restauración en JSON |

### Fórmula de precio (editable en Configuración)

- **Precio unitario** = precio de la prenda + colores × ubicaciones × costo por color (S/ 1.50 por defecto)
- **Pantallas** = colores × ubicaciones × costo por pantalla (S/ 35 por defecto), se cobra una vez por pedido
- **Descuento por volumen:** 50+ prendas 5 %, 100+ 10 %, 300+ 15 %
- Cada línea acepta un **precio manual** que reemplaza el cálculo.

### Mensajes de WhatsApp

- **Cotización:** el botón *Guardar y enviar por WhatsApp* (o 📲 en la lista) arma el mensaje con el detalle, el total, el adelanto, la fecha de entrega y la validez. El mensaje se puede editar antes de enviarlo. Al enviarlo, la cotización pasa a *Enviada*.
- **Pedido listo:** al mover un pedido a *Listo* se abre el aviso para el cliente, con el saldo pendiente y dónde recogerlo. También se puede enviar desde el tablero o desde el detalle del pedido, y queda registrado que se avisó.
- Se usa el enlace `wa.me`. Los números peruanos de 9 dígitos reciben automáticamente el prefijo 51.

### Reglas automáticas

- Al aprobar una cotización (*El cliente aceptó: crear pedido*) se crea el pedido con la fecha de entrega elegida en la cotización.
- Al pasar un pedido a **Estampado** se descuentan las prendas del inventario.
- Al registrar una compra de insumos con costo, se crea el gasto en caja y se actualiza el costo unitario.

## Limitaciones del prototipo

- Los datos se guardan **en el navegador** (localStorage). Cada computadora tiene sus propios datos. Usa *Configuración → Descargar respaldo* para no perder información.
- No hay usuarios ni contraseñas, ni facturación electrónica SUNAT.
