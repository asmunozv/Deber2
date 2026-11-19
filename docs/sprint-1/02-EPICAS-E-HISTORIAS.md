# Sprint 1 — Épicas e historias de usuario

**Issue:** [#2](https://github.com/asmunozv/Deber2/issues/2) · **Versión:** 1.0 · **Estado:** propuesta lista para revisión · **Aprobación de negocio:** pendiente

## Convenciones
- Cada historia utiliza **Como / quiero / para** y criterios de aceptación observables en situaciones de negocio: **Dado / cuando / entonces**.
- **MVP**: cubierto por los flujos fundamentales del diseño; **Evolución**: queda identificado sin imponer implementación.
- Los identificadores **CAT, INV, REP, FUL, FLT, DAS, ANA** se mantienen estables en backlog, UML, C4 y ADR.
- Los criterios son requisitos esperados, **no resultados de pruebas ejecutadas**.
- **Flujos:** F1 recepción, F2 control de stock, F3 alerta/reposición, F4 reserva FEFO, F5 despacho/flota, F6 consulta operativa, F7 analítica.

## E1. Catálogo (responsabilidad: información maestra del producto)
### CAT-01 — Registrar y consultar un SKU · MVP · F1/F2/F4
**Como** administrador de catálogo, **quiero** definir un SKU con nombre, unidad base y condición de perecibilidad, **para** que las operaciones de almacén hagan referencia a productos identificables.
1. **Dado** un SKU nuevo con atributos obligatorios, **cuando** se registra, **entonces** se incorpora una única ficha consultable.
2. **Dado** un identificador ya existente, **cuando** se intenta registrarlo de nuevo, **entonces** se rechaza la duplicación.
3. **Dado** un SKU inactivo, **cuando** se intenta recibir un lote nuevo, **entonces** se impide esa recepción según política propuesta.

### CAT-02 — Validar atributos de un lote · MVP · F1/F4
**Como** operador de recepción, **quiero** conocer los datos exigidos para cada tipo de SKU, **para** recibir lotes consistentes.
1. **Dado** un SKU perecible, **cuando** se propone ingresar su lote, **entonces** se exige identificación y fecha de caducidad.
2. **Dado** un vencimiento anterior al día de recepción, **cuando** se intenta ingresar el lote como disponible, **entonces** se rechaza o se clasifica para cuarentena (política a ratificar).
3. **Dado** un SKU no perecible, **cuando** se valida su lote, **entonces** no se exige vencimiento si la política acordada lo permite.

## E2. Inventario por lote y ubicación (responsabilidad: stock)
### INV-01 — Registrar recepción de existencias · MVP · F1
**Como** operador de recepción, **quiero** registrar cantidad por SKU, lote y ubicación, **para** actualizar stock físico con trazabilidad.
1. **Dado** un SKU y ubicación válidos, **cuando** se registra un ingreso positivo de un lote válido, **entonces** se incrementa únicamente el stock de esa combinación.
2. **Dado** un lote con datos insuficientes, **cuando** se propone la recepción, **entonces** no se contabiliza como disponible.
3. **Dado** una recepción registrada, **cuando** se consulta su historial conceptual, **entonces** se distinguen origen, cantidad y ubicación.

### INV-02 — Consultar y ajustar disponibilidad · MVP · F2/F3/F4
**Como** encargado de almacén, **quiero** ver stock físico, reservado y disponible por SKU/lote/ubicación, **para** evitar comprometer unidades inexistentes.
1. **Dado** un lote con 20 unidades físicas y 7 reservadas, **cuando** se consulta su disponibilidad, **entonces** se presentan 13 unidades disponibles.
2. **Dado** un movimiento de salida o un ajuste autorizado, **cuando** se registra, **entonces** queda trazado sin generar valores negativos.
3. **Dado** un lote bloqueado o vencido, **cuando** se calcula disponibilidad elegible, **entonces** no se oferta a reservas.

## E3. Reposición (responsabilidad: señales y propuestas de abastecimiento)
### REP-01 — Detectar necesidad de reponer · MVP · F3
**Como** planificador de compras, **quiero** recibir una señal si el stock disponible de un SKU llega a su umbral, **para** revisar oportunamente el abastecimiento.
1. **Dado** un SKU con umbral 10, **cuando** su disponibilidad cae a 8, **entonces** aparece como candidato de reposición.
2. **Dado** una alerta, **cuando** se consulta, **entonces** contiene SKU, disponibilidad utilizada y umbral configurado.
3. **Dado** un SKU sin umbral aprobado, **cuando** se analiza, **entonces** se señala configuración pendiente en vez de inventar un valor.

### REP-02 — Revisar propuesta de reposición · Evolución · F3
**Como** planificador, **quiero** revisar y aprobar o descartar una propuesta, **para** separar la detección de una decisión de compra.
1. **Dada** una propuesta existente, **cuando** se revisa, **entonces** queda un estado de aprobación o descarte.
2. **Dada** una propuesta aprobada, **cuando** se confirma, **entonces** no se registra stock físico hasta que ocurra una recepción.
3. **Dada** una propuesta duplicada, **cuando** se visualiza, **entonces** se identifica su relación con otras necesidades abiertas del mismo SKU.

## E4. Fulfillment / pedidos (responsabilidad: compromiso y despacho del pedido)
### FUL-01 — Reservar unidades según FEFO · MVP · F4
**Como** coordinador de pedidos, **quiero** reservar unidades de lotes elegibles priorizando vencimientos próximos, **para** reducir caducidades sin sobreasignar stock.
1. **Dados** dos lotes elegibles que vencen el 10 y el 20 de diciembre, **cuando** se solicitan unidades, **entonces** se asigna primero el lote del día 10.
2. **Dada** una solicitud superior a la disponibilidad total elegible, **cuando** se intenta reservar, **entonces** no se confirma una reserva parcial en el MVP.
3. **Dadas** dos solicitudes concurrentes sobre un mismo lote, **cuando** se evalúa la disponibilidad, **entonces** el modelo exige una sola decisión consistente sin exceder el físico.
4. **Dado** un pedido cancelado antes del despacho, **cuando** se libera la reserva, **entonces** esas unidades vuelven a quedar disponibles si siguen siendo elegibles.

### FUL-02 — Confirmar despacho asociado a reserva · MVP · F5
**Como** operador de despacho, **quiero** confirmar la salida de unidades previamente reservadas, **para** mantener consistente el pedido con la existencia física.
1. **Dada** una reserva vigente, **cuando** se confirma despacho, **entonces** las unidades reservadas salen de stock físico y se deja de contabilizar su compromiso.
2. **Dado** un pedido sin reserva suficiente, **cuando** se intenta despachar, **entonces** la operación no se considera confirmada.
3. **Dado** un despacho ya confirmado, **cuando** se intenta confirmarlo otra vez, **entonces** no ocurre un segundo descuento.

## E5. Flota (responsabilidad: disponibilidad y asignación logística)
### FLT-01 — Asignar vehículo disponible · MVP · F5
**Como** coordinador de flota, **quiero** relacionar un despacho con un vehículo disponible, **para** identificar el recurso logístico asignado.
1. **Dado** un vehículo disponible, **cuando** se asigna a un despacho, **entonces** su asignación queda visible.
2. **Dado** un vehículo ya ocupado o inactivo, **cuando** se intenta asignarlo a otro despacho simultáneo, **entonces** se señala conflicto.
3. **Dado** un despacho sin vehículo, **cuando** se revisa, **entonces** aparece como pendiente de asignación.

### FLT-02 — Consultar estado de entrega · Evolución · F5
**Como** coordinador de flota, **quiero** registrar los estados preparado, en ruta y entregado, **para** conocer el avance logístico.
1. **Dado** un despacho asignado, **cuando** se registra un estado nuevo, **entonces** se conserva la secuencia de estados.
2. **Dado** un despacho entregado, **cuando** se consulta, **entonces** se conoce su estado final sin alterar stock ya descontado.

## E6. Dashboard (responsabilidad: lectura operativa agregada)
### DAS-01 — Consultar tablero de operación · MVP · F6
**Como** supervisor, **quiero** visualizar stock, alertas y despachos pendientes, **para** identificar prioridades diarias.
1. **Dadas** existencias, alertas y despachos registrados, **cuando** se consulta el tablero, **entonces** se muestran indicadores diferenciados por origen de negocio.
2. **Dada** una lectura desactualizada, **cuando** se consulta, **entonces** se indica que es información de referencia y puede tener desfase.
3. **Dado** un indicador del tablero, **cuando** se observa, **entonces** no permite editar directamente la fuente de verdad de inventario.

### DAS-02 — Explorar lotes detrás de un indicador · Evolución · F6
**Como** responsable de almacén, **quiero** consultar el detalle de lotes por SKU desde el tablero, **para** entender alertas de caducidad o falta de stock.
1. **Dado** un SKU con alerta, **cuando** se accede a su detalle, **entonces** se diferencian lotes, ubicaciones y disponibilidad.
2. **Dado** un lote bloqueado, **cuando** se consulta el detalle, **entonces** se identifica como no elegible para reserva.

## E7. Analítica (responsabilidad: interpretación histórica, no transacciones)
### ANA-01 — Analizar tendencias de movimientos · Evolución · F7
**Como** analista de operaciones, **quiero** comparar ingresos y salidas por período, **para** estudiar patrones de rotación.
1. **Dado** un período seleccionado, **cuando** se consulta, **entonces** se distinguen ingresos y salidas sin confundir reservas con ventas.
2. **Dado** un período sin datos, **cuando** se consulta, **entonces** se indica ausencia de información, no valores inferidos.

### ANA-02 — Interpretar indicadores de caducidad y reposición · Evolución · F7
**Como** gerente, **quiero** examinar lotes próximos a caducar y frecuencia de alertas, **para** priorizar mejoras operativas.
1. **Dadas** fechas de vencimiento existentes, **cuando** se define una ventana de análisis, **entonces** se identifican lotes dentro de ella.
2. **Dadas** alertas de reposición, **cuando** se consulta su histórico, **entonces** se diferencian alertas de propuestas o compras efectivas.

## Mapa de trazabilidad por flujo
| Flujo | Historias de entrada | Verificación conceptual esperada |
|---|---|---|
| F1 Recepción | CAT-01, CAT-02, INV-01 | SKU válido → lote válido → existencias por ubicación |
| F2 Disponibilidad | INV-02 | físico − reservado = disponible; elegibilidad controlada |
| F3 Alerta y reposición | INV-02, REP-01, REP-02 | el umbral produce señal; compra no crea stock |
| F4 Reserva FEFO | CAT-02, INV-02, FUL-01 | asignación de lotes en orden de vencimiento |
| F5 Despacho y flota | FUL-02, FLT-01, FLT-02 | compromiso → salida física → asignación logística |
| F6 Dashboard | DAS-01, DAS-02 | lectura sin escritura sobre fuentes propietarias |
| F7 Analítica | ANA-01, ANA-02 | análisis derivado de datos históricos, no operacional |

**Escenario vertical para posteriores diagramas:** registrar SKU perecible → recibir dos lotes en ubicaciones distintas → consultar stock → detectar umbral → reservar cantidad con FEFO → confirmar despacho → consultar tablero. El plan de Sprint 2 documentará los escenarios sin construirlos.

**Relaciones:** [Visión/MVP](01-VISION-Y-MVP.md) · [Backlog](03-BACKLOG-Y-ROLES.md) · [Límites/Riesgos](04-LIMITES-Y-RIESGOS.md).

**Control de revisión:** historias y criterios redactados; **pendiente** revisión documentada por otro integrante y aceptación del equipo.
