# Sprint 4 — Propuesta visual del dashboard

> **Auditoría documental (24/11/2026):** prototipo HTML estático disponible y actualizado. La revisión visual por el equipo y el ensayo de presentación deben registrarse por separado.

**Issue:** [#15](https://github.com/asmunozv/Deber2/issues/15) · **Versión:** 1.1 · **Estado:** prototipo disponible; revisión del equipo registrada en la issue, fecha exacta visible en GitHub.

## 1. Objetivo de la vista

Ofrecer una vista de consulta que reúna indicadores de inventario, alertas, pedidos y recursos logísticos, sin convertir al dashboard en fuente de verdad ni permitir que modifique directamente las existencias.

## 2. Estructura del prototipo

Archivo: [dashboard/index.html](../dashboard/index.html). Es HTML estático y navegable, con **datos ilustrativos**; no está conectado a servicios reales ni a una base de datos.

La navegación lateral incluye cinco secciones:

- **Resumen:** indicadores generales, movimiento de inventario, distribución del stock, productos que requieren atención, alertas y actividad operativa.
- **Inventario y lotes:** búsqueda por SKU/producto/lote/zona, filtros por estado, consulta de cantidades y vencimientos, sugerencia de reposición y explicación de FEFO.
- **Pedidos:** estados y avance de preparación/despacho, con secuencia del proceso.
- **Flota y muelles:** muestra en una misma sección la **planta interna** (recepción, racks, picking y AMR) y la **planta externa** (patio, camiones, acceso y muelles).
- **Alertas:** lista filtrable por texto y severidad.

## 3. Indicadores y reglas de consulta

- Indicadores de unidades registradas, disponibilidad estimada, pedidos activos y alertas.
- Distribución ilustrativa de stock normal, bajo mínimo y crítico/próximo a vencer.
- Los filtros de inventario y alertas actúan sobre los registros de muestra cargados en el HTML.
- La exportación CSV descarga los registros visibles de la tabla de inventario.
- La etiqueta **“Datos ilustrativos”** advierte que los valores no son telemetría ni datos operativos reales.

## 4. Planta interna y externa

### 4.1 Planta interna

- Zona de recepción con lotes recibidos.
- Racks de almacenamiento y lotes con fecha de vencimiento.
- Zona de picking y recurso AMR asignado.
- Indicadores de condición normal, bajo mínimo y próximo a vencer.

### 4.2 Planta externa

- Camiones asociados a pedidos.
- Muelles libres, ocupados o en espera.
- Patio, acceso y zona de espera.

Ambas representaciones están disponibles dentro de la sección **Flota y muelles**; no se alternan mediante botones independientes.

## 5. Reglas de lectura (no de escritura)

- El dashboard es una vista de consulta; no es dueño del stock ni registra movimientos.
- Las acciones de negocio pertenecen a la capacidad responsable.
- La proyección de lectura puede presentar desfase frente al dato transaccional; la frescura debe mostrarse cuando exista conexión real. El prototipo actual no simula una marca dinámica de última actualización.

## 6. Criterios de aceptación de #15

- [x] Prototipo HTML navegable con resumen, inventario, pedidos, flota/muelles y alertas.
- [x] Representación de planta interna y externa, indicadores, alertas y flujo de pedidos.
- [x] Datos identificados explícitamente como ilustrativos; búsqueda, filtros y exportación CSV de muestra.
- [x] Comentario de revisión de otro integrante registrado en la issue #15.

**Relaciones:** [Versionamiento](16-VERSIONAMIENTO.md) · [Presentación](18-PRESENTACION.md) · [Requisitos de calidad](../sprint-3/13-REQUISITOS-CALIDAD.md).
