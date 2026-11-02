# Estado actual de Delycia

Última actualización: 2026-11-02.

## Negocio
- Restaurante casual de comida casera artesanal. Av. San Pablo de Tarso esq. Las Hortensias (al lado del
  Cond. La Pradera), Santa Cruz de la Sierra. Tel. 33212850. Atención **18:00–23:30** (antes 12:00–15:00; cambio informado el 2026-11-01).
- **Situación: crisis.** Deudas con proveedores y personal, ventas bajas, insumos caros.

## Equipo
| Persona | Rol | Nota |
|---|---|---|
| Yasser | Dueño; finanzas, redes y WhatsApp | Trabaja además en remoto (DevOps) |
| Harumi | Control diario de costos, gastos y ventas | |
| Dña. Ely | Cocina | |
| Samuel | (rol: pendiente) | Sueldo adeudado 823,50 Bs |
| Yaque | (rol: pendiente) | Sueldo adeudado 688,33 Bs |

## Números clave
| Dato | Valor | Estado |
|---|---|---|
| Alquiler | 2.000 Bs/mes | ✅ fijo; noviembre pagado el 28/10 por Yasser |
| Luz | pendiente | ❓ sin registros |
| Agua | pendiente | ❓ sin registros |
| Gas | pendiente | ❓ sin registros |
| Sueldos mensuales (planilla) | pendiente | ❓ |
| Precio plato del día | ≈ 38 Bs | ⚠️ confirmar con `datos/ventas_por_plato.csv` |
| Deuda con terceros | ≈ 4.307 Bs | al 02/11 tras pagos de Yasser (era ≈ 7.114); ver `deudas.md` |
| Deuda con Yasser | 5.000 Bs + 4.806,83 Bs | ⚠️ sin confirmar si los 4.806,83 (pagos 28/10–02/11) son aparte del préstamo |
| Ventas diarias promedio | ≈ 1.031 Bs | 17/10–31/10: 15.461 Bs ÷ 15 días (`ventas_por_dia.csv`) |
| Food cost % | pendiente | faltan compras de insumos registradas |

## Sistemas y datos
- **Siesam** (sistema anterior): cortado por deuda. Se le deben 1.800 Bs en 3 cuotas mensuales de 600.
- **Sistema propio (`delycia-pos`)**: 1–2 semanas de ventas registradas. Export diario 01:00 → `datos/`.
- Gastos operativos (alquiler, luz, sueldos...) se registran en el POS como compras de la categoría
  "Gastos operativos" (`datos/gastos.csv`, tipo `gasto_operativo`). El préstamo NO va en el POS.
- No hay registros previos de gastos ni costos fijos. Al 01/11 `gastos.csv` está vacío (no se registran compras).
- Fiado pendiente al 01/11: 1.728 Bs en 21 cuentas (`cuentas_por_cobrar.csv`).

## Datos operativos conocidos
- Papa frita: ≈ 470 g por kg facturado (≈ 48 % pérdida al freír + ≈ 2 % faltante del proveedor). Referencia
  teórica era 37,5 % de merma. ⚠️ Confirmar con muestras más grandes.
- En reportes viejos de Siesam, "SALCHIPAPA CLASICA" = salchipapa de pollo.

## Pendientes de dato (pedir a Yasser)
1. Luz, agua, gas: monto mensual promedio.
2. Sueldos mensuales de cada persona (no solo lo adeudado) y roles de Samuel y Yaque.
3. Confirmar reparto del préstamo de 5.000 Bs (ver `decisiones.md`).
4. Fechas de las cuotas de Siesam.
5. Precio exacto de la mozzarella (≈ 140 Bs por 2 kg).
6. Cierre del 30/10 dice "cuentas pagadas de yaque −285, samuel −200 y michael −112" (efectivo del cajón):
   ¿son pagos de sueldo? ¿Quién es Michael? Ojo: ese mismo 30/10 Yasser pagó por transferencia los sueldos
   adeudados de Yaque (683,33) y Samuel (823,50); los del cajón serían otra cosa.
7. ¿Los pagos de Yasser del 28/10–02/11 (4.806,83 Bs) salieron del préstamo de 5.000 o son aparte?
8. Sueldo adeudado de Yaque: ¿era 688,33 o 683,33? (pagó 683,33).
