# KPIs

Última actualización: 2026-10-31 (precarga: todavía sin datos del export).
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
| Ventas diarias promedio | pendiente | — | esperar primer export |
| Platos/día promedio | pendiente | — | esperar primer export |
| Ticket promedio | pendiente | — | esperar primer export |
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
