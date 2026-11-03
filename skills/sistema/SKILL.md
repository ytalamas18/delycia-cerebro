---
name: sistema
description: Usar cuando la pregunta es sobre el sistema POS de Delycia (delycia-pos) — cómo hacer algo en una pantalla (abrir caja, vender, cobrar, fiar, anular, cerrar, cargar compras o gastos, inventario, recetas, usuarios), quién puede hacer qué, por qué un número del sistema no cuadra (arqueo, fiados, stock), o para detectar en los datos algo mal registrado.
---

# Sistema POS de Delycia (delycia-pos)

App web propia (reemplazó a Siesam en oct-2026). Corre en una EC2 de AWS; se entra por el navegador con
**usuario + PIN de 4 dígitos**. Tiempo real: la Cocina ve las comandas al instante. Montos en Bs.
Si algo de aquí no coincide con lo que Yasser ve en pantalla, manda lo que él ve (la app pudo cambiar): anotarlo.

> **Mejoras v2 (delycia-pos `main` 2548528, 02/11/2026): listas en código, FALTA DESPLEGAR en la EC2.** Hasta que se
> desplieguen, en pantalla sigue lo de antes (botón "Enviar a cocina", sin retiros, sin Caja y bancos). Lo marcado
> **[v2]** abajo vale después del despliegue. Al desplegar: respaldo antes y cargar saldos iniciales de las 3 cuentas.

## 1. Pantallas y quién las usa

| Pantalla | Para qué | Rol por defecto |
|---|---|---|
| **POS** | Tomar pedidos: canal Local o PEYA, comer aquí / para llevar (por ítem), mesa, cliente, nota | Caja, Admin |
| **Órdenes** | Órdenes abiertas: "Por pagar" y "Pagadas, esperando cocina" | Caja, Admin |
| **Cocina** (KDS) | Comandas: pendiente → en preparación → lista (= entregada); mensajes de caja | Cocina, Admin |
| **Cuentas por cobrar** | Fiados: quién debe, cuánto, registrar abonos | Caja, Admin |
| **Historial** | Órdenes de hoy y días anteriores, con detalle y anuladas aparte | Caja, Admin |
| **Cierre** | Apertura de caja (fondo inicial) y cierre con arqueo efectivo/QR/tarjeta; [v2] sección Retiros | Caja, Admin |
| **Retiro de efectivo** [v2] | Botón en la barra superior, todo el día: monto + motivo (sin PIN); anulable con motivo solo el mismo día | Caja, Admin (`cash.withdraw`) |
| **Caja y bancos** [v2] (`/caja-bancos`) | Libro Efectivo / Banco (QR) / ATC-PeYa con saldo acumulado; traspasos con comisión; saldos iniciales; PDF/Excel. Reemplaza el cuaderno | Solo Admin (se puede dar a otro rol en Roles) |
| **Catálogo** | Ítems, precios, categorías, modificadores, recetas y costo, carga rápida Excel | Admin |
| **Compras** | Proveedores, compras (contado/crédito/parcial), pagos y abonos, cuentas por pagar | Admin |
| **Inventario** | Stock, kárdex, ingreso (producción propia), conteo físico, salida rápida | Admin (salida rápida: también Caja) |
| **Reportes** | Ventas por canal, productos, anulaciones, fiados, stock, mermas, compras, por pagar, [v2] **Pagos a proveedores** (por fecha del pago, método/cuenta, n° comprobante) (PDF/Excel) | Admin |
| **Ajustes** | % recargo PEYA, tiempos y mensajes rápidos de cocina | Admin |
| **Usuarios** | Usuarios, roles y permisos por pantalla, resetear PIN | Admin |

Roles: **Admin** (todo), **Caja** (POS, cobrar, descuento, anular con autorización, historial, fiados, mensajes a
cocina, apertura/cierre, ver Cocina, salida rápida), **Cocina** (ver y atender comandas). Los permisos se cambian en
Usuarios → Roles. Nada se borra: usuarios, roles e ítems se **desactivan**.

## 2. El día en el sistema (orden correcto)

1. **Apertura de caja** (Cierre → Apertura): fondo inicial en efectivo. **Obligatoria antes de vender, una por día
   y NO se puede editar** (ni Admin). Contar bien antes de guardar.
2. **Vender** (POS): agregar ítems → "Enviar a cocina" (solo manda lo nuevo) → la orden queda **Por pagar**.
   [v2] Ya no hay botón "Enviar a cocina": **Guardar** y **Cobrar** envían solos lo pendiente (Cobrar lo envía
   aunque luego se cierre la ventana sin cobrar). Queda el botón solo en "Pagadas, esperando cocina" para órdenes viejas.
