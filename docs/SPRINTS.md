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
| Product Owner | Pendiente |
| Scrum Master / facilitador | Pendiente |
| Líder de arquitectura | Pendiente |
| Equipo de diseño | Pendiente |

> Este documento registra la **planificación**, no constituye evidencia de que los cuatro sprints ya se ejecutaron.


## Planificación de roles, tiempo y presupuesto (propuesta ajustable)

> **Importante:** el enunciado exige registrar responsables y cuatro sprints de dos semanas, pero no establece número de integrantes, tarifa horaria ni presupuesto. Los valores siguientes son una **estimación académica ilustrativa**, no gastos ejecutados ni fechas acordadas por el equipo. Sustituir cuando se confirme la composición del grupo.

### Roles y responsabilidades
| Rol | Función en los sprints | Asignación nominal |
|---|---|---|
| Product Owner | Priorizar historias, definir alcance MVP y aceptar incrementos | Por confirmar |
| Scrum Master / facilitador | Organizar planificación, review y retrospectiva, registrar bloqueos | Por confirmar |
| Líder de arquitectura | Revisar límites de servicio, propiedad de datos, C4, UML y ADR | Por confirmar |
| Equipo de diseño | Preparar backlog, diagramas, matriz, mockups, informe y presentación | Por confirmar |

**Distribución orientativa si son 3 personas:** integrante A = Product Owner + artefactos de producto; integrante B = Scrum Master + seguimiento/trazabilidad; integrante C = líder de arquitectura + revisión técnica. Los tres colaboran en el diseño y revisan trabajo de otro integrante. No confundir los roles con personas adicionales.

### Calendario y capacidad estimada
- **Duración total:** 8 semanas, 4 sprints × 2 semanas.
- **Escenario de cálculo:** 3 personas × 6 horas por semana cada una = 18 horas de equipo/semana, o **36 horas de equipo por sprint**.
- **Capacidad total:** 144 horas-persona. Incluye planificación, elaboración, revisión y retrospectiva.
- **Fechas de inicio y fin:** por definir con el equipo (no se presume que los sprints ya comenzaron).

| Sprint | Semanas relativas | Resultado | Horas-persona estimadas | Costo de trabajo estimado (USD) |
|---|---|---|---:|---:|
| Sprint 1 | 1–2 | Visión, MVP, backlog, límites iniciales | 36 | 288 |
| Sprint 2 | 3–4 | C4, UML, propiedad de datos, ADR | 36 | 288 |
| Sprint 3 | 5–6 | Interacciones, patrones, SOLID, calidad | 36 | 288 |
| Sprint 4 | 7–8 | Dashboard, trazabilidad, informe y presentación | 36 | 288 |
| **Total base** | **8 semanas** | | **144** | **1.152** |

### Presupuesto referencial
Se usa una **tarifa ficticia de valoración del tiempo de USD 8 por hora-persona**, exclusivamente para estimar el esfuerzo del proyecto académico. No implica pagos al equipo.

| Concepto | Fórmula | Valor estimado (USD) |
|---|---|---:|
| Trabajo del equipo | 3 × 6 horas/semana × 8 semanas × USD 8/h | 1.152,00 |
| GitHub + diagramas y documentación gratuitos | Supuesto: uso de herramientas sin costo | 0,00 |
| Contingencia por cambios y correcciones | 10 % del costo base | 115,20 |
| **Presupuesto referencial total** | | **1.267,20** |

**Costo monetario esperado:** USD 0 si el equipo no recibe remuneración y usa herramientas gratuitas. El valor USD 1.267,20 representa tiempo valorizado más contingencia, no dinero que necesariamente se gaste.

**Fórmula para adaptar el cálculo:** presupuesto = (número de integrantes × horas semanales por integrante × 8 × tarifa por hora) × 1,10 + costos adicionales reales.

### Dedicación propuesta por persona en cada sprint (6 h/semana)
- Planificación y seguimiento: 2 h por sprint.
- Elaboración de historias, diagramas o documentos: 8 h por sprint.
- Revisión cruzada y ajustes: 1 h por sprint.
- Revisión del sprint y retrospectiva: 1 h por sprint.

**Por confirmar antes de iniciar:** integrantes, roles definitivos, disponibilidad semanal, fecha de inicio, presupuesto real y acuerdos de revisión. Las estimaciones no reemplazan el registro efectivo de horas y resultados.
