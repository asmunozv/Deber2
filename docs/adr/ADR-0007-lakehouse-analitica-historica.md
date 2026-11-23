# ADR-0007 — Lakehouse para analítica histórica

**Estado:** Propuesto (pendiente de ratificación del equipo)
**Fecha:** por definir (sin fecha real asignada)

## Contexto

La Analítica necesita histórico de movimientos, rotación, quiebres, vencimientos, puntualidad y predicciones. No debe interferir con las transacciones operativas.

## Decisión

El **broker** carga los hechos de negocio en un **Lakehouse**, que conserva la información para análisis histórico. La Analítica consume del Lakehouse; **no** consulta las bases transaccionales de los servicios.

## Consecuencias

**Positivas:**
- Análisis aislado del camino crítico operativo.
- Datos históricos acumulables sin presión sobre las tablas de negocio.

**Costos / riesgos:**
- Infraestructura y gobierno de datos adicionales (fuera del alcance técnico de esta materia).

**Vínculos:** Issue [#9](https://github.com/asmunozv/Deber2/issues/9) · [C4](../sprint-2/05-C4-ARQUITECTURA.md)
