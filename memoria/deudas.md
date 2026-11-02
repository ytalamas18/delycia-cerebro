# Deudas

Última actualización: 2026-11-02 (pagos con comprobante; el préstamo de 5.000 queda descartado).
Fuente de verdad para proveedores registrados en el POS: `datos/cuentas_por_pagar.csv` y `datos/pagos_deuda.csv`.
Este archivo lleva además lo que no está en el POS (préstamo del dueño, Siesam si no se registra).

## Deudas con terceros

| Acreedor | Monto inicial (Bs) | Plan | Pagos | Saldo (Bs) |
|---|---:|---|---|---:|
| Siesam (sistema anterior) | 1.800,00 | 3 cuotas mensuales de 600 | 02/11: 600,00 (1.ª cuota, Yasser vía Peso #232467) | 1.200,00 |
| Carne | 1.215,00 | a definir | — | 1.215,00 |
| Papas | 780,00 | a definir | — | 780,00 |
| Barril de cerveza (Thelen Enrique, barril lager del 25/08) | 700,00 | — | 30/10: 700,00 (Yasser vía Peso #226297) | 0,00 ✅ |
| Abarrotes | 581,00 | a definir | — | 581,00 |
| Verduras | 386,00 | a definir | — | 386,00 |
| Sueldo Samuel (Bailaba Mollo Samuel) | 823,50 | — | 30/10: 823,50 (Yasser vía Peso #226287) | 0,00 ✅ |
| Sueldo Yaque (Yaquelin Torres Choque) | 683,33 (corregido por Yasser; antes 688,33) | — | 30/10: 683,33 (Yasser vía Peso #226284) | 0,00 ✅ |
| Mozzarella 2 kg | ≈ 140,00 | a definir | — | ≈ 140,00 |
| **Total** | **≈ 7.108,83** | | **2.806,83** | **≈ 4.302,00** |

Cálculo saldo: 1.200 + 1.215 + 780 + 581 + 386 + 140 = 4.302,00 (= 7.108,83 − 2.806,83).
Sin Siesam (proveedores de comida): 4.302 − 1.200 = 3.102,00.

## Pagos de Yasser con su dinero (comprobantes del 28/10 al 02/11)

| Fecha | A quién | Concepto | Bs | Medio |
|---|---|---|---:|---|
| 28/10 | Cuenta Banco Ganadero 1310753162 | Alquiler **octubre 2026** (el comprobante dice "noviembre"; Yasser corrigió: es octubre) | 2.000,00 | BCP, trx 0726102800224079 |
| 30/10 | Yaquelin Torres Choque | Sueldo adeudado | 683,33 | Peso #226284 |
| 30/10 | Samuel Bailaba Mollo | Sueldo adeudado | 823,50 | Peso #226287 |
| 30/10 | Thelen Enrique | Barril lager del 25/08 | 700,00 | Peso #226297 |
| 02/11 | Soluciones Informáticas Siesam | 1.ª cuota | 600,00 | Peso #232467 |
| | | **Total** | **4.806,83** | |

2.000 + 683,33 + 823,50 + 700 + 600 = 4.806,83.
✅ Yasser (02/11): estos pagos **son** su préstamo al negocio. Los 5.000 Bs se ignoran (descartados).
Registro compartido: Google Sheet **Préstamo Yasser** en Drive `Agente Delycia` (ID `1gNcXK6Jl1Cy1sT5DySDRmCFAZTzjEnauPbQO0TG06yU`).

## Deuda con el dueño

| Acreedor | Monto (Bs) | Plan | Pagos | Saldo (Bs) |
|---|---:|---|---|---:|
| Préstamo de Yasser (pagos 28/10–02/11, tabla de arriba) | 4.806,83 | sin urgencia de devolución; va al final de la prioridad | — | 4.806,83 |

Es **préstamo**, no venta ni capital: no suma a ventas ni a ganancia.
Si Yasser pone más plata, se agrega aquí y en el Sheet "Préstamo Yasser".

## ~~Reparto propuesto del préstamo de 5.000~~ — ❌ DESCARTADO (02/11: Yasser dice ignorar los 5.000)

| Destino | Bs |
|---|---:|
| Sueldos (Samuel 823,50 + Yaque 688,33) | 1.511,83 |
| Siesam, 1.ª cuota | 600,00 |
| Verduras (total) | 386,00 |
| Papas (total) | 780,00 |
| Abarrotes (total) | 581,00 |
| Carne (a cuenta) | 141,17 |
| Reserva de caja | 1.000,00 |
| **Total** | **5.000,00** |

Si se aplica tal cual, la deuda con terceros queda en **3.113,83 Bs**:
Siesam 1.200 (2 cuotas) + carne 1.073,83 + cerveza 700 + mozzarella ≈ 140.
(7.113,83 − 4.000,00 pagados = 3.113,83.)

Al confirmar: registrar cada pago en la columna "Pagos" (fecha y monto) y en el POS como abono
(medio **Transferencia** si el dinero no sale del cajón, para no descuadrar el cierre).
