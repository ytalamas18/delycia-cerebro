---
name: sistema
description: Usar cuando la pregunta es sobre el sistema POS de Delycia (delycia-pos) — cómo hacer algo en una pantalla (abrir caja, vender, cobrar, fiar, anular, cerrar, cargar compras o gastos, inventario, recetas, usuarios), quién puede hacer qué, por qué un número del sistema no cuadra (arqueo, fiados, stock), o para detectar en los datos algo mal registrado.
---

# Sistema POS de Delycia (delycia-pos)

App web propia (reemplazó a Siesam en oct-2026). Corre en una EC2 de AWS; se entra por el navegador con
**usuario + PIN de 4 dígitos**. Tiempo real: la Cocina ve las comandas al instante. Montos en Bs.
Si algo de aquí no coincide con lo que Yasser ve en pantalla, manda lo que él ve (la app pudo cambiar): anotarlo.

## 1. Pantallas y quién las usa

| Pantalla | Para qué | Rol por defecto |
|---|---|---|
| **POS** | Tomar pedidos: canal Local o PEYA, comer aquí / para llevar (por ítem), mesa, cliente, nota | Caja, Admin |
| **Órdenes** | Órdenes abiertas: "Por pagar" y "Pagadas, esperando cocina" | Caja, Admin |
| **Cocina** (KDS) | Comandas: pendiente → en preparación → lista (= entregada); mensajes de caja | Cocina, Admin |
| **Cuentas por cobrar** | Fiados: quién debe, cuánto, registrar abonos | Caja, Admin |
| **Historial** | Órdenes de hoy y días anteriores, con detalle y anuladas aparte | Caja, Admin |
| **Cierre** | Apertura de caja (fondo inicial) y cierre con arqueo efectivo/QR/tarjeta | Caja, Admin |
| **Catálogo** | Ítems, precios, categorías, modificadores, recetas y costo, carga rápida Excel | Admin |
| **Compras** | Proveedores, compras (contado/crédito/parcial), pagos y abonos, cuentas por pagar | Admin |
| **Inventario** | Stock, kárdex, ingreso (producción propia), conteo físico, salida rápida | Admin (salida rápida: también Caja) |
| **Reportes** | Ventas por canal, productos, anulaciones, fiados, stock, mermas, compras, por pagar (PDF/Excel) | Admin |
| **Ajustes** | % recargo PEYA, tiempos y mensajes rápidos de cocina | Admin |
| **Usuarios** | Usuarios, roles y permisos por pantalla, resetear PIN | Admin |

Roles: **Admin** (todo), **Caja** (POS, cobrar, descuento, anular con autorización, historial, fiados, mensajes a
cocina, apertura/cierre, ver Cocina, salida rápida), **Cocina** (ver y atender comandas). Los permisos se cambian en
Usuarios → Roles. Nada se borra: usuarios, roles e ítems se **desactivan**.

## 2. El día en el sistema (orden correcto)

1. **Apertura de caja** (Cierre → Apertura): fondo inicial en efectivo. **Obligatoria antes de vender, una por día
   y NO se puede editar** (ni Admin). Contar bien antes de guardar.
2. **Vender** (POS): agregar ítems → "Enviar a cocina" (solo manda lo nuevo) → la orden queda **Por pagar**.
3. **Cobrar**: efectivo (calcula vuelto), QR, tarjeta, PEYA o **Cuenta por cobrar** (fiado, exige nombre del
   cliente). Se puede pagar mixto. Descuento opcional (solo quien tiene permiso). Una orden pagada no se modifica.
4. La orden pasa a **Cerrada** sola cuando cocina marca todas sus comandas como listas.
5. **Gastos del día pagados con el cajón** (gas, delivery, compras al paso): registrarlos en **Compras** como compra
   **contado en efectivo** el mismo día → aparecen en el cierre como "Pagos a proveedores" y el arqueo cuadra.
6. **Cierre**: contar efectivo, revisar QR (banco) y tarjeta (datáfono); escribir motivo si hay diferencia.
   **Efectivo esperado = fondo + efectivo de ventas + efectivo cobrado de fiados − pagos a proveedores en efectivo.**

