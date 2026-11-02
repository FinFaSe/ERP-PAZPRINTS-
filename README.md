# ERP PazPrints · Prototipo v0.1

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
| Cotizaciones | Cotizador de serigrafía (prenda, colores, ubicaciones y pantallas), descuento por volumen, IGV opcional e impresión o PDF |
| Pedidos / Producción | Tablero por estados: Pendiente → Diseño → Pantallas → Estampado → Listo → Entregado |
| Inventario | Prendas (color/talla) e insumos (tintas, emulsión, mallas), con alertas de stock mínimo |
| Caja y pagos | Adelantos y saldos (Efectivo, Yape, Plin, transferencia o tarjeta), gastos y resultado del mes |
| Configuración | Datos de la empresa, precios, respaldo y restauración en JSON |

### Fórmula de precio (editable en Configuración)

- **Precio unitario** = precio de la prenda + colores × ubicaciones × costo por color (S/ 1.50 por defecto)
- **Pantallas** = colores × ubicaciones × costo por pantalla (S/ 35 por defecto), se cobra una vez por pedido
- **Descuento por volumen:** 50+ prendas 5 %, 100+ 10 %, 300+ 15 %
- Cada línea acepta un **precio manual** que reemplaza el cálculo.

### Reglas automáticas

- Al aprobar una cotización se crea el pedido, con entrega a 5 días.
- Al pasar un pedido a **Estampado** se descuentan las prendas del inventario.
- Al registrar una compra de insumos con costo, se crea el gasto en caja y se actualiza el costo unitario.

## Limitaciones del prototipo

- Los datos se guardan **en el navegador** (localStorage). Cada computadora tiene sus propios datos. Usa *Configuración → Descargar respaldo* para no perder información.
- No hay usuarios ni contraseñas, ni facturación electrónica SUNAT.
