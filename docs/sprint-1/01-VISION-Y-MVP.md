# Sprint 1 — Visión de producto, interesados y MVP

**Proyecto:** Smart Inventory · **Asignatura:** Diseño de Sistemas (USFQ) · **Issue:** [#1](https://github.com/asmunozv/Deber2/issues/1)  
**Versión:** 1.0 (propuesta de diseño) · **Estado:** redactado; pendiente de validación del equipo · **Fecha de aprobación:** pendiente

## 1. Problema y oportunidad
Una operación que recibe productos por lote y los almacena en múltiples ubicaciones necesita saber qué existencias están disponibles, dónde se encuentran y cuándo vencen. Cuando catálogo, inventario, reposición y despacho se administran de manera aislada, aparecen duplicidad de registros, quiebres de stock, pérdidas por caducidad, reservas superiores a lo disponible y poca trazabilidad del despacho.

**Smart Inventory** propone un diseño de sistema con responsabilidades y propiedad de datos claras que permita seguir el flujo completo desde la recepción hasta el despacho. La prioridad del ejercicio es la coherencia arquitectónica, **no** la cantidad de microservicios ni la construcción de software funcional.

## 2. Visión
> Para equipos que administran productos, lotes, ubicaciones y pedidos, Smart Inventory será una plataforma de gestión de inventario que consolide el estado de existencias, ayude a reponer oportunamente y permita reservar productos con criterio FEFO, haciendo trazable la preparación y el despacho. A diferencia de registros inconexos, su diseño define quién es dueño de cada dato y cómo se coordinan las capacidades de negocio.

### Objetivos de diseño y evidencias esperadas
| Objetivo | Cómo se verifica en la entrega de Diseño de Sistemas |
|---|---|
| Trazar un producto entre recepción, ubicación, reserva y despacho | Recorrido narrado y diagramas de flujo/UML en Sprint 2 |
| Evitar ambigüedad sobre quién actualiza el stock | Matriz explícita de propiedad de datos en Sprint 2 |
| Explicar qué significa disponibilidad frente a stock físico y reservado | Reglas de negocio y escenarios de las historias |
| Justificar decisiones sin fragmentar servicios arbitrariamente | Límites candidatos y ADR contrastados en Sprint 2 |
| Hacer visible la reposición y el estado operativo | Historias, tablero conceptual y criterios de calidad |
| Mantener vínculos entre necesidades y artefactos | Identificadores estables, backlog e issues de GitHub |

Estas son **metas de la documentación**, no métricas de rendimiento medidas en un sistema implementado.

## 3. Interesados
| Interesado | Necesidad / decisión principal | Participación requerida |
|---|---|---|
| Responsable de almacén | Visibilidad por SKU, lote y ubicación; control de movimientos | Validar reglas de recepción y stock |
| Operador de recepción | Registrar lote, vencimiento, cantidad y ubicación | Validar escenarios de ingreso y errores |
| Planificador de abastecimiento / compras | Conocer bajo stock y propuestas de reposición | Validar umbrales y responsabilidades de aprobación |
| Encargado de pedidos / fulfillment | Reservar existencias elegibles y preparar despacho | Validar reserva FEFO, cancelación y despacho |
| Coordinador de flota | Saber qué vehículo puede atender un despacho | Validar disponibilidad y seguimiento básico |
| Gerencia / supervisión | Leer indicadores sin alterar transacciones | Priorizar información de dashboard y analítica |
| Equipo académico de diseño | Evaluar límites, coherencia, decisiones y trazabilidad | Revisar documentación, diagramas y ADR |

**Supuesto:** los nombres de personas, organización real, tamaño de operación y volúmenes no se han definido. Los perfiles anteriores son roles de negocio propuestos, no participantes confirmados.

## 4. Actores y vocabulario de dominio
- **SKU:** identificador único de un producto en el catálogo.
- **Lote:** conjunto de unidades de un SKU con atributos comunes; para perecibles incluye fecha de vencimiento.
- **Ubicación:** punto de almacenamiento identificable.
- **Stock físico:** unidades registradas en ubicación, descontadas las salidas físicas.
- **Stock reservado:** unidades comprometidas para pedidos aún no despachados.
- **Disponible para reservar:** stock físico elegible menos stock reservado; nunca puede ser negativo.
- **FEFO (First Expire, First Out):** se priorizan los lotes con vencimiento más próximo que siguen siendo elegibles.
- **Punto de reposición:** umbral de unidades disponibles que activa una alerta o propuesta de abastecimiento.
- **Despacho:** confirmación de salida física vinculada a una reserva y a un pedido.

## 5. Alcance funcional del MVP conceptual
La palabra **MVP** significa aquí *mínimo conjunto de capacidades que el diseño debe cubrir de punta a punta*; **no** significa que se entregará una aplicación ejecutable.

| Capacidad | Incluida en el MVP conceptual | Resultado observable en el modelo |
|---|---|---|
| Catálogo | Alta/consulta de SKU y atributos básicos; validación de datos del lote | Los movimientos hacen referencia a productos válidos |
| Inventario | Recepción con lote y ubicación, consulta, movimiento y disponibilidad | Existencias coherentes y trazables |
| Reposición | Umbral configurable y detección de nivel bajo | Alerta y propuesta conceptual de reposición |
| Fulfillment | Reserva de pedido por FEFO y confirmación de despacho | No se reserva más de lo disponible ni lote vencido |
| Flota | Asignación básica de vehículo disponible al despacho | Despacho asociado a un recurso logístico |
| Dashboard | Vista consolidada de existencias, alertas y despachos | Información operativa visible sin ser fuente de verdad |

**Evolución posterior / fuera del MVP:** aprobación completa de compras, planificación sofisticada de rutas, optimización de flota, pronósticos y análisis históricos complejos, integraciones ERP, múltiple organización, notificaciones reales y aplicaciones móviles. Las capacidades de analítica avanzada se describen como historias futuras para mantener la visión integral.

**Fuera del alcance de esta asignatura:** implementación de APIs, especificación de contratos técnicos o mensajes, construcción de microservicios, desarrollo frontend/backend, persistencia física detallada, CI/CD, infraestructura, despliegue y ejecución de pruebas. Esos temas pueden pertenecer a Desarrollo de Software Moderno, pero **no forman parte de los entregables de Diseño de Sistemas**.

## 6. Flujos de negocio prioritarios
1. **Recepción → inventario:** el operador elige un SKU existente, registra lote, vencimiento, cantidad y ubicación; Inventario actualiza existencias.
2. **Stock → alerta → reposición:** Inventario calcula la disponibilidad; Reposición compara contra umbrales y comunica una necesidad de abastecimiento. Reposición no modifica el stock por sí sola.
3. **Pedido → reserva FEFO:** Fulfillment solicita cantidad de SKU; Inventario determina y compromete lotes elegibles en orden de vencimiento; Fulfillment conserva el estado del pedido.
4. **Reserva → despacho → flota:** se valida una reserva vigente, se registra la salida del stock y se asocia el despacho a un vehículo elegible.
5. **Consulta operativa:** Dashboard presenta datos derivados de las capacidades propietarias y puede mostrar desfase temporal; nunca corrige el inventario por cuenta propia.

## 7. Reglas de negocio iniciales (hipótesis a ratificar)
- RB-01: todo lote almacenado corresponde a un SKU existente.
- RB-02: cantidades de recepción y movimientos son positivas; los ajustes requieren motivo y trazabilidad.
- RB-03: solo lotes no vencidos y no bloqueados participan en reservas FEFO.
- RB-04: FEFO usa primero menor fecha de vencimiento; ante empate, fecha de recepción más antigua. La regla de desempate debe confirmarse.
- RB-05: si la cantidad total elegible no alcanza, el MVP **rechaza la reserva completa**, sin reserva parcial.
- RB-06: confirmar un despacho descuenta unidades físicas ya reservadas y libera el compromiso asociado, sin doble descuento.
- RB-07: una cancelación de pedido antes del despacho libera su reserva; las devoluciones están fuera del MVP.
- RB-08: solo Inventario mantiene la fuente de verdad de cantidades físicas y compromisos; otros módulos solicitan operaciones conceptuales.
- RB-09: el dashboard es una proyección informativa, no una autoridad para escribir movimientos.

## 8. Restricciones y decisiones aún abiertas
| Supuesto / pregunta | Tratamiento ahora | Validación pendiente |
|---|---|---|
| El sistema se utiliza en una operación de almacén sin sector especificado | Modelo de dominio genérico | Confirmar productos y regulación aplicable |
| La mayoría de lotes tiene vencimiento | FEFO se usa como flujo representativo | Definir SKU no perecibles |
| Una sola unidad de medida base por SKU | Simplifica cantidades | Definir conversiones, empaques y fracciones |
| Reservas sin parcialidad | Regla RB-05 | Confirmar política comercial |
| Un vehículo puede vincularse a un despacho | Cobertura mínima de flota | Confirmar capacidad y restricciones |
| No existe obligación demostrada de microservicios | Comparar monolito modular vs servicios en ADR futuro | Ratificar límites en Sprint 2 |
| No hay métricas reales, equipo designado ni clientes entrevistados | Evitar inventar evidencia | Validación del equipo y de actores |

## 9. Trazabilidad y aceptación
- Épicas e historias: [02-EPICAS-E-HISTORIAS.md](02-EPICAS-E-HISTORIAS.md)
- Backlog y dependencias: [03-BACKLOG-Y-ROLES.md](03-BACKLOG-Y-ROLES.md)
- Límites y riesgos: [04-LIMITES-Y-RIESGOS.md](04-LIMITES-Y-RIESGOS.md)
- Registro para revisión/retrospectiva: [05-REVISION-Y-RETROSPECTIVA.md](05-REVISION-Y-RETROSPECTIVA.md)
- Issue de seguimiento: [#1](https://github.com/asmunozv/Deber2/issues/1)

**Control de revisión:** elaboración documentada; **revisión por otro integrante: pendiente**. No equivale a aprobación del Product Owner.