3. **Cobrar**: efectivo (calcula vuelto), QR, tarjeta, PEYA o **Cuenta por cobrar** (fiado, exige nombre del
   cliente). Se puede pagar mixto. Descuento opcional (solo quien tiene permiso). Una orden pagada no se modifica.
4. La orden pasa a **Cerrada** sola cuando cocina marca todas sus comandas como listas.
5. **Gastos del día pagados con el cajón** (gas, delivery, compras al paso): registrarlos en **Compras** como compra
   **contado en efectivo** el mismo día → aparecen en el cierre como "Pagos a proveedores" y el arqueo cuadra.
6. **Cierre**: contar efectivo, revisar QR (banco) y tarjeta (datáfono); escribir motivo si hay diferencia.
   **Efectivo esperado = fondo + efectivo de ventas + efectivo cobrado de fiados − pagos a proveedores en efectivo.**
   [v2] **Esperado = fondo + efectivo de ventas + cobros de fiado en efectivo − pagos a proveedores con cuenta de
   origen Efectivo − retiros − traspasos desde Efectivo.** (Un pago en efectivo marcado con cuenta Banco, ej. plata
   del cajero, ya no descuadra la caja.)
7. [v2] **Retiros** (plata que sale del cajón sin ser pago a proveedor): botón "Retiro de efectivo" con motivo, así
   no aparece como faltante. **Depósitos** de efectivo o de ATC/PeYa al banco: Admin → Caja y bancos → traspaso.

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

- [v2] **Pagos a proveedores:** campos nuevos **cuenta de origen** (Efectivo / Banco QR / ATC-PeYa; por defecto
  según el método, editable) y **n° de comprobante/referencia** (n° de transferencia/QR o recibo).
- [v2] **Libro de caja y bancos:** ventas cobradas = 1 línea por día y medio (EFECTIVO→Efectivo, QR→Banco,
  TARJETA/PEYA→ATC-PeYa); fiado entra solo al cobrarse; compras a crédito solo al pagarse; pagos, cobros de fiado,
  retiros y traspasos uno por uno. Faltante/sobrante del cierre = línea "Diferencia de arqueo" (Efectivo = lo
  contado). Traspaso: se escribe lo que sale y lo que llega; la diferencia queda sola como "Comisión". Traspasos
  desde Efectivo solo con fecha de hoy; **hacia Efectivo no se permiten** (pendiente de decidir). Saldo inicial: uno
  por cuenta con fecha; se corrige anulándolo y cargando otro; puede ser negativo.

## 4. Errores típicos y cómo detectarlos en `datos/`

| Señal en los datos | Causa probable | Qué hacer |
|---|---|---|
| `cierres_caja.diferencia_bs` negativa con nota "gas", "delivery", "compra" | Gasto pagado del cajón sin registrar | Registrarlo como compra contado efectivo ese día |
| Diferencia por "cambio", "suelto" o "QR" | Vuelto dado por QR o al revés | Anotar; si se repite, tener más sencillo en el fondo |
| Fondo de apertura ≠ efectivo contado del cierre anterior | Apertura mal escrita (no editable) | Contar antes de abrir; explicar en la nota del cierre |
| `gastos.csv` vacío | No se registran compras ni gastos | Sin esto no hay food cost, margen ni equilibrio: pedirlo |
| `fiado_bs` alto vs total del día | Mucho fiado | Revisar `cuentas_por_cobrar.csv` y cobrar los saldos viejos |
| Muchas `ordenes_anuladas` | Errores al tomar pedido o mal uso | Revisar motivos en Reportes → Anulaciones |
| [v2] Faltante en el cierre por plata sacada del cajón | Retiro no registrado | Registrar con "Retiro de efectivo" ese mismo día |
| Pagos de sueldo en notas del cierre | Sueldos pagados del cajón sin registrar | Registrar en Compras (Gastos operativos → Sueldo) |

## 5. Lo que el sistema NO hace (todavía)

- No hay módulo de gastos propio (se usa Compras). No registra préstamos del dueño (van en `memoria/deudas.md`).
- No hay ficha de clientes (solo el nombre en el fiado). No hay tiempos de cocina en reportes.
- [v2] Sin traspasos hacia Efectivo; el libro de caja y bancos solo lo ve Admin (darlo a Harumi: decidir).
- La apertura de caja no se corrige. Una venta cobrada de un día anterior no se anula.
- Los PDF no muestran emojis.
- Para cambios en el sistema (nueva función, error): eso es otro repo (`delycia-pos`); anotarlo como pendiente en
  `estado.md` y decirle a Yasser que lo pida en una sesión de ese repo.