## 3. Reglas que explican los números

- **Día de negocio** = fecha en hora de La Paz. Las órdenes se numeran desde 1 cada día.
- **Venta ≠ dinero:** el fiado cuenta como venta del día de la orden; el dinero entra el día del abono.
- **PEYA:** precio = (lista + extras) × (1 + % de Ajustes), redondeado al Bs. Orden PEYA se cobra solo con PEYA.
- **Anulaciones:** de un ítem (solo si la orden está por pagar) o de la orden entera; motivo obligatorio. Caja
  necesita **usuario y PIN de quien autoriza** (Admin u otro con "Autorizar anulaciones"). Orden ya cobrada: solo el
  mismo día (el pago queda como devuelto). Fiado con abonos: no se anula. Cocina ve el aviso hasta "Entendido".
- **Compras:** el gasto cuenta en la **fecha de compra** aunque se pague después; el dinero sale en la fecha de cada
  pago. Para anular una compra hay que anular antes sus pagos.
- **Gastos operativos** (alquiler, luz, agua, gas, sueldos, Siesam): compra de un ítem de la categoría
  **"Gastos operativos"** (tipo Insumo, unidad "unidad", sin "suma al inventario"). Proveedor = a quién se paga.
- **Tipos de ítem:** Normal (se vende tal cual, ej. bebida), Preparado (se vende y tiene receta), Ingrediente (se
  produce en cocina, no se vende), Insumo (se compra, no se vende). El POS solo muestra Normal y Preparado.
- **Recetas y costo:** en Catálogo → ítem → "Receta y costo" (puede variar para llevar / comer aquí). El costo usa
  el **último costo de compra** de cada insumo → sin compras registradas, el costo de receta no sirve.
- **Inventario:** stock = suma de movimientos (kárdex), nunca se edita a mano. Ventas descuentan según receta; compras
  suman; anular revierte. Conteo físico registra la diferencia (merma o sobrante). Stock negativo = falta registrar
  una compra o la receta está mal.
- **Fiados:** el cliente es el **nombre escrito** (sin teléfono). "Juan Pérez" y "juan perez" se juntan; dos
  personas con el mismo nombre también.

## 4. Errores típicos y cómo detectarlos en `datos/`

| Señal en los datos | Causa probable | Qué hacer |
|---|---|---|
| `cierres_caja.diferencia_bs` negativa con nota "gas", "delivery", "compra" | Gasto pagado del cajón sin registrar | Registrarlo como compra contado efectivo ese día |
| Diferencia por "cambio", "suelto" o "QR" | Vuelto dado por QR o al revés | Anotar; si se repite, tener más sencillo en el fondo |
| Fondo de apertura ≠ efectivo contado del cierre anterior | Apertura mal escrita (no editable) | Contar antes de abrir; explicar en la nota del cierre |
| `gastos.csv` vacío | No se registran compras ni gastos | Sin esto no hay food cost, margen ni equilibrio: pedirlo |
| `fiado_bs` alto vs total del día | Mucho fiado | Revisar `cuentas_por_cobrar.csv` y cobrar los saldos viejos |
| Muchas `ordenes_anuladas` | Errores al tomar pedido o mal uso | Revisar motivos en Reportes → Anulaciones |
| Pagos de sueldo en notas del cierre | Sueldos pagados del cajón sin registrar | Registrar en Compras (Gastos operativos → Sueldo) |

## 5. Lo que el sistema NO hace (todavía)

- No hay módulo de gastos propio (se usa Compras). No registra préstamos del dueño (van en `memoria/deudas.md`).
- No hay ficha de clientes (solo el nombre en el fiado). No hay tiempos de cocina en reportes.
- La apertura de caja no se corrige. Una venta cobrada de un día anterior no se anula.
- Los PDF no muestran emojis.
- Para cambios en el sistema (nueva función, error): eso es otro repo (`delycia-pos`); anotarlo como pendiente en
  `estado.md` y decirle a Yasser que lo pida en una sesión de ese repo.
