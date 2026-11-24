# Sprint 3 — Informe de patrones de software

> **Auditoría documental (23/11/2026):** el contenido técnico está redactado. Las revisiones, aprobaciones, etiquetas/releases y actos de cierre solo deben declararse realizados si existen evidencias correspondientes en GitHub o actas confirmadas por el equipo.


**Issue:** [#11](https://github.com/asmunozv/Deber2/issues/11) · **Versión:** 1.0 · **Estado:** artefacto redactado; revisión y aceptación pendientes de verificar

Se justifican **siete patrones** (la consigna exige al menos cuatro). Para cada uno: **problema, ubicación, beneficios, costos y límites**.

## 1. Puertos y adaptadores (arquitectura hexagonal)

- **Problema:** el dominio de negocio no debe acoplarse a infraestructura (bases de datos, broker, ERP) que cambia con frecuencia.
- **Ubicación:** todos los contenedores; visible en [`c4-componente-inventario.mmd`](../diagrams/c4-componente-inventario.mmd) (API/puerto de entrada, dominio, repositorios, Outbox).
- **Beneficios:** el dominio queda aislado; se puede sustituir una integración sin tocar reglas de negocio.
- **Costos:** indirección adicional; contratos de puertos que mantener.
- **Límites:** no elimina la necesidad de decidir la especificación técnica de APIs (fuera de esta materia).

## 2. Pub/Sub basado en eventos

- **Problema:** comunicar hechos de negocio sin acoplar directamente productores y consumidores.
- **Ubicación:** el broker central de [`c4-contenedores.mmd`](../diagrams/c4-contenedores.mmd).
- **Beneficios:** desacoplamiento; nuevos consumidores (proyección, Lakehouse) se añaden sin tocar productores.
- **Costos:** consistencia eventual; orden y duplicados deben gobernarse.
- **Límites:** no sirve para operaciones que exigen respuesta inmediata (reserva, salida).

## 3. Outbox + idempotencia

- **Problema:** evitar que un cambio de negocio quede registrado pero sin notificar (o viceversa).
- **Ubicación:** Inventario, Fulfillment y Reposición publican a través de Outbox; los consumidores toleran duplicados (idempotencia).
- **Beneficios:** registro y notificación atómicos; consumidores seguros ante reintentos.
- **Costos:** tabla Outbox y proceso de publicación; cada consumidor debe ser idempotente.
- **Límites:** la entrega puede repetirse; no garantiza orden global por sí solo.

## 4. CQRS / proyección de lectura

- **Problema:** el dashboard necesita una vista agregada optimizada, distinta del modelo transaccional.
- **Ubicación:** proyección de lectura consumida por Dashboard (ver ADR-0005).
- **Beneficios:** lecturas rápidas sin presionar las tablas transaccionales; separa escritura (dueño) de lectura (proyección).
- **Costos:** duplicación de datos derivada que hay que sincronizar.
- **Límites:** la proyección **no** es fuente de escritura; puede tener desfase (consistencia eventual).

## 5. State (máquina de estados)

- **Problema:** garantizar transiciones válidas en pedidos, reservas y órdenes de compra.
- **Ubicación:** [`uml-estados-pedido.mmd`](../diagrams/uml-estados-pedido.mmd), [`uml-estados-reserva.mmd`](../diagrams/uml-estados-reserva.mmd), [`uml-estados-orden-compra.mmd`](../diagrams/uml-estados-orden-compra.mmd).
- **Beneficios:** transiciones explícitas; evita estados imposibles (p. ej., despachar sin reserva).
- **Costos:** más estados que mantener al evolucionar el flujo.
- **Límites:** modela el ciclo de vida, no la persistencia ni la concurrencia.

## 6. Strategy / Adapter

- **Problema:** variar políticas (FEFO, reposición) e integraciones (ERP, transportistas) sin modificar el flujo principal.
- **Ubicación:** selección FEFO en Inventario; cálculo de sugerencia en Reposición; integraciones externas.
- **Beneficios:** nuevas estrategias se agregan sin tocar el caso de uso (abierto/cerrado).
- **Costos:** una abstracción más; riesgo de sobreingeniería si hay una sola estrategia.
- **Límites:** cada estrategia debe respetar el mismo contrato.

## 7. Circuit Breaker / Retry

- **Problema:** limitar el impacto de dependencias inestables (ERP, transportistas, telemetría).
- **Ubicación:** integraciones externas y consumidores del broker.
- **Beneficios:** degradación controlada; evita fallos en cascada.
- **Costos:** reintentos deben ser **selectivos e idempotentes**; complejidad de configuración.
- **Límites:** no sustituye una política de disponibilidad (ver [13-REQUISITOS-CALIDAD.md](13-REQUISITOS-CALIDAD.md)).

## 8. Criterios de aceptación de #11

- [x] Al menos cuatro patrones justificados (se documentan siete).
- [x] Problema, ubicación, beneficios, costos y límites por patrón.
- [x] Vínculo con diagramas y ADR.
- [x] Revisión cruzada registrada: comentario de Ariana en la issue #11 (fecha visible en GitHub).

**Relaciones:** [SOLID](12-SOLID.md) · [Requisitos de calidad](13-REQUISITOS-CALIDAD.md) · [C4](../sprint-2/05-C4-ARQUITECTURA.md).
