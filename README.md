# delycia-cerebro

Memoria y skills del agente gerente-asistente de **Delycia**. Repo **privado**: tiene deudas, sueldos y ventas.

## Qué hay
| Ruta | Qué es | Quién escribe |
|---|---|---|
| `CLAUDE.md` | Instrucciones del agente | Yasser |
| `memoria/estado.md` | Foto actual del negocio | Agente (con tu OK) |
| `memoria/decisiones.md` | Bitácora de decisiones | Agente (con tu OK) |
| `memoria/deudas.md` | Deudas, plan y pagos | Agente (con tu OK) |
| `memoria/kpis.md` | Ventas, platos/día, food cost, equilibrio | Agente (con tu OK) |
| `datos/` | CSVs del POS, todos los días a las 16:00 | Export automático de la EC2 (no editar a mano) |
| `skills/` | Finanzas y operaciones | Yasser |

## Cómo se usa
1. Abre un chat en el Proyecto de Claude conectado a este repo.
2. El agente lee `estado.md`, las últimas 10 decisiones y el export más reciente.
3. Al cerrar, di **"actualiza la memoria"**: el agente propone los cambios y solo los aplica si apruebas.

## Por qué así
- **Archivos en git:** cada cambio de memoria queda en el historial (se puede ver qué cambió y volver atrás).
- **CSVs y no acceso a la base:** el agente nunca tiene credenciales de la DB. El export usa un usuario de
  solo lectura y un deploy key que solo sirve para este repo (detalle en `delycia-pos/docs/infra-agente.md`).
