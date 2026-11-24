# ADR-0007 — Lakehouse para analítica histórica

**Estado:** Propuesto (aceptación pendiente de evidencia de revisión del equipo)
**Fecha consignada en borrador:** 22 de noviembre de 2026 (validación pendiente)

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

## Alternativas consideradas

| Alternativa | Motivo para no elegirla |
|---|---|
| Consultar directamente bases transaccionales | Compite con operaciones y mezcla cargas analíticas con operativas |
| Mantener solo reportes manuales | No facilita análisis histórico recurrente ni trazabilidad |
| Replicar cada tabla operativa sin modelo histórico | No resuelve por sí solo gobierno, retención y transformación analítica |

**Vínculos:** Issue [#9](https://github.com/asmunozv/Deber2/issues/9) · [C4](../sprint-2/05-C4-ARQUITECTURA.md)
