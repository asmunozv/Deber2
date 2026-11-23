# Sprint 2 — Registro de decisiones de arquitectura (ADR)

**Issue:** [#9](https://github.com/asmunozv/Deber2/issues/9) · **Versión:** 1.0 · **Estado:** propuesta para revisión · **Responsable principal (rol):** Líder de arquitectura (Laura Reyes)

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

Cada decisión registra: **contexto**, **decisión**, **consecuencias** (positivas y costos/riesgos) y **alternativas consideradas**. La **fecha** se completa en la ratificación real del equipo (ver [16-VERSIONAMIENTO.md](../sprint-4/16-VERSIONAMIENTO.md)).

## Estado y trazabilidad

- Los ADR tienen estado **Propuesto** hasta la revisión por otro integrante y el acuerdo del equipo.
- Cada ADR enlaza la issue, el diagrama y el documento que afecta.
- Un cambio de arquitectura posterior debe generar un **nuevo ADR** (o la actualización versionada del existente), no una edición silenciosa.

## Criterios de aceptación de #9

- [x] ADR iniciales redactados con contexto, decisión, consecuencias y alternativas.
- [x] Trazabilidad a riesgos, decisiones abiertas y flujos.
- [x] Estado "Propuesto" sin fabricar fechas ni acuerdos.
- [ ] Revisión por otro integrante.
- [ ] Ratificación y fecha real registradas en cada ADR.

**Relaciones:** [C4](05-C4-ARQUITECTURA.md) · [Propiedad de datos](06-PROPIEDAD-DE-DATOS.md) · [Flujos](07-FLUJOS-RECEPCION-REPOSICION.md) · [Reserva/despacho](08-FLUJOS-RESERVA-DESPACHO.md).
