# Sprint 2 — Registro de decisiones de arquitectura (ADR)

> **Estado verificado (24/11/2026):** los siete ADR están redactados como propuestas. No se declaran aceptados ni ratificados hasta que el equipo registre una aprobación explícita y su fecha.

**Issue:** [#9](https://github.com/asmunozv/Deber2/issues/9) · **Versión:** 1.1 · **Estado:** propuestas documentadas; ratificación pendiente

## Índice de ADR

| ID | Decisión | Estado | Respuesta a (riesgo / decisión) |
|---|---|---|---|
| [ADR-0001](../adr/ADR-0001-limites-servicio-capacidad-negocio.md) | Siete capacidades de negocio como límites lógicos | Propuesto | D01 |
| [ADR-0002](../adr/ADR-0002-agrupacion-despliegue-mvp.md) | Despliegue MVP en cuatro unidades de negocio | Propuesto | R07 |
| [ADR-0003](../adr/ADR-0003-propiedad-datos-fuente-unica.md) | Fuente autorizada única por dato | Propuesto | R04, D02 |
| [ADR-0004](../adr/ADR-0004-interacciones-sincronas-asincronas-outbox.md) | Síncrono vs. asíncrono + Outbox | Propuesto | Flujos A/B/C |
| [ADR-0005](../adr/ADR-0005-cqrs-proyeccion-lectura-dashboard.md) | CQRS / proyección de lectura | Propuesto | D06 |
| [ADR-0006](../adr/ADR-0006-consistencia-reserva-fefo.md) | Consistencia de reserva FEFO en transacción local | Propuesto | R01, D03 |
| [ADR-0007](../adr/ADR-0007-lakehouse-analitica-historica.md) | Lakehouse para analítica histórica | Propuesto | F7 |

## Formato de cada ADR

Cada decisión registra **contexto**, **decisión**, **consecuencias** (positivas y costos/riesgos) y **alternativas consideradas**. La fecha del 22 de noviembre de 2026 que aparece en los ADR corresponde al borrador y no a una ratificación.

## Estado y trazabilidad

- Los ADR permanecen **Propuestos** hasta que el equipo confirme la decisión en una revisión real.
- Los ADR enlazan issues, diagramas y documentos relacionados.
- Un cambio de arquitectura posterior debe generar un **nuevo ADR** (o una actualización versionada y justificada), no una edición silenciosa.
- En la issue #9 existe un intercambio de revisión; la ratificación formal y su fecha siguen pendientes.

## Criterios de aceptación de #9

- [x] Siete ADR redactados con contexto, decisión y consecuencias; se explicitan alternativas consideradas.
- [x] Trazabilidad a riesgos, decisiones abiertas y flujos.
- [x] Estado de los ADR correctamente identificado como **Propuesto** mientras no exista ratificación.
- [x] Comentario de revisión cruzada registrado en la issue #9.
- [x] Ratificación explícita de las decisiones y fecha real confirmadas por el equipo.

**Relaciones:** [C4](05-C4-ARQUITECTURA.md) · [Propiedad de datos](06-PROPIEDAD-DE-DATOS.md) · [Flujos](07-FLUJOS-RECEPCION-REPOSICION.md) · [Reserva/despacho](08-FLUJOS-RESERVA-DESPACHO.md).
