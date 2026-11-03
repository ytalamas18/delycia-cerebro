# Google Drive — carpeta del agente

Última actualización: 2026-11-03.

**El agente solo usa la carpeta `Agente Delycia`** (ID `1YqyLESUm7jfF7GJg7MclB2o419669RW8`, en Mi unidad) y sus
subcarpetas. Lo que esté fuera de ella no se lee, aunque el conector lo permita. Yasser pone ahí los archivos que
quiere que el agente revise (y los cambia o actualiza seguido).

Cómo listarla: buscar con `parentId = '1YqyLESUm7jfF7GJg7MclB2o419669RW8'`; para subcarpetas, repetir con su ID.
Los `.xlsx` se leen directo (sin convertir): el conector devuelve los **valores calculados**, no las fórmulas.
Los Sheets nuevos salen en locale `es_ES`: fórmulas con `;` (`=DATE(2026;10;28)`), no `,`.
Archivos grandes salen largos: buscar la hoja o tabla que se necesita en vez de leer todo.

## Contenido (guía; se actualiza al revisarla)

| Archivo | Para qué | Modificado | ID |
|---|---|---|---|
| Costos Delycia.xlsx | Costos: tabla de insumos (precio real, +20 %, unidad de compra y de receta, precio por unidad), tabla de preparaciones (carne de hamburguesa, milanesas...) y productos | 2026-10-01 (subido el 02/11) | `1_vi322IUp-bl3UkMYjX2U2xGU2yZiNI0` |

Notas de `Costos Delycia.xlsx` (revisado 03/11): el conector lo devuelve como texto plano de ~154 KB (se guarda a
archivo; buscar "Costos totales"). Tabla **Costos totales**: Producto, Costo elaboración, Gastos operativos
(= **38,25 % del PVP**, asignación), Costo total, PVP, Ganancia real, Margen real, PVP/ganancia PeYa, Costo
elaboración proyectado. También: gaseosas (costo y PVP), preparación de carnes (hamburguesa 90 g, milanesa pollo
150 g, carne 140 g, pipoca 250 g, sándwich 110 g), ventas Siesam 01/07–17/09 (79 días) y tablas de PVP
recomendado (Tabla D adoptada 26/09). **No tiene tiempos de preparación.** Nachos Supremos tiene el mismo costo que
Porción de papas (receta incompleta). Almuerzos (caja china, pique macho...) no están.

## Registros (el agente escribe aquí)

| Archivo | Para qué | ID |
|---|---|---|
| Carpeta `Registros` | Lo que el agente mantiene para Yasser y Harumi | `1zWCs8Nae_lVmvmBf9lVnsuHKq90cQduI` |
| Delycia — Registros (Google Sheets) | Pestañas Deudas, Pagos, Decisiones, Pendientes | `1cCv96Z7ciMjgXnERZe-ujPhQ80K07Osof5jwWfA-ghI` |
| Préstamo Yasser (Google Sheets, raíz de `Agente Delycia`) | Pagos de Yasser con su dinero (préstamo) y devoluciones; resumen en J2:J4 | `1gNcXK6Jl1Cy1sT5DySDRmCFAZTzjEnauPbQO0TG06yU` |

Fuera de la carpeta hay archivos de Delycia que el agente **no** lee (Precios_Insumos, Gastos consolidados,
Cierre Diario, Plantilla_Gastos_Ventas...). Si hacen falta, pedirle a Yasser que los copie o mueva a
`Agente Delycia`.
