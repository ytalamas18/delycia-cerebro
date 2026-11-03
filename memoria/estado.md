# Estado actual de Delycia

Última actualización: 2026-11-03.

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
| Samuel | (rol: pendiente) | Sueldo adeudado pagado 30/10 (823,50) |
| Yaque | (rol: pendiente) | Sueldo adeudado pagado 30/10 (683,33) |

## Números clave
| Dato | Valor | Estado |
|---|---|---|
| Alquiler | 2.000 Bs/mes | ✅ fijo; se paga a fin del mes en curso (~día 28). Octubre pagado el 28/10 por Yasser; **noviembre vence ~28/11** |
| Luz (CRE) | factura 681 / 712,30 / 742 (ago/sep/oct); a pagar −250 = 431 / 462,30 / 492 | ⚠️ "−250" sin confirmar; ago–oct impagos |
| Agua (Saguapac) | factura 108,95 / 196,87 / 99,01 (ago/sep/oct); a pagar −80 = 28,95 / 116,87 / 19,01 | ⚠️ "−80" sin confirmar; ago–oct impagos |
| Gas | pendiente | ❓ sin registros |
| Sueldos mensuales (planilla) | pendiente | ❓ |
| Precio plato del día | ≈ 38 Bs | ⚠️ confirmar con `datos/ventas_por_plato.csv` |
| Deuda con terceros | ≈ 6.552,13 Bs | al 02/11 (Siesam 1.200 + comida 3.102 + luz 1.385,30 + agua 164,83 + barril 700); ver `deudas.md` |
| Préstamo de Yasser al negocio | 4.806,83 Bs | pagos 28/10–02/11 (los 5.000 de antes quedan descartados); Sheet "Préstamo Yasser" |
| Ventas diarias promedio | ≈ 1.031 Bs | 17/10–31/10: 15.461 Bs ÷ 15 días (`ventas_por_dia.csv`) |
| Food cost % | pendiente | faltan compras de insumos registradas |

## Caja (saldos de inicio de mes, dados por Yasser)
| Fecha | Efectivo (Bs) | Cuenta bancaria (Bs) | Total (Bs) | Nota |
|---|---:|---:|---:|---|
| 2026-11-01 (inicio de noviembre) | 56,70 | 1.792,79 | 1.849,49 | Efectivo = fondo de apertura del 01/11 en `cierres_caja.csv` ✅. Cuenta = saldo de inicio de noviembre, antes de las ventas del 01/11 ✅ |

Cálculo: 56,70 + 1.792,79 = 1.849,49. Es el saldo inicial para el flujo de caja de noviembre.

**Cómo entra el dinero QR:** los cobros QR caen en una **cuenta puente**; de ahí se consolidan y se hace un solo
depósito a la cuenta del negocio (la de 1.792,79). ⚠️ Pendiente: saldo de la cuenta puente al 01/11 y cada cuánto se
pasa a la cuenta principal (si tenía saldo, también es caja del negocio).

## Sistemas y datos
- **Siesam** (sistema anterior): cortado por deuda. Se le deben 1.800 Bs en 3 cuotas mensuales de 600.
- **Sistema propio (`delycia-pos`)**: 1–2 semanas de ventas registradas. Export diario 01:00 → `datos/`.
- **Mejoras v2 del POS** (02/11, `main` 2548528): envío automático a cocina, retiros de efectivo, cuenta de origen y
  n° de comprobante en pagos, reporte "Pagos a proveedores" y **libro de caja y bancos** (reemplaza el cuaderno).
  **Listo en código, falta desplegar** en la EC2. Detalle en `skills/sistema/SKILL.md` ([v2]).
- Gastos operativos (alquiler, luz, sueldos...) se registran en el POS como compras de la categoría
  "Gastos operativos" (`datos/gastos.csv`, tipo `gasto_operativo`). El préstamo NO va en el POS.
- No hay registros previos de gastos ni costos fijos. Al 01/11 `gastos.csv` está vacío (no se registran compras).
- Fiado pendiente al 03/11: 1.820 Bs en 23 órdenes (`cuentas_por_cobrar.csv`). **Tope: 400 Bs por persona** (desde 03/11).
  ⚠️ Sin confirmar: ¿"eli" (210) es Dña. Ely y es distinta de "elizabeth" (478)?

## Datos operativos conocidos
- Papa frita: ≈ 470 g por kg facturado (≈ 48 % pérdida al freír + ≈ 2 % faltante del proveedor). Referencia
  teórica era 37,5 % de merma. ⚠️ Confirmar con muestras más grandes.
- En reportes viejos de Siesam, "SALCHIPAPA CLASICA" = salchipapa de pollo.

## Pendientes de dato (pedir a Yasser)
1. Gas: monto mensual. Luz y agua: ¿qué es el "−250" (CRE) y el "−80" (Saguapac)? ¿Fecha de corte de CRE?
2. Sueldos mensuales de cada persona (no solo lo adeudado) y roles de Samuel y Yaque.
3. Fechas de las cuotas de Siesam (la 1.ª se pagó el 02/11).
4. Precio exacto de la mozzarella (≈ 140 Bs por 2 kg).
5. ¿Los proveedores (carne, papas, abarrotes, verduras) están cobrando ya? ¿Fechas?
6. **Revisar al terminar la carga en el POS:** cómo manejar la merma de la papa (1 kg cruda ≠ 1 kg frita) en
   compras, inventario y recetas. Yasser pidió no tratarlo todavía.

7. **POS v2:** desplegar (respaldo antes) y cargar saldos iniciales de Efectivo / Banco (QR) / ATC-PeYa en Caja y
   bancos. Decidir: ¿la cuenta puente del QR es la cuenta "Banco"? ¿Harumi ve el libro? ¿traspasos hacia Efectivo?

8. **Tiempo de preparación por plato** (minutos): no está en el archivo de costos ni en el export. Pedir a Dña. Ely
   cronometrar o pedir en delycia-pos un reporte de tiempos de cocina (el KDS guarda las horas). Para decidir qué
   platos sacar de la carta.

## En espera (no considerar)
- Cierre del 30/10: "cuentas pagadas de yaque −285, samuel −200 y michael −112" (cajón). Yasser lo revisa con
  Harumi; **no tomarlo en cuenta** hasta que avise.
