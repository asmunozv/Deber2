# ADR-0004 — Interacciones síncronas vs. asíncronas + Outbox

**Estado:** Aceptado
**Fecha:** 22 de noviembre de 2026

## Contexto

La consigna propone combinar interacciones **síncronas** (consultas y comandos inmediatos) con **mensajería asíncrona** (hechos de negocio). Hay que decidir qué interacciones son inmediatas y cuáles eventuales.

## Decisión

- **Síncrono** cuando la operación exige respuesta inmediata y consistencia: validar SKU, reservar unidades, confirmar salida, consultar disponibilidad.
- **Asíncrono** para propagar **hechos de negocio** a consumidores eventuales (proyección de lectura, Lakehouse, Reposición, Dashboard).
- El registro de un hecho y su notificación se mantienen en la **misma transacción** mediante el patrón **Outbox**.

## Consecuencias

**Positivas:**
- Consistencia fuerte donde se necesita; desacoplamiento donde se tolera desfase.
- El Outbox evita que un movimiento quede sin notificar.

**Costos / riesgos:**
- Consistencia eventual en lecturas (hay que informar el desfase al usuario).
- Reintentos y duplicados posibles (mitigado con idempotencia, ADR-0005 y [11-PATRONES.md](../sprint-3/11-PATRONES.md)).

**Vínculos:** Issue [#9](https://github.com/asmunozv/Deber2/issues/9) · [C4](../sprint-2/05-C4-ARQUITECTURA.md) · [Flujo recepción](../sprint-2/07-FLUJOS-RECEPCION-REPOSICION.md)
