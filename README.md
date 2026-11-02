# delycia-cerebro

Memoria y skills del agente gerente-asistente de **Delycia**. Repo **privado**: tiene deudas, sueldos y ventas.

## Qué hay
| Ruta | Qué es | Quién escribe |
|---|---|---|
| `CLAUDE.md` | Instrucciones del agente | Yasser |
| `memoria/estado.md` | Foto actual del negocio | Agente (solo, avisa) |
| `memoria/decisiones.md` | Bitácora de decisiones | Agente (solo, avisa) |
| `memoria/deudas.md` | Deudas, plan y pagos | Agente (solo, avisa) |
| `memoria/kpis.md` | Ventas, platos/día, food cost, equilibrio | Agente (solo, avisa) |
| `memoria/charlas/` | Resumen de cada charla (por fecha) | Agente |
| `memoria/drive.md` | Carpeta de Drive del agente (`Agente Delycia`) y su contenido | Agente |
| `datos/` | CSVs del POS, todos los días a la 01:00 | Export automático de la EC2 (no editar a mano) |
| `skills/` | Finanzas, operaciones y sistema POS | Yasser |

## Cómo se usa
1. Abre una sesión de **Claude Code** (app, web o celular) con este repo.
2. El agente lee `estado.md`, las últimas 10 decisiones, los últimos resúmenes de charla y el export más reciente.
3. **Guarda solo** lo nuevo (decisiones, pagos, datos) y avisa con `📝 Guardé: ...`. Para revertir: "deshaz eso".

## Por qué así
- **Archivos en git:** cada cambio de memoria queda en el historial (se puede ver qué cambió y volver atrás).
- **CSVs y no acceso a la base:** el agente nunca tiene credenciales de la DB. El export usa un usuario de
  solo lectura y un deploy key que solo sirve para este repo (detalle en `delycia-pos/docs/infra-agente.md`).
