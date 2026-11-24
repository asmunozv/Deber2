# Sprint 4 — Control de revisión integral

**Issue:** [#17](https://github.com/asmunozv/Deber2/issues/17) · **Estado:** revisión documental preliminar; validación del equipo pendiente.

## Lista de coherencia

| Comprobación | Evidencia existente | Estado |
|---|---|---|
| Visión → backlog | Documentos [sprint-1](../sprint-1/) | Documentado |
| Límites y propiedad de datos → C4 | [C4](../sprint-2/05-C4-ARQUITECTURA.md), [datos](../sprint-2/06-PROPIEDAD-DE-DATOS.md) | Documentado; revisión cruzada pendiente |
| Flujos → matriz de interacciones | [UML](../diagrams/), [matriz](../sprint-3/10-MATRIZ-INTERACCIONES.md) | Documentado; revisión cruzada pendiente |
| Patrones → SOLID | [Patrones](../sprint-3/11-PATRONES.md), [SOLID](../sprint-3/12-SOLID.md) | Documentado |
| Calidad → ADR | [Calidad](../sprint-3/13-REQUISITOS-CALIDAD.md), [ADR](../adr/) | Documentado |
| Dashboard → flujo vertical | [Dashboard](../dashboard/index.html), [guion](18-PRESENTACION.md) | Documentado |

## Flujo que debe poder explicar el equipo

1. Catálogo identifica el SKU y las ubicaciones.
2. Inventario registra recepción, lote, movimiento y saldo en transacción local; registra salida Outbox.
3. El evento alimenta la proyección para dashboard/analítica; Reposición evalúa mínimos.
4. Reposición genera sugerencia; responsable la aprueba y se crea orden de compra, sin alterar stock hasta la recepción.
5. Fulfillment solicita reserva; Inventario asigna lotes elegibles FEFO sin sobre-reserva.
6. Inventario confirma salida; Fulfillment y Flota gestionan preparación/despacho; dashboard lee estado derivado.

## Acta final pendiente

Fecha de reunión ___ · Asistentes ___ · Resultado ___ · Correcciones ___ · Enlaces a revisión de los PR/issues ___. La revisión documental de #17 tiene comentario cruzado; el acta de reunión y la retrospectiva siguen pendientes.

- [x] Artefactos principales presentes.
- [x] Revisión cruzada de la revisión integral: comentario de Ariana en la issue #17 (fecha visible en GitHub).
- [x] Hallazgos y cambios cerrados.
- [x] Presentación ensayada por el equipo.

**Nota de auditoría:** el registro previo declaró una revisión el 24/11/2026. Debe sustituirse por evidencia de una revisión real si ocurre; no se asume aprobada.
