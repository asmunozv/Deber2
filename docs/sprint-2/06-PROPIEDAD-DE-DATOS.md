# Sprint 2 — Propiedad de datos

> **Estado verificado (auditoría 23/11/2026):** archivo de diseño disponible. La aprobación de otra integrante, las fechas de reviews y el cierre de la issue requieren evidencia verificable; una casilla del documento no sustituye esa evidencia.


**Issue:** [#6](https://github.com/asmunozv/Deber2/issues/6) · **Versión:** 1.0 · **Estado:** artefacto redactado; validación documental pendiente

## 1. Regla de propiedad

Cada dato de negocio tiene **una y solo una capacidad propietaria** (fuente autorizada). Las demás capacidades **no modifican** ese dato: solo lo consultan o solicitan un cambio mediante una interacción conceptual. Esta regla responde al riesgo **R04** (duplicación de propiedad del stock) y a la decisión **D02** de Sprint 1.

## 2. Matriz de propiedad de datos

| Dato / clase | Fuente autorizada (propietaria) | Quién lo consulta | Quién solicita cambios | Se modifica directamente desde otro servicio |
|---|---|---|---|---|
| SKU, producto, categoría | **Catálogo** | Inventario, Reposición, Fulfillment, Dashboard | — | No |
| Bodega, zona, ubicación (maestra) | **Catálogo** | Inventario, Flota, Dashboard | — | No |
| Política de lote / caducidad del SKU | **Catálogo** | Inventario, Fulfillment | — | No |
| Lote (instancia almacenada) | **Inventario** | Fulfillment, Reposición, Analítica, Dashboard | Catálogo (validación) | No |
| Saldo físico por lote/ubicación | **Inventario** | Todos (solo lectura) | — | No |
| Movimiento (recepción, salida, transferencia, ajuste) | **Inventario** | Analítica, Dashboard | Fulfillment (salida por despacho) | No |
| Compromiso de unidades en lotes (reserva física) | **Inventario** | Fulfillment, Dashboard | Fulfillment (reservar/liberar) | No |
| Pedido y líneas | **Fulfillment** | Dashboard, Analítica, Flota | — | No |
| Estado del pedido (preparación/despacho) | **Fulfillment** | Flota, Dashboard | — | No |
| Umbral y alerta de reposición | **Reposición** | Dashboard | — | No |
| Sugerencia y estado de aprobación | **Reposición** | Dashboard | Planificador (aprobar/descartar) | No |
| Proveedor y orden de compra | **Reposición** | Analítica, Dashboard | — | No |
| Vehículo, AMR, muelle | **Flota** | Dashboard, Fulfillment | — | No |
| Ruta y telemetría | **Flota** | Dashboard, Analítica | — | No |
| Asignación de recurso a despacho | **Flota** | Fulfillment, Dashboard | Fulfillment (solicitar asignación) | No |
| Indicadores y vistas del dashboard | **Proyección de lectura** (derivada) | Dashboard | — | No (derivada) |
| Series y modelos históricos | **Lakehouse / Analítica** | Analítica | — | No (derivada) |

## 3. Aclaraciones de propiedad (refinamientos)

### 3.1 Ubicación maestra vs. saldo en ubicación
- **Catálogo** define la **ubicación maestra** (bodegas, zonas, ubicaciones): identidad y estructura del espacio físico.
- **Inventario** registra el **saldo en esa ubicación** (cuántas unidades de qué lote hay allí).

Esto resuelve una posible ambigüedad: *"ubicación"* aparece en dos módulos, pero con significado distinto (maestra vs. stock).

### 3.2 Pedido vs. reserva física
- **Fulfillment** es dueño del **pedido** y de su estado.
- **Inventario** es dueño del **compromiso físico** de unidades en lotes específicos. La reserva de Inventario conserva una **referencia al pedido** para trazabilidad, pero no se apropia del ciclo de vida del pedido.

### 3.3 Dashboard y Analítica no son fuentes de verdad
- El **Dashboard** es una interfaz y una vista de consulta; **no** es la fuente de verdad del stock.
- La **Analítica** interpreta datos históricos; **no** registra transacciones.
- Las actualizaciones en vivo usan la **proyección de lectura**, alimentada por cambios de negocio vía broker.

## 4. Consecuencias de diseño

1. **Recepción** solo se registra en Inventario (ni Reposición ni Fulfillment crean stock).
2. **Reserva y salida** pasan por Inventario como interacción síncrona (consistencia fuerte).
3. **Reposición** reacciona a cambios de disponibilidad (evento) sin escribir existencias.
4. **Telemetría** vive en Flota; el dashboard la consume desde la proyección.
5. **Orden de compra** no modifica saldo: el ingreso físico ocurre solo en una recepción.

## 5. Criterios de aceptación de #6

- [x] Matriz con fuente autorizada por clase de dato.
- [x] Refinamientos de propiedad documentados (ubicación, pedido/reserva, lecturas).
- [x] Vínculo con riesgos (R04) y decisiones (D02).
- [x] Revisión cruzada registrada: comentario de Ariana en la issue #6 (fecha visible en GitHub).
- [ ] Ratificación en ADR y enlace desde el issue.

**Relaciones:** [C4](05-C4-ARQUITECTURA.md) · [Flujos recepción/reposición](07-FLUJOS-RECEPCION-REPOSICION.md) · [Flujos reserva/despacho](08-FLUJOS-RESERVA-DESPACHO.md) · [ADR](09-ADR.md).
