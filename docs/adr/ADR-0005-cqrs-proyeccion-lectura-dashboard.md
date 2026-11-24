# ADR-0005 — CQRS / proyección de lectura para el dashboard

**Estado:** Propuesto (aceptación pendiente de evidencia de revisión del equipo)
**Fecha consignada en borrador:** 22 de noviembre de 2026 (validación pendiente)

## Contexto

El dashboard necesita indicadores agregados (stock, alertas, flujo de pedidos, planta). La consigna aclara que el dashboard **no es la fuente de verdad** y que las actualizaciones en vivo usan una **proyección de lectura**.

## Decisión

Mantener una **proyección de lectura** optimizada para el dashboard, alimentada por los hechos de negocio del broker. El dashboard **solo lee** esa proyección; las **acciones** (aprobar sugerencia, reservar stock) se dirigen a la capacidad responsable a través de la capa de aplicación.

## Consecuencias

**Positivas:**
- Consultas rápidas sin acoplar el dashboard a las tablas transaccionales.
- La proyección puede ser eventual y etiquetar su frescura.

**Costos / riesgos:**
- Duplicación controlada de datos (derivada) que debe mantenerse sincronizada.
- Posible desfase entre la proyección y el stock real (hay que informarlo).

**Vínculos:** Issue [#9](https://github.com/asmunozv/Deber2/issues/9) · [Requisitos de calidad](../sprint-3/13-REQUISITOS-CALIDAD.md)
