# Sprint 3 — Requisitos de calidad

**Issue:** [#13](https://github.com/asmunozv/Deber2/issues/13) · **Versión:** 1.0 · **Estado:** terminado (revisión registrada) · **Responsable principal (rol):** Líder de arquitectura (Laura Reyes)

Cada requisito se redacta de forma **verificable** y se justifica su umbral. Los umbrales son **propuestas académicas** (no hay carga real; ver supuesto S01).

## 1. Seguridad

| ID | Requisito verificable | Justificación |
|---|---|---|
| Q-SEG-01 | Toda operación sensible (recepción, ajuste, reserva, aprobación de compra, despacho) requiere una **identidad autenticada** y un **rol con permiso** explícito; un usuario sin permiso no puede ejecutarla | Protege operaciones que alteran stock o compromisos |
| Q-SEG-02 | Las operaciones de escritura registran **quién** y **cuándo** las ejecutó (trazabilidad de auditoría) | Exigido para ajustes (RB-02) y revisiones |
| Q-SEG-03 | El repositorio **no contiene secretos** (claves, tokens, credenciales); se validan con una revisión de PR | Evita filtraciones |
| Q-SEG-04 | Los roles se separan: **consulta** no implica **reserva** ni **ajuste** (ISP) | Principio de menor privilegio |

## 2. Disponibilidad

| ID | Requisito verificable | Justificación |
|---|---|---|
| Q-DISP-01 | Si el **broker** cae, las operaciones síncronas de negocio (recepción, reserva, despacho) **siguen disponibles**; solo se aplaza la propagación asíncrona | Aísla el camino crítico del transporte de eventos |
| Q-DISP-02 | Si una **dependencia externa** (ERP, transportista) no responde, el flujo degrada con **Circuit Breaker** y no bloquea la recepción ni la reserva | Evita fallos en cascada |
| Q-DISP-03 | Si la **telemetría** de flota no llega, el dashboard conserva el **último estado conocido** y lo marca como desactualizado | No inventar datos (coherencia con DAS-01) |
| Q-DISP-04 | Disponibilidad objetivo de la plataforma: **99,9 %** mensual para el camino recepción → reserva → despacho | Umbral de referencia para un sistema operativo interno |

## 3. Rendimiento

| ID | Requisito verificable | Justificación |
|---|---|---|
| Q-REND-01 | El **95 % de las consultas de disponibilidad** de un SKU responde en **menos de 200 ms** bajo carga normal | Lectura frecuente del tablero y de reserva |
| Q-REND-02 | El **95 % de las operaciones de reserva FEFO** responde en **menos de 500 ms** (transacción local) | Operación crítica de confirmación |
| Q-REND-03 | El **95 % de los eventos de recepción** se refleja en la vista del dashboard en **menos de 5 segundos** bajo carga normal | Umbral de frescura propuesto (consistencia eventual) |

## 4. Escalabilidad

| ID | Requisito verificable | Justificación |
|---|---|---|
| Q-ESC-01 | **Inventario** escala **vertical** (más recursos) y puede replicarse en lectura **horizontalmente** sin separar la escritura del stock | Es el cuello de botella de escritura |
| Q-ESC-02 | **Proyección de lectura** y **Dashboard** escalan **horizontalmente** por ser solo lectura | Se aíslan del camino transaccional |
| Q-ESC-03 | La **Analítica / Lakehouse** escala de forma **independiente** bajo picos de consulta histórica | No compite con las transacciones |
| Q-ESC-04 | La señal para escalar es el **tiempo de respuesta p95** y la **tasa de eventos** del broker | Señales medibles y operables |

## 5. Consistencia

| ID | Requisito verificable | Justificación |
|---|---|---|
| Q-CON-01 | Recepción, movimiento y reserva usan **transacción local** (saldo y movimiento atómicos) | ADR-0004, ADR-0006 |
| Q-CON-02 | La **proyección de lectura**, el **Lakehouse** y las **alertas de reposición** aceptan **consistencia eventual**, con indicación de frescura | ADR-0005, riesgo R06 |
| Q-CON-03 | El compromiso de reserva **nunca excede** el stock físico elegible | Invariante FEFO (R01, R03) |

## 6. Mantenibilidad

| ID | Requisito verificable | Justificación |
|---|---|---|
| Q-MANT-01 | Cada capacidad tiene **límite y dato propietario** documentados; un cambio debe indicar qué capacidad y ADR afecta | Facilita evolución sin impactos no previstos |
| Q-MANT-02 | Diagramas C4/UML y ADR están **versionados** y su cambio queda trazado a una historia | Ver [16-VERSIONAMIENTO.md](../sprint-4/16-VERSIONAMIENTO.md) |
| Q-MANT-03 | Los patrones y decisiones se justifican con problema/ubicación/consecuencias | Ver [11-PATRONES.md](11-PATRONES.md) |

## Criterios de aceptación de #13

- [x] Requisitos verificables de seguridad, disponibilidad, rendimiento, escalabilidad, consistencia y mantenibilidad.
- [x] Umbrales propuestos y justificados.
- [x] Vínculo con ADR, patrones y riesgos.
- [ ] Revisión por otro integrante.

**Relaciones:** [Matriz de interacciones](10-MATRIZ-INTERACCIONES.md) · [Patrones](11-PATRONES.md) · [ADR](../sprint-2/09-ADR.md).
