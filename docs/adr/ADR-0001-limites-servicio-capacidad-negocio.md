# ADR-0001 — Límites de servicio por capacidad de negocio

**Estado:** Aceptado
**Fecha:** 22 de noviembre de 2026

## Contexto

La consigna pide una plataforma empresarial que pueda evolucionar hacia microservicios y exige que cada responsabilidad tenga un dueño claro. Sprint 1 identificó siete capacidades y dejó abierta la pregunta **D01** (cómo agrupar límites lógicos en contenedores).

## Decisión

Modelar **siete capacidades de negocio** como límites lógicos de servicio:

Catálogo, Inventario, Reposición, Fulfillment, Flota, Dashboard y Analítica.

Cada capacidad es propietaria de sus datos y expone interacciones conceptuales. **No se decide aquí el número de procesos desplegables** (eso es ADR-0002).

## Consecuencias

**Positivas:**
- Responsabilidades y propiedad de datos explícitas y trazables.
- El modelo no depende de una decisión de despliegue concreta.

**Costos / riesgos:**
- Riesgo de fragmentar de más si se confunde "capacidad" con "microservicio obligatorio" (mitigado por ADR-0002).

## Alternativas consideradas

| Alternativa | Rechazada porque |
|---|---|
| Un único servicio monolítico sin límites | No permite razonar sobre propiedad ni evolución |
| Más de siete capacidades (ej. separar muelles de flota) | Fragmentación sin justificación de negocio en el MVP |

**Vínculos:** Issue [#5](https://github.com/asmunozv/Deber2/issues/5) · [C4](../sprint-2/05-C4-ARQUITECTURA.md) · [Propiedad de datos](../sprint-2/06-PROPIEDAD-DE-DATOS.md)
