# ADR-0003 — Propiedad de datos: fuente autorizada única

**Estado:** Propuesto (pendiente de ratificación del equipo)
**Fecha:** por definir (sin fecha real asignada)

## Contexto

La regla de diseño exige que cada dato tenga un dueño claro y que los datos **no se modifiquen directamente desde otro servicio**. Sprint 1 documentó el riesgo R04 (duplicación de propiedad del stock) y la decisión D02.

## Decisión

Cada clase de dato tiene **una única fuente autorizada**. El resto de capacidades solo consulta o solicita cambios mediante interacciones conceptuales. La matriz completa está en [06-PROPIEDAD-DE-DATOS.md](../sprint-2/06-PROPIEDAD-DE-DATOS.md).

Casos clave:
- **SKU y ubicación maestra** → Catálogo; **saldo en ubicación** → Inventario.
- **Pedido** → Fulfillment; **compromiso de unidades en lotes** → Inventario.
- **Dashboard y Analítica** no son fuentes de verdad (solo lecturas derivadas).

## Consecuencias

**Positivas:**
- Elimina duplicación de escritura y sobreasignación de stock.

**Costos / riesgos:**
- Operaciones que abarcan dos propietarios (reserva, despacho) requieren coordinación explícita (ver ADR-0006).

**Vínculos:** Issue [#6](https://github.com/asmunozv/Deber2/issues/6) · [Propiedad de datos](../sprint-2/06-PROPIEDAD-DE-DATOS.md)
