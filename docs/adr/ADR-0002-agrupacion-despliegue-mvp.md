# ADR-0002 — Agrupación de despliegue en el MVP

**Estado:** Propuesto (aceptación pendiente de evidencia de revisión del equipo)
**Fecha consignada en borrador:** 22 de noviembre de 2026 (validación pendiente)

## Contexto

La consigna pregunta qué servicios conviene **desplegar por separado** y cuáles **agrupar en el MVP**. Separar las siete capacidades como procesos independientes desde el inicio añade complejidad de operación sin evidencia de escala (riesgo R07).

## Decisión

Partir de la **arquitectura propuesta por la consigna** (servicios + broker + proyección de lectura + Lakehouse), agrupando el despliegue en **cuatro unidades de negocio** en el MVP:

1. **Catálogo + Inventario** (misma vida de datos de stock: el saldo siempre referencia SKU).
2. **Fulfillment** (ciclo de vida del pedido).
3. **Reposición + Flota** (señales de abastecimiento y operación logística).
4. **Dashboard + Analítica** (lectura; sin transacciones propias).

Los límites lógicos se mantienen **aunque** dos capacidades compartan despliegue. La base de datos de cada capacidad permanece **aislada por esquema y permisos**, aunque comparta infraestructura física.

## Consecuencias

**Positivas:**
- Menor coordinación distribuida en el MVP sin sacrificar límites lógicos.
- Evolución a separación real cuando aparezca una señal (carga, frecuencia de cambio, equipo).

**Costos / riesgos:**
- El acoplamiento de despliegue exige disciplina para no cruzar límites lógicos.

## Alternativas consideradas

| Alternativa | Rechazada porque |
|---|---|
| Siete microservicios separados desde el inicio | Complejidad de reserva/consistencia sin evidencia de escala |
| Monolito único sin aislamiento de datos | Contradice la propiedad de datos de la consigna |

**Vínculos:** Issue [#5](https://github.com/asmunozv/Deber2/issues/5) · [C4](../sprint-2/05-C4-ARQUITECTURA.md)
