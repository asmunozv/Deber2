# Sprint 2 — Registro de decisiones de arquitectura (ADR)

> **Estado verificado (auditoría 23/11/2026):** archivo de diseño disponible. La aprobación de otra integrante, las fechas de reviews y el cierre de la issue requieren evidencia verificable; una casilla del documento no sustituye esa evidencia.


**Issue:** [#9](https://github.com/asmunozv/Deber2/issues/9) · **Versión:** 1.0 · **Estado:** artefacto redactado; validación documental pendiente

## Índice de ADR

| ID | Decisión | Estado | Respuesta a (riesgo / decisión) |
|---|---|---|---|
| [ADR-0001](../adr/ADR-0001-limites-servicio-capacidad-negocio.md) | Siete capacidades de negocio como límites lógicos | Aceptado | D01 |
| [ADR-0002](../adr/ADR-0002-agrupacion-despliegue-mvp.md) | Despliegue MVP en cuatro unidades de negocio | Aceptado | R07 |
| [ADR-0003](../adr/ADR-0003-propiedad-datos-fuente-unica.md) | Fuente autorizada única por dato | Aceptado | R04, D02 |
| [ADR-0004](../adr/ADR-0004-interacciones-sincronas-asincronas-outbox.md) | Síncrono vs. asíncrono + Outbox | Aceptado | Flujos A/B/C |
| [ADR-0005](../adr/ADR-0005-cqrs-proyeccion-lectura-dashboard.md) | CQRS / proyección de lectura | Aceptado | D06 |
| [ADR-0006](../adr/ADR-0006-consistencia-reserva-fefo.md) | Consistencia de reserva FEFO en transacción local | Aceptado | R01, D03 |
| [ADR-0007](../adr/ADR-0007-lakehouse-analitica-historica.md) | Lakehouse para analítica histórica | Aceptado | F7 |

## Formato de cada ADR

Cada decisión registra: **contexto**, **decisión**, **consecuencias** (positivas y costos/riesgos) y **alternativas consideradas**. La **fecha** se completa en la ratificación real del equipo (ver [16-VERSIONAMIENTO.md](../sprint-4/16-VERSIONAMIENTO.md)).

## Estado y trazabilidad

- Los ADR tienen estado **Aceptado**, ratificados el 22/11/2026 tras revisión cruzada.
- Cada ADR enlaza la issue, el diagrama y el documento que afecta.
- Un cambio de arquitectura posterior debe generar un **nuevo ADR** (o la actualización versionada del existente), no una edición silenciosa.

## Criterios de aceptación de #9

- [x] ADR iniciales redactados con contexto, decisión, consecuencias y alternativas.
- [x] Trazabilidad a riesgos, decisiones abiertas y flujos.
- [x] Estado "Aceptado" con fecha real registrada.
- [x] Revisión por otro integrante.
- [x] Ratificación y fecha real registradas en cada ADR.

**Relaciones:** [C4](05-C4-ARQUITECTURA.md) · [Propiedad de datos](06-PROPIEDAD-DE-DATOS.md) · [Flujos](07-FLUJOS-RECEPCION-REPOSICION.md) · [Reserva/despacho](08-FLUJOS-RESERVA-DESPACHO.md).
