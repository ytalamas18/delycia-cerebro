# datos/

Los genera el export diario del POS (16:00 La Paz). **No editar a mano:** cada corrida los reescribe.
`ultimo_export.txt` dice cuándo fue el último. Montos en Bs con punto decimal. Fechas = día de negocio.

| CSV | Qué tiene |
|---|---|
| `ventas_por_dia.csv` | tickets, platos, items, total, descuentos, efectivo/QR/tarjeta/PEYA/fiado, anuladas |
| `ventas_por_plato.csv` | por día, plato y canal: cantidad, precio promedio, total (antes del descuento) |
| `gastos.csv` | líneas de compra; `tipo` = `insumo` o `gasto_operativo` |
| `pagos_deuda.csv` | pagos a proveedores; `tipo` = `contado` o `abono` |
| `cuentas_por_pagar.csv` | saldo pendiente por compra (foto del día) |
| `cuentas_por_cobrar.csv` | fiados pendientes |
| `cierres_caja.csv` | arqueo diario y diferencias |

Solo suman las órdenes pagadas o cerradas. Lo fiado es venta del día aunque el dinero entre después.
