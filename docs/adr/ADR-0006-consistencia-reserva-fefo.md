# ADR-0006 — Consistencia de la reserva FEFO

**Estado:** Propuesto (pendiente de ratificación del equipo)
**Fecha:** por definir (sin fecha real asignada)

## Contexto

Dos pedidos concurrentes podrían reservar las mismas unidades (riesgo R01). La reserva debe ser coherente y no exceder el stock físico elegible.

## Decisión

La reserva es una interacción **síncrona** `Fulfillment → Inventario` que se resuelve en una **transacción local** dentro de Inventario:

1. Seleccionar lotes elegibles con criterio FEFO.
2. Verificar disponibilidad (físico − reservado).
3. Comprometer unidades **o** rechazar la reserva completa (sin parcialidad en el MVP).

Esto mantiene la consistencia fuerte donde más importa, sin coordinar una transacción distribuida entre servicios.

## Consecuencias

**Positivas:**
- Sin sobreasignación de stock; una sola decisión consistente por solicitud.
- Simple de razonar y de implementar más adelante.

**Costos / riesgos:**
- Acoplamiento puntual Fulfillment→Inventario en el flujo de reserva.
- Si el MVP evolucionara a reserva parcial, habría que revisar este ADR.

**Vínculos:** Issue [#8](https://github.com/asmunozv/Deber2/issues/8) · [Flujo reserva FEFO](../sprint-2/08-FLUJOS-RESERVA-DESPACHO.md)
