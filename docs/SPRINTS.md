# Plan de sprints — Smart Inventory

**Materia:** Diseño de Sistemas · **Duración:** 4 sprints de 2 semanas · **Estado:** planificación general; artefactos documentales de Sprint 1 preparados para revisión (sin aprobación formal ni cierre).

## Reglas de seguimiento
- Backlog: [Issues](https://github.com/asmunozv/Deber2/issues). Las tareas se identifican por el prefijo de sprint.
- Cada sprint registra objetivo, historias/tareas, responsable, incremento revisable, revisión y retrospectiva.
- Estados: Pendiente / En progreso / En revisión / Terminado (cerrar el issue solo cuando se cumpla su aceptación).
- No asignar fechas reales ni responsables sin acuerdo del equipo.
- Cada historia terminada enlaza su documento, diagrama fuente, versión o ADR y evidencia de revisión por otro integrante.
- Quedan fuera del alcance APIs, contratos técnicos de mensajes, CI/CD, despliegues y pruebas.

## Definición de terminado (DoD)
- [ ] Se satisfacen los criterios de aceptación del issue.
- [ ] Se identifica el módulo o capacidad propietaria.
- [ ] Se actualizan los diagramas o ADR afectados y se conserva versión e historial.
- [ ] Otro integrante revisa el artefacto.
- [ ] Se adjunta o enlaza evidencia verificable a la historia.
- [ ] Se registra la revisión del sprint y la retrospectiva, sin inventar resultados.

## Sprint 1 — Visión y planificación (2 semanas)
**Objetivo:** acordar visión, MVP, interesados, épicas, historias, backlog y límites candidatos.

**Historias seleccionadas:** [#1](https://github.com/asmunozv/Deber2/issues/1), [#2](https://github.com/asmunozv/Deber2/issues/2), [#3](https://github.com/asmunozv/Deber2/issues/3), [#4](https://github.com/asmunozv/Deber2/issues/4).

**Incremento documental redactado (pendiente de revisión):**
- [Visión, interesados y MVP](sprint-1/01-VISION-Y-MVP.md).
- [Épicas, historias de usuario y criterios](sprint-1/02-EPICAS-E-HISTORIAS.md).
- [Backlog priorizado, dependencias y roles](sprint-1/03-BACKLOG-Y-ROLES.md).
- [Límites candidatos, riesgos y decisiones abiertas](sprint-1/04-LIMITES-Y-RIESGOS.md).
- [Lista de validación, registro para review y retrospectiva](sprint-1/05-REVISION-Y-RETROSPECTIVA.md).

**Responsables:** roles funcionales propuestos; nombres del equipo por asignar. **Fechas:** por definir.  
**Estado de las issues #1–#4:** artefactos elaborados en rama de revisión; pendientes revisión por otra persona, acuerdos reales y criterios de cierre. No cerrarlas por el solo hecho de redactar documentos.

**Revisión:** fecha real pendiente; integrantes y comentarios pendientes; aceptación pendiente.  
**Retrospectiva:** pendiente de reunión y acta real. El documento de control indica los campos por completar.

## Sprint 2 — Arquitectura y flujos (2 semanas)
**Objetivo:** justificar límites y propiedad de datos, modelar C4 y flujos UML, registrar ADR iniciales.

**Historias seleccionadas:** [#5](https://github.com/asmunozv/Deber2/issues/5), [#6](https://github.com/asmunozv/Deber2/issues/6), [#7](https://github.com/asmunozv/Deber2/issues/7), [#8](https://github.com/asmunozv/Deber2/issues/8), [#9](https://github.com/asmunozv/Deber2/issues/9).

**Incremento revisable esperado:** diagramas C4 fuente, matriz de propiedad de datos, flujos de recepción/reposición/reserva/despacho y ADR iniciales.

**Responsables:** por asignar. **Fechas:** por definir.

**Revisión:** fecha: ___; entregables verificados: ___; acuerdos: ___.

**Retrospectiva:** funcionó: ___; mejorar: ___; acción siguiente: ___.

## Sprint 3 — Interacciones, patrones y calidad (2 semanas)
**Objetivo:** completar matriz de interacciones, justificar patrones/SOLID y fijar requisitos medibles, refinando diagramas y decisiones.

**Historias seleccionadas:** [#10](https://github.com/asmunozv/Deber2/issues/10), [#11](https://github.com/asmunozv/Deber2/issues/11), [#12](https://github.com/asmunozv/Deber2/issues/12), [#13](https://github.com/asmunozv/Deber2/issues/13), [#14](https://github.com/asmunozv/Deber2/issues/14).

**Incremento revisable esperado:** matriz arquitectónica por flujo, informe de cuatro o más patrones, evidencia SOLID, requisitos verificables y revisiones de ADR.

**Responsables:** por asignar. **Fechas:** por definir.

**Revisión:** fecha: ___; entregables verificados: ___; acuerdos: ___.

**Retrospectiva:** funcionó: ___; mejorar: ___; acción siguiente: ___.

## Sprint 4 — Coherencia, trazabilidad y entrega (2 semanas)
**Objetivo:** cerrar documentación, trazabilidad y política de versiones; preparar mockups, informe y presentación.

**Historias seleccionadas:** [#15](https://github.com/asmunozv/Deber2/issues/15), [#16](https://github.com/asmunozv/Deber2/issues/16), [#17](https://github.com/asmunozv/Deber2/issues/17), [#18](https://github.com/asmunozv/Deber2/issues/18), [#19](https://github.com/asmunozv/Deber2/issues/19).

**Incremento revisable esperado:** paquete de diseño versionado y coherente; prototipo planta interna/externa; informe PDF o Word y presentación recepción → stock → alerta → reposición.

**Responsables:** por asignar. **Fechas:** por definir.

**Revisión:** fecha: ___; entregables verificados: ___; acuerdos: ___.

**Retrospectiva:** funcionó: ___; mejorar: ___; acción siguiente: ___.

## Roles por completar
| Rol | Responsable |
|---|---|
| Product Owner | Ariana |
| Scrum Master / facilitador | Ana |
| Líder de arquitectura | Lau |
| Equipo de diseño | Lau, Ana y Ariana |

> Este documento registra la **planificación**, no constituye evidencia de que los cuatro sprints ya se ejecutaron.


## Roles, tiempo y presupuesto del equipo

**Equipo (3 personas):** Lau, Ana y Ariana. La asignación siguiente es la propuesta de organización del deber; las tres colaboran en el diseño y realizan revisión cruzada.

| Integrante | Rol principal | Responsabilidad |
|---|---|---|
| **Lau** | Líder del proyecto y líder de arquitectura | Coordina decisiones, define límites y datos propietarios, revisa C4/UML y ADR |
| **Ana** | Scrum Master / facilitadora | Organiza tablero, backlog, seguimiento, revisión/retrospectiva y trazabilidad |
| **Ariana** | Product Owner | Define visión, alcance MVP y criterios de aceptación; coordina prototipo del dashboard y presentación |

### Tiempo: calendario vs. trabajo efectivo
**Se conservan los 4 sprints de 2 semanas indicados en el deber (8 semanas de calendario).** Esto no significa trabajar a tiempo completo: el esfuerzo previsto es **54 horas-persona entre las tres**, aproximadamente **18 horas por persona en todo el trabajo** (promedio 2 h 15 min semanales por persona). Son estimaciones ajustables, no tiempos ya ejecutados.

| Sprint | Plazo formal | Responsable de coordinación | Trabajo previsto | Esfuerzo total del equipo |
|---|---|---|---|---:|
| **1** | Semanas 1–2 | Ariana (producto) + Ana (seguimiento) | Visión, épicas, MVP, backlog y riesgos iniciales | **9 h-persona** |
| **2** | Semanas 3–4 | Lau (arquitectura) | Diagramas C4/UML, límites, propietarios de datos, ADR | **18 h-persona** |
| **3** | Semanas 5–6 | Lau (diseño) + Ana (registro) | Matriz de interacciones, patrones, SOLID, calidad | **15 h-persona** |
| **4** | Semanas 7–8 | Ariana (presentación) + Ana (trazabilidad) | Dashboard, versionamiento, informe y exposición | **12 h-persona** |
| **Total** | **8 semanas formales** | Equipo completo | | **54 h-persona** |

**Tiempos aproximados por actividad:** Sprint 1: issues #1 2 h, #2 2 h, #3 2 h, #4 3 h; Sprint 2: #5 4 h, #6 3 h, #7 4 h, #8 4 h, #9 3 h; Sprint 3: #10 3 h, #11 4 h, #12 3 h, #13 3 h, #14 2 h; Sprint 4: #15 3 h, #16 2 h, #17 2 h, #18 3 h, #19 2 h. **Son horas-persona sumadas, no duración de cada sprint.**

### Presupuesto monetario (USD)
| Concepto | Costo previsto |
|---|---:|
| GitHub (plan gratuito) | **$0** |
| Diagramas y documentación con herramientas gratuitas | **$0** |
| Trabajo académico de los integrantes (no remunerado) | **$0** |
| Suscripción de IA paga, opcional, máximo una mensualidad | **Hasta $20** |
| **Presupuesto máximo previsto** | **$20** |

**Escenario sin suscripción nueva:** $0. **Escenario con suscripción:** hasta $20, si no existen impuestos, comisiones o cargos adicionales; comprobar el total facturado antes de pagar. La estimación **no** incluye laptops, internet u otras herramientas que el equipo ya posee. No se debe tratar como gasto ejecutado.

### Asignación principal y horas estimadas por historia
| Issue | Tema | Responsable principal | Esfuerzo equipo |
|---|---|---|---:|
| #1 | Visión, interesados y MVP | Ariana | 2 h |
| #2 | Épicas e historias | Ariana | 2 h |
| #3 | Backlog y responsabilidades | Ana | 2 h |
| #4 | Límites iniciales y riesgos | Lau | 3 h |
| #5 | C4 y límites de servicio | Lau | 4 h |
| #6 | Propiedad de datos | Lau | 3 h |
| #7 | Recepción y reposición UML | Ana | 4 h |
| #8 | Reserva FEFO y despacho UML | Ariana | 4 h |
| #9 | ADR iniciales | Lau | 3 h |
| #10 | Matriz de interacciones | Ana | 3 h |
| #11 | Patrones y justificación | Lau | 4 h |
| #12 | Evidencia SOLID | Ariana | 3 h |
| #13 | Requisitos de calidad | Lau | 3 h |
| #14 | Revisión de diagramas y ADR | Ana | 2 h |
| #15 | Dashboard interno/externo | Ariana | 3 h |
| #16 | Versionamiento y trazabilidad | Ana | 2 h |
| #17 | Revisión integral | Lau | 2 h |
| #18 | Presentación de flujo | Ariana | 3 h |
| #19 | Informe final y cierre | Ana | 2 h |

Los responsables son dueños de cada entrega, no ejecutores únicos. **No se documentarán revisiones/retrospectivas ficticias**; se rellenarán al cierre real de cada sprint. Las fechas concretas se acuerdan con el equipo.
