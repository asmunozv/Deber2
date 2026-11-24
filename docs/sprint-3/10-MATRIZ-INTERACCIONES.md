# Sprint 3 — Matriz de interacciones arquitectónicas

> **Auditoría documental (23/11/2026):** el contenido técnico está redactado. Las revisiones, aprobaciones, etiquetas/releases y actos de cierre solo deben declararse realizados si existen evidencias correspondientes en GitHub o actas confirmadas por el equipo.


**Issue:** [#10](https://github.com/asmunozv/Deber2/issues/10) · **Versión:** 1.0 · **Estado:** artefacto redactado; revisión y aceptación pendientes de verificar

## 1. Convención

Cada interacción identifica **origen**, **destino**, **propósito**, **necesidad de respuesta** (inmediata / eventual) y **efecto en el flujo de negocio**. No se especifican endpoints, métodos HTTP, payloads ni contratos técnicos (fuera del alcance de esta materia).

| Respuesta | Significado |
|---|---|
| **Inmediata (síncrona)** | El origen necesita el resultado para continuar la operación en curso |
| **Eventual (asíncrona)** | El destino reacciona sin bloquear la operación del origen |

## 2. Matriz por flujo

### F1 — Recepción → stock

| # | Origen | Destino | Propósito | Respuesta | Efecto en el flujo |
|---|---|---|---|---|---|
| 1 | Capa de aplicación | Inventario | Registrar recepción | Inmediata | Inicia la contabilización |
| 2 | Inventario | Catálogo | Validar SKU y política de lote | Inmediata | Bloquea recepción de SKU inválido |
| 3 | Inventario | Broker | Publicar "stock actualizado" | Eventual | Refresca proyección y Lakehouse |
| 4 | Broker | Proyección de lectura | Refrescar indicadores | Eventual | Dashboard ve stock al día |
| 5 | Broker | Lakehouse | Conservar histórico | Eventual | Analítica dispone de movimientos |

### F3 — Alerta → reposición

| # | Origen | Destino | Propósito | Respuesta | Efecto en el flujo |
|---|---|---|---|---|---|
| 6 | Inventario | Broker | Publicar cambio de disponibilidad | Eventual | Dispara evaluación de umbral |
| 7 | Broker | Reposición | Notificar disponibilidad | Eventual | Reposición calcula sugerencia |
| 8 | Capa de aplicación | Reposición | Listar/crear sugerencia u orden | Inmediata | Planificador decide |
| 9 | Reposición | Inventario | Leer disponibilidad vigente | Inmediata | Sugerencia usa dato actual |
| 10 | Reposición | Broker | Publicar "orden de compra creada" | Eventual | Otros componentes ven el cambio |

### F4 — Reserva FEFO

| # | Origen | Destino | Propósito | Respuesta | Efecto en el flujo |
|---|---|---|---|---|---|
| 11 | Capa de aplicación | Fulfillment | Crear pedido | Inmediata | Nace el pedido |
| 12 | Fulfillment | Inventario | Solicitar reserva FEFO | Inmediata | Compromete lotes o rechaza |
| 13 | Fulfillment | Broker | Publicar "reserva confirmada" | Eventual | Proyección y otros consumidores |
| 14 | Broker | Proyección de lectura | Refrescar disponibilidad proyectada | Eventual | Dashboard refleja el compromiso |

### F5 — Despacho → flota

| # | Origen | Destino | Propósito | Respuesta | Efecto en el flujo |
|---|---|---|---|---|---|
| 15 | Capa de aplicación | Fulfillment | Preparar / confirmar despacho | Inmediata | Avanza el estado del pedido |
| 16 | Fulfillment | Inventario | Confirmar salida de unidades reservadas | Inmediata | Descuenta físico y libera compromiso |
| 17 | Fulfillment | Flota | Solicitar asignación de recurso | Inmediata | Vincula vehículo/AMR al despacho |
| 18 | Fulfillment | Broker | Publicar "despacho actualizado" | Eventual | Refresca flujo de pedidos |
| 19 | Flota | Broker | Publicar "progreso logístico" | Eventual | Dashboard ve estado en ruta/entregado |

### F6/F7 — Dashboard y analítica (solo lectura)

| # | Origen | Destino | Propósito | Respuesta | Efecto en el flujo |
|---|---|---|---|---|---|
| 20 | Dashboard | Proyección de lectura | Consultar indicadores | Inmediata | Vista operativa |
| 21 | Dashboard | Capa de aplicación | Aprobar sugerencia / reservar | Inmediata | Acción dirigida a la capacidad dueña |
| 22 | Analítica | Lakehouse | Consultar histórico | Inmediata | Análisis de tendencias |

## 3. Observaciones de consistencia

- Las interacciones **2, 12 y 16** son las que exigen **consistencia fuerte** (validación de SKU, reserva y salida).
- Las interacciones **3–5, 6–7, 10, 13–14, 18–19** son **eventuales**: el dashboard debe **etiquetar la frescura** del dato (riesgo R06).
- **El dashboard nunca escribe** en Inventario: sus acciones pasan por la capa de aplicación hacia la capacidad responsable.

## 4. Criterios de aceptación de #10

- [x] Matriz con origen, destino, propósito, tipo de respuesta y efecto.
- [x] Vinculada a los flujos F1–F7.
- [x] Distinción entre consistencia fuerte y eventual.
- [ ] Revisión por otro integrante.

**Relaciones:** [C4](../sprint-2/05-C4-ARQUITECTURA.md) · [Flujos](../sprint-2/07-FLUJOS-RECEPCION-REPOSICION.md) · [Reserva/despacho](../sprint-2/08-FLUJOS-RESERVA-DESPACHO.md) · [Requisitos de calidad](13-REQUISITOS-CALIDAD.md).
