# Sprint 1 — Límites candidatos de diseño y riesgos iniciales

> **Estado verificado (auditoría 23/11/2026):** archivo de diseño disponible. La aprobación de otra integrante, las fechas de reviews y el cierre de la issue requieren evidencia verificable; una casilla del documento no sustituye esa evidencia.


**Issue:** [#4](https://github.com/asmunozv/Deber2/issues/4) · **Versión:** 1.1 · **Estado:** documentado en ADR propuestos (Sprint 2, borrador 22/11/2026); ratificación pendiente

## 1. Criterios para proponer un límite
1. Separar capacidades por **reglas y responsabilidades**, no por cantidad deseada de servicios.
2. Cada dato mutable debe tener una **capacidad propietaria**; otros módulos solo consumen o solicitan cambios mediante interacciones conceptuales.
3. Considerar cohesión, cambios frecuentes, acoplamiento y consistencia antes de separar procesos desplegables.
4. Diferenciar **límite lógico/módulo** de **microservicio físico**. Un límite no exige despliegue independiente.
5. Documentar alternativas, riesgos y acuerdos como ADR en Sprint 2, sin anticipar decisiones aprobadas.

## 2. Mapa candidato de capacidades y propiedad
| Capacidad lógica | Responsabilidad | Datos de los que sería propietaria | Consulta / interacción conceptual |
|---|---|---|---|
| Catálogo | Identidad, atributos y elegibilidad del SKU | SKU, unidad base, estado y política de caducidad | Inventario consulta producto válido |
| Inventario | Stock físico y comprometido, lotes, ubicaciones y movimientos | Lotes almacenados, ubicaciones, saldos, reservas de unidades y trazabilidad del movimiento | Reposición consulta disponibilidad; Fulfillment solicita reserva y salida |
| Reposición | Umbrales, alertas y propuestas de abastecimiento | Umbral por SKU, alertas, estado de propuesta | Reacciona a stock disponible, nunca contabiliza recepción |
| Fulfillment | Estado del pedido, selección de cantidades y confirmación de intención de despacho | Pedidos, sus líneas y estado de preparación/despacho | Pide a Inventario compromiso y salida de existencias |
| Flota | Estado y asignación logística de vehículos | Vehículos, disponibilidad, asignación y estado de entrega | Asocia un recurso al despacho sin editar existencias |
| Dashboard | Presentación de información operativa derivada | Preferencias de visualización y vistas derivadas (no stock original) | Lee indicadores de capacidades propietarias |
| Analítica | Agregaciones e interpretación histórica | Modelos analíticos derivados y series históricas | Utiliza datos de negocio sin ser fuente transaccional |

### Límite especialmente sensible: pedido versus reserva física
- **Fulfillment** es propietario del pedido y sus estados.
- **Inventario** es propietario del **compromiso de unidades en lotes específicos** y de la disponibilidad; la referencia al pedido es necesaria para rastrear la reserva.
- La operación conceptual de reserva debe ser coherente ante solicitudes simultáneas. Una reserva confirmada en pedido **sin** unidades comprometidas en Inventario constituye una inconsistencia de diseño que Sprint 2 deberá tratar.
- El despacho requiere coordinar estado de pedido y salida física sin duplicar descuentos.
- Catálogo define políticas y atributos de SKU; Inventario conserva la instancia de cada lote recibido y su estado de almacenamiento.

## 3. Alternativas de organización arquitectónica
La consigna propone una **arquitectura de referencia** (Figura 1): servicios propietarios de sus datos, una capa de aplicación que coordina el dashboard, un broker que alimenta una proyección de lectura y un Lakehouse, combinando interacciones síncronas y asíncronas. Sobre esa base, la única decisión abierta es **cómo agrupar el despliegue** de las capacidades, sin fragmentar arbitrariamente.

| Alternativa | Ventaja | Riesgo / costo | Evaluación preliminar |
|---|---|---|---|
| A. **Servicios por capacidad + broker + proyección + Lakehouse** (según la consigna) | Responsabilidad y propiedad de datos explícitas; evolución a microservicios | Coordinación distribuida si se separa de más | **Base de la propuesta**; respeta la regla de "un dueño por dato" |
| B. Servicios separados como procesos independientes desde el inicio | Autonomía de despliegue potencial | Complejidad en reservas, consistencia, observabilidad y operación | **No justificada aún**; no confundir capacidades con siete microservicios |
| C. Núcleo transaccional compartido (catálogo/inventario/fulfillment) y capacidades de consulta separables | Reduce acoplamiento en parte crítica | Requiere gobernar datos derivados e interfaces | Alternativa de despliegue para comparar en ADR |

**Propuesta, no decisión aprobada:** representar los límites lógicos según la consigna y resolver la agrupación de despliegue en Sprint 2 mediante ADR (ver [ADR-0001](../adr/ADR-0001-limites-servicio-capacidad-negocio.md) y [ADR-0002](../adr/ADR-0002-agrupacion-despliegue-mvp.md)). La primera entrega C4 representa responsabilidades, no inventa infraestructura técnica.

## 4. Interacciones relevantes (sin contratos técnicos)
| Flujo | Origen → destino | Intención | Consistencia relevante |
|---|---|---|---|
| F1 Recepción | Recepción/Inventario → Catálogo | Validar SKU y política de lote | No contabilizar SKU inválido |
| F1 Recepción | Operador → Inventario | Contabilizar lote en ubicación | Saldo y movimiento concordantes |
| F3 Reposición | Inventario → Reposición | Comunicar disponibilidad para evaluar umbral | Una alerta puede ser eventual; no debe crear stock |
| F4 Reserva | Fulfillment → Inventario | Comprometer lotes elegibles FEFO | Exclusividad para no sobreasignar |
| F5 Despacho | Fulfillment → Inventario | Confirmar salida de unidades reservadas | Sin salida duplicada ni negativa |
| F5 Flota | Fulfillment → Flota | Solicitar asignación a despacho | Evitar doble uso del vehículo |
| F6 Dashboard | Capacidades → Dashboard | Presentar estado resumido | Identificar frescura del dato, sin modificar fuentes |
| F7 Analítica | Capacidades → Analítica | Elaborar tendencias históricas | No confundir proyección histórica con saldo actual |

Estas relaciones expresan intenciones de negocio, **no** definen APIs, eventos técnicos, protocolos ni formatos de mensajes.

## 5. Supuestos que condicionan la arquitectura
| ID | Supuesto | Impacto si cambia |
|---|---|---|
| S01 | No se conoce una carga real ni un SLA de operación | No se puede justificar escala o distribución por números |
| S02 | Los SKUs perecibles tienen vencimiento conocido | Es necesario diferenciar flujos de no perecibles |
| S03 | Reservas sin parcialidad en el MVP | Se complica FUL-01 si se permiten asignaciones parciales |
| S04 | Cantidades en una unidad base por SKU | Conversión de unidades afectaría catálogo y movimientos |
| S05 | No se definen múltiples bodegas ni múltiples empresas | Varias organizaciones exigirían otra dimensión de propiedad y acceso |
| S06 | El dashboard tolera cierto desfase | Requerimientos de tiempo real podrían alterar interacciones |
| S07 | La flota tiene una asignación simple, sin optimización de rutas | Ruteo y capacidades de carga son una evolución futura |
| S08 | Las decisiones de arquitectura son académicas/propuestas | Requieren revisión del equipo, no representan acuerdos reales |

## 6. Registro inicial de riesgos
Escala cualitativa **Probabilidad** (Baja/Media/Alta) y **Impacto** (Bajo/Medio/Alto). Son juicios iniciales **no medidos**.

| ID | Riesgo | Prob. | Impacto | Mitigación de diseño propuesta | Responsable de seguimiento (rol) |
|---|---|---|---|---|---|
| R01 | Dos pedidos reservan las mismas unidades | Alta | Alto | Inventario controla compromisos y consistencia; UML de concurrencia | Líder de arquitectura |
| R02 | Despacho descuenta dos veces o pierde vínculo con reserva | Media | Alto | Diferenciar intención, reserva y confirmación; diagramar transición | Diseño Fulfillment/Inventario |
| R03 | Lotes vencidos o bloqueados aparecen elegibles | Media | Alto | Invariantes FEFO y política de cuarentena explícitas | Encargado de almacén / PO |
| R04 | Duplicación de propiedad del stock entre módulos | Alta | Alto | Un único propietario; matriz de datos en #6 | Líder de arquitectura |
| R05 | Reposición confunde alerta con compra o ingreso físico | Media | Medio | Estados distintos; recepción únicamente en Inventario | PO / Diseño Reposición |
| R06 | Dashboard muestra datos antiguos como actuales | Media | Medio | Etiquetar frescura; no usar dashboard para decidir compromiso | Diseño Dashboard |
| R07 | Exceso de microservicios sin necesidad real | Alta | Alto | Comparar alternativas y registrar ADR | Líder de arquitectura |
| R08 | Vehículo se asigna a dos despachos a la vez | Media | Medio | Flota controla exclusividad conceptual y estados | Diseño Flota |
| R09 | Faltan responsables, feedback y validación real | Alta | Alto | Revisión cruzada y acuerdos documentados antes de cerrar issues | Facilitador / equipo |
| R10 | Requisitos ambiguos sobre unidades y productos no perecibles | Media | Medio | Aclarar supuestos S02/S04 y documentar casos límite | PO / Encargado de almacén |

## 7. Decisiones resueltas en Sprint 2 (ADR)
| ID | Pregunta de diseño | Alternativas a considerar | Issue futuro |
|---|---|---|---|
| D01 | ¿Cómo agrupar límites lógicos en contenedores? | Monolito modular / agrupaciones / servicios | [#5](https://github.com/asmunozv/Deber2/issues/5), [#9](https://github.com/asmunozv/Deber2/issues/9) |
| D02 | ¿Quién posee cada clase de dato compartido? | Inventario dueño del compromiso; pedido en Fulfillment | [#6](https://github.com/asmunozv/Deber2/issues/6) |
| D03 | ¿Cómo razonar sobre concurrencia en FEFO? | Reserva consistente en núcleo único / coordinación distribuida | [#8](https://github.com/asmunozv/Deber2/issues/8), [#9](https://github.com/asmunozv/Deber2/issues/9) |
| D04 | ¿Qué reglas se aplican a productos sin vencimiento? | Segmentación de políticas / orden alterno | [#6](https://github.com/asmunozv/Deber2/issues/6), [#8](https://github.com/asmunozv/Deber2/issues/8) |
| D05 | ¿Qué hace el sistema si la recepción se cancela o corrige? | Ajuste trazable / política de reverso | [#7](https://github.com/asmunozv/Deber2/issues/7) |
| D06 | ¿Qué frescura se exige al dashboard? | Consulta operativa / proyección eventual | [#10](https://github.com/asmunozv/Deber2/issues/10), [#13](https://github.com/asmunozv/Deber2/issues/13) |

## 8. Criterios para validar en la revisión
- [x] Capacidades, responsabilidades y propietario candidato de cada dato definido.
- [x] Riesgos, supuestos e interrogantes documentados.
- [x] Alternativas comparadas sin imponer microservicios.
- [x] Validación de límites con otros integrantes.
- [x] Revisión por otra persona registrada y enlace desde el issue.
- [x] Decisiones de Sprint 2 ratificadas en ADR.

**Trazabilidad:** [Visión](01-VISION-Y-MVP.md) · [Historias](02-EPICAS-E-HISTORIAS.md) · [Backlog](03-BACKLOG-Y-ROLES.md) · [Registro de revisión](05-REVISION-Y-RETROSPECTIVA.md).
