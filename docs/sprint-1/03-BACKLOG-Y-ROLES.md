# Sprint 1 — Backlog priorizado, dependencias y roles

> **Estado verificado (auditoría 24/11/2026):** documento disponible. Los usuarios GitHub ya están asignados; los comentarios de revisión cruzada y los cierres deben contrastarse con las issues. El Sprint 1 no se declara cerrado formalmente mientras #1 y #2 no tengan revisión independiente y falte la retrospectiva.


**Issue:** [#3](https://github.com/asmunozv/Deber2/issues/3) · **Versión:** 1.0 · **Estado:** artefacto redactado; validación documental pendiente

## 1. Criterios de priorización
Se propone ordenar historias por: **(1)** riesgo para la consistencia de existencias y despachos, **(2)** necesidad para completar el recorrido vertical, **(3)** dependencias de otros módulos y **(4)** valor informativo para operación.

- **P0 / imprescindible:** definición del flujo integral del MVP conceptual.
- **P1 / importante:** diseño complementario que puede postergarse sin perder coherencia en el flujo inicial.
- **P2 / evolución:** capacidades analíticas y exploratorias que no bloquean los flujos centrales.
- **Sprint previsto:** momento de **profundización del artefacto de diseño**, no fecha en que se construye software. **Todas las historias se formulan en Sprint 1**.
- **Responsable académico:** integrante asignado a la tarea en el backlog; los usuarios GitHub correspondientes ya están asignados en las issues.

## 2. Backlog ordenado (historias de producto)
| Orden | Historia | Prioridad | Dependencia principal | Rol validador propuesto | Diseño detallado previsto | MVP |
|---:|---|---|---|---|---|---|
| 1 | CAT-01 — SKU | P0 | Ninguna | Encargado de catálogo | S2 | Sí |
| 2 | CAT-02 — Reglas de lote | P0 | CAT-01 | Operador de recepción | S2 | Sí |
| 3 | INV-01 — Recepción | P0 | CAT-01, CAT-02 | Encargado de almacén | S2 | Sí |
| 4 | INV-02 — Disponibilidad | P0 | INV-01 | Encargado de almacén | S2 | Sí |
| 5 | FUL-01 — Reserva FEFO | P0 | INV-02, CAT-02 | Coordinador de pedidos | S2 | Sí |
| 6 | FUL-02 — Despacho | P0 | FUL-01, INV-02 | Operador de despacho | S2 | Sí |
| 7 | REP-01 — Alerta de reposición | P0 | INV-02 | Planificador de compras | S2 | Sí |
| 8 | FLT-01 — Asignación vehículo | P1 | FUL-02 | Coordinador de flota | S3 | Sí |
| 9 | DAS-01 — Tablero operativo | P1 | INV-02, REP-01, FUL-02 | Supervisor | S4 | Sí |
| 10 | REP-02 — Revisión de propuesta | P1 | REP-01 | Planificador de compras | S3 | No |
| 11 | FLT-02 — Seguimiento de entrega | P1 | FLT-01 | Coordinador de flota | S3 | No |
| 12 | DAS-02 — Detalle de lotes | P2 | DAS-01, INV-02 | Encargado de almacén | S4 | No |
| 13 | ANA-01 — Tendencias | P2 | INV-01, FUL-02 | Analista | S4 | No |
| 14 | ANA-02 — Caducidad y alertas | P2 | CAT-02, REP-01 | Gerente | S4 | No |

**Distinción importante:** que FLT-01 o DAS-01 sea P1 no contradice su inclusión en el alcance funcional mínimo: el **diseño básico** se incluye como dependencia del flujo y el análisis detallado/prototipo puede llegar después. El MVP solo delimita un recorrido conceptual, sin promesa de implementación.

### Camino crítico del recorrido de negocio
`CAT-01 → CAT-02 → INV-01 → INV-02 → FUL-01 → FUL-02 → FLT-01`  
Rama de control: `INV-02 → REP-01 → DAS-01` y `FUL-02 → DAS-01`.

### Orden de negociación si el equipo reduce alcance
1. Mantener la propiedad de existencias y la secuencia recepción → disponibilidad → reserva FEFO → despacho.
2. Mantener REP-01 para documentar el caso de alerta y reposición, aunque su aprobación (REP-02) permanezca futura.
3. Reducir FLT-01 a asignación conceptual y DAS-01 a lectura agregada.
4. Posponer FLT-02, REP-02, DAS-02 y ANA-01/ANA-02.

## 3. Backlog académico (GitHub Issues)
| Sprint | Issues | Entregable definido | Estado verificable en esta rama |
|---|---|---|---|
| S1 | [#1](https://github.com/asmunozv/Deber2/issues/1) | Visión, actores y MVP | Cerrado en GitHub; revisión cruzada pendiente de regularizar |
| S1 | [#2](https://github.com/asmunozv/Deber2/issues/2) | 7 épicas, 14 historias y criterios | Cerrado en GitHub; revisión cruzada pendiente de regularizar |
| S1 | [#3](https://github.com/asmunozv/Deber2/issues/3) | Backlog, dependencias, roles y tablero | Cerrado; comentario de revisión de Ariana registrado |
| S1 | [#4](https://github.com/asmunozv/Deber2/issues/4) | Límites, riesgos, supuestos y decisiones | Cerrado; comentario de revisión de Ariana registrado |
| S2 | [#5–#9](https://github.com/asmunozv/Deber2/issues?q=is%3Aissue+%22Sprint+2%22) | C4, datos, UML, ADR | Entregable redactado; cierre pendiente |
| S3 | [#10–#14](https://github.com/asmunozv/Deber2/issues?q=is%3Aissue+%22Sprint+3%22) | Interacciones, patrones, SOLID y calidad | Entregable redactado; cierre pendiente |
| S4 | [#15–#19](https://github.com/asmunozv/Deber2/issues?q=is%3Aissue+%22Sprint+4%22) | Trazabilidad, prototipo e informe | Entregable redactado; cierre pendiente |

Las 19 issues tienen entregables documentales; su cierre real y revisión se comprobarán individualmente en GitHub.

## 4. Roles Scrum y de arquitectura
| Rol | Responsabilidad concreta | Persona asignada | Cómo se confirma |
|---|---|---|---|
| Product Owner (PO) | Validar valor, alcance, orden del backlog y reglas de negocio | **Ariana Muñoz** | Aceptación del equipo y cierre de #3 |
| Scrum Master / facilitadora | Facilitar planificación, seguimiento, review, retro y impedimentos | **Ana Paula López** | Aceptación del equipo y cierre de #3 |
| Líder de arquitectura | Cuidar límites, propiedad de datos, trazabilidad C4/UML/ADR | **Laura Reyes** | Aceptación del equipo y cierre de #3 |
| Equipo de diseño | Redactar y revisar historias, diagramas y decisiones | **Laura Reyes, Ariana Muñoz y Ana Paula López** | Asignaciones registradas por historia |
| Revisor cruzado | Verificar calidad de un entregable que no redactó | Rotativo (Laura ↔ Ariana ↔ Ana) | Comentario/review con autor, fecha y observaciones |

**Asignación GitHub:** Ariana Muñoz (@asmunozv), Ana Paula López (@anypau) y Laura Reyes / Lau (@crazylilypad0801). Los usuarios están asignados en las issues. La revisión cruzada observada y sus pendientes se detallan en [05-REVISION-Y-RETROSPECTIVA.md](05-REVISION-Y-RETROSPECTIVA.md).

## 5. Tablero de seguimiento para el Sprint 1
| Columna | Qué significa | Elementos |
|---|---|---|
| Pendiente de validación | Artefactos redactados, no revisados por otra persona | Ninguno |
| En progreso | Ajustes de acuerdo con comentarios documentados | Ninguno |
| En validación | Se dispone de entregables y enlaces, falta comprobar revisión cruzada y cierre real | #1, #2, #3, #4 |

**Política para mover un issue a Terminado:** el documento está disponible en la rama principal, los criterios están comprobados, otra persona lo revisó, existe evidencia de aceptación y se registra la review/retro correspondiente. Las columnas anteriores son una vista documental inicial; **no** se afirma que exista un tablero de GitHub Projects configurado.

## 6. Trazabilidad de incrementos
| Incremento académico | Issues | Historias de producto afectadas | Evidencia prevista |
|---|---|---|---|
| S1 Visión y alcance | #1–#4 | CAT a ANA (definición) | Estos cuatro documentos, PR y revisión cruzada |
| S2 Modelo arquitectónico | #5–#9 | CAT, INV, REP, FUL y FLT | C4 fuente, propiedad de datos, UML y ADR |
| S3 Justificación y calidad | #10–#14 | Todas, priorizando interacciones críticas | Matrices, patrones, SOLID y requisitos medibles |
| S4 Síntesis y comunicación | #15–#19 | Todas, visualizando DAS-01 | Prototipo, trazabilidad, presentación e informe |

## 7. Criterios de aceptación específicos de #3
- [x] Orden de prioridad, dependencias, sprint de diseño y rol funcional documentados.
- [x] Roles PO, facilitador, arquitectura y equipo definidos en cuanto a responsabilidad.
- [x] Responsables nominales acordados (Ariana Muñoz, Ana Paula López, Laura Reyes).
- [x] Comentario de revisión cruzada de Ariana registrado en la issue #3 (fecha exacta visible en GitHub).
- [x] Issue #3 cerrada en GitHub; la retrospectiva del Sprint 1 sigue pendiente.

**Referencias:** [Historias](02-EPICAS-E-HISTORIAS.md) · [Visión](01-VISION-Y-MVP.md) · [Límites y riesgos](04-LIMITES-Y-RIESGOS.md) · [Revisión/retro](05-REVISION-Y-RETROSPECTIVA.md).
