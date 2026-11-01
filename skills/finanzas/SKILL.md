---
name: finanzas
description: Usar cuando la pregunta es de plata en Delycia — flujo de caja, cuánto y a quién pagar de las deudas, costo y margen de un plato, food cost %, prime cost, punto de equilibrio en platos por día, cierre diario (costo/gasto/ganancia) o P&L mensual.
---

# Finanzas de Delycia

Reglas: todo en Bs, **siempre mostrar el cálculo**, decir la fuente (archivo/columna) y marcar lo estimado.
Si falta un dato, listarlo como "falta" y no rellenarlo. No usar referencias de la industria como hechos.

## 1. Flujo de caja (dinero real)
- **Entradas** = efectivo + QR + tarjeta (+ PEYA cuando se liquida) de `ventas_por_dia.csv`
  + abonos de fiados (`cuentas_por_cobrar.csv`, cambio de `cobrado_bs`). El fiado del día NO es entrada.
- **Salidas** = pagos de `pagos_deuda.csv` (contado y abonos) + gastos pagados fuera del POS que diga Yasser.
- El préstamo de Yasser es entrada de caja, pero no venta.
- Formato: `Saldo inicial + entradas − salidas = saldo final`. Alertar si el saldo proyectado de la semana
  queda por debajo de la reserva de caja (hoy 1.000 Bs propuesto, ver `deudas.md`).

## 2. Plan de pago de deudas
1. Disponible semanal = ganancia semanal real (o estimada, marcada) − reserva mínima.
2. Prioridad (sin intereses conocidos): (a) sueldos; (b) proveedores sin los que no se opera (carne, papas,
   verduras); (c) acuerdos con fecha (Siesam, 600 Bs/mes); (d) el resto; (e) préstamo de Yasser al final.
3. Dentro del mismo nivel: primero la deuda más chica (se cierra antes y libera crédito con ese proveedor).
4. Salida: tabla `acreedor | pago esta semana | saldo después`, y semanas estimadas para quedar en 0.
5. Si hay intereses o cortes de servicio, eso cambia la prioridad: preguntar.

## 3. Costo y margen por plato
```
costo ingrediente = (precio de compra por kg ÷ rendimiento) × kg usados
costo plato       = Σ costo ingredientes (+ envase si es para llevar)
margen Bs         = precio − costo plato
margen %          = margen Bs ÷ precio × 100
```
- Rendimiento = peso útil ÷ peso facturado. Papa frita: 0,47 (pendiente confirmar) → 1 kg útil cuesta
  precio por kg ÷ 0,47.
- Precio de compra: último de `gastos.csv` (monto_bs ÷ cantidad, cuidando la `unidad`).

## 4. Food cost % y prime cost %
```
food cost %  = compras de insumos del período ÷ ventas del período × 100      (gastos.csv tipo=insumo)
prime cost % = (insumos + sueldos del período) ÷ ventas del período × 100
```
- Con pocas semanas de datos el food cost por compras es ruidoso (se compra un día y se usa varios): avisar.
- Si hay costo de receta por plato, calcular también el food cost teórico = Σ(costo plato × cantidad) ÷ ventas.

## 5. Punto de equilibrio (platos por día)
```
costos fijos/día        = costos fijos mensuales ÷ días abiertos al mes
margen de contribución  = precio promedio por plato − costo variable por plato
platos/día de equilibrio = costos fijos/día ÷ margen de contribución
```
EJEMPLO ilustrativo (no son datos reales): fijos 6.000 Bs/mes, 26 días → 230,77 Bs/día; precio 38 −
costo 15 = 23 Bs → 230,77 ÷ 23 = **10,03 → 11 platos/día** (siempre redondear hacia arriba).
Hoy solo se conoce el alquiler (2.000 Bs): listar los fijos que faltan.

## 6. Cierre diario (costo / gasto / ganancia)
```
ventas del día   = total_bs (ventas_por_dia.csv)
costo            = ventas × food cost %            (último de kpis.md; si no hay → "falta")
gasto            = costos fijos mensuales ÷ días abiertos
ganancia         = ventas − costo − gasto
```
Agregar: diferencia de caja (`cierres_caja.csv`) y pagos de deuda del día.

## 7. P&L mensual
```
Ventas                                   (Σ total_bs del mes)
− Costo de insumos                       (gastos tipo=insumo)
= Margen bruto                    (y % sobre ventas)
− Sueldos
− Alquiler (2.000)
− Servicios (luz, agua, gas)
− Otros gastos operativos
= Resultado operativo             (y % sobre ventas)
```
Debajo, aparte (flujo, no resultado): pagos de deuda del mes, préstamo recibido/devuelto, saldo de deuda
al cierre. Comparar con el mes anterior cuando exista.
