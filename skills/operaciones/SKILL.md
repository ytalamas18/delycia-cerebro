---
name: operaciones
description: Usar para el día a día de Delycia — compras y proveedores (qué comprar, comparar precios, registrar en el POS), mermas y rendimientos (pruebas de peso, papa frita), personal y turnos, y el menú del día (qué platos ofrecer y el mensaje de difusión de WhatsApp).
---

# Operaciones de Delycia

Reglas: números en Bs y kg, decir la fuente, marcar lo estimado, no inventar precios.

## 1. Compras y proveedores
- **Precio por unidad base** = monto_bs ÷ cantidad (`gastos.csv`, ojo con la columna `unidad`). Comparar
  contra la compra anterior del mismo concepto: si sube más de lo normal, avisar con Bs y %.
- **Cómo registrar en el POS** (para que el export lo vea):
  - Insumos: compra normal, ítem tipo Insumo/Ingrediente.
  - Gastos fijos y sueldos: categoría **"Gastos operativos"**, ítem tipo Insumo, unidad "unidad", sin stock.
  - A crédito: elegir proveedor; cada pago después es un abono.
  - Pagos que no salen del cajón (préstamo, bolsillo de Yasser): medio **Transferencia** + nota, para no
    descuadrar el cierre de caja.
- Con deudas: priorizar proveedores que dan crédito y no cortar con los críticos (carne, papas, verduras).

## 2. Mermas y rendimientos
```
rendimiento = peso útil ÷ peso facturado        merma % = (1 − rendimiento) × 100
costo real por kg útil = precio por kg facturado ÷ rendimiento
```
- **Papa frita:** ≈ 470 g por kg facturado (rendimiento 0,47): ≈ 48 % pérdida al freír + ≈ 2 % faltante del
  proveedor. Referencia teórica que usaba: 37,5 % de merma. ⚠️ Pendiente confirmar con más muestras.
- **Protocolo de prueba** (repetir 5 veces, días distintos): pesar lo facturado → pesar al recibir (faltante) →
  pesar pelado/limpio → pesar cocido/frito. Anotar cada peso. Usar el promedio y mostrar mínimo y máximo.
- Mermas de inventario: conteos físicos del POS (diferencias en el kárdex). Si una merma se repite, buscar causa
  (porción, recepción, robo, vencimiento) antes de subir precios.

## 3. Personal y turnos
- Atención 18:00–23:30; la preparación es antes. Equipo y sueldos en `memoria/estado.md`.
- **Costo de personal %** = sueldos del período ÷ ventas del período × 100 (entra en el prime cost).
- Si se proponen cambios de turno: comparar platos/día que se atienden vs horas pagadas
  (`platos por hora-persona = platos del día ÷ horas trabajadas totales`).
- Sueldos adeudados van primero en el plan de pagos (ver skill finanzas).

## 4. Menú del día
- **Elegir platos:** priorizar los de mejor margen (skill finanzas §3) y los que más salen
  (`ventas_por_plato.csv`); usar lo que ya hay en stock antes de que se pierda.
- **Mensaje de difusión de WhatsApp** (cuando Yasser comparta la foto de la pizarra), en español, natural y
  con emojis:
  1. Saludo según el día (**verificar el día de la semana** en hora de La Paz).
  2. Platos del día con precio (**leer bien los precios** de la pizarra; si no se leen, preguntar).
  3. Platos fijos.
  4. Horario 18:00 a 23:30.
  5. Dirección: Av. San Pablo de Tarso esq. Las Hortensias, al lado del Cond. La Pradera.
  6. Contacto: 33212850.
  7. Contexto especial si lo hay (feriado, evento).
- Se escribe **Delycia** (no "DelyGia").
