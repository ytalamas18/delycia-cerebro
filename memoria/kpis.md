# KPIs

Última actualización: 2026-11-01 (primer export: 17/10–31/10).
Cada número dice de dónde sale. Si falta un dato, queda "pendiente" (no se estima sin avisar).

## Fórmulas

| KPI | Fórmula | Fuente |
|---|---|---|
| Ventas diarias | Σ `total_bs` del día | `ventas_por_dia.csv` |
| Ticket promedio | total_bs ÷ tickets | `ventas_por_dia.csv` |
| Platos/día | Σ `platos` del día | `ventas_por_dia.csv` |
| Food cost % | compras de insumos del período ÷ ventas del período × 100 | `gastos.csv` (tipo `insumo`) + `ventas_por_dia.csv` |
| Prime cost % | (insumos + sueldos) ÷ ventas × 100 | ídem + sueldos en `gastos.csv` |
| Margen por plato | precio − costo de receta | `ventas_por_plato.csv` + recetas del POS |
| Punto de equilibrio (platos/día) | costos fijos mensuales ÷ días abiertos ÷ (precio promedio − costo variable por plato) | ver abajo |

## Valores actuales

| KPI | Valor | Período | Estado |
|---|---|---|---|
| Ventas diarias promedio | 1.030,73 Bs | 17/10–31/10 | 15.461 ÷ 15 días |
| Platos/día promedio | 22,2 | 17/10–31/10 | 333 platos ÷ 15 días |
| Ticket promedio | 70,28 Bs | 17/10–31/10 | 15.461 ÷ 220 tickets (un ticket puede tener varios platos) |
| Precio plato del día | ≈ 38 Bs | — | ⚠️ confirmar con datos |
| Food cost % | pendiente | — | faltan compras de insumos en el POS |
| Prime cost % | pendiente | — | faltan sueldos mensuales |
| Punto de equilibrio | pendiente | — | faltan costos fijos |

## Punto de equilibrio — datos que faltan
- Costos fijos mensuales: alquiler 2.000 Bs ✅ · luz ❓ · agua ❓ · gas ❓ · sueldos ❓ · otros ❓.
- Días abiertos por mes ❓.
- Costo variable por plato (insumos) ❓.

## Historial semanal
| Semana | Ventas (Bs) | Platos | Ticket prom. | Food cost % | Nota |
|---|---:|---:|---:|---:|---|
| — | | | | | |
