# Sprint 4 — Propuesta visual del dashboard

**Issue:** [#15](https://github.com/asmunozv/Deber2/issues/15) · **Versión:** 1.0 · **Estado:** propuesta para revisión · **Responsable principal (rol):** Product Owner (Ariana Muñoz)

## 1. Objetivo de la vista

Separar la **supervisión de existencias** (indicadores) de la **visualización física de la bodega** (planta). Ambas vistas comparten **alertas, indicadores y flujo de pedidos**.

| Vista | Qué muestra | Fuente conceptual |
|---|---|---|
| **Planta interna** | Racks, pallets, lotes, zonas de recepción y picking, y AMR dentro de la bodega | Proyección de lectura (Inventario/Flota) |
| **Planta externa** | Camiones en el patio, muelles, acceso y zona de espera | Proyección de lectura (Flota) |
| **Indicadores compartidos** | Stock total, alertas activas, pedidos en preparación y en ruta | Proyección de lectura |

## 2. Prototipo navegable

Archivo: [`dashboard/index.html`](../dashboard/index.html) (ábralo en el navegador). Es **HTML estático con datos ilustrativos**; **no** representa una conexión funcional con servicios reales.

- Botones **Planta interna / Planta externa** para alternar vistas.
- Tarjetas KPI, panel de **alertas** y **flujo de pedidos** compartidos.
- Etiqueta de **frescura** ("última lectura: hace … s") que materializa la consistencia eventual.

## 3. Explicación de las vistas

### 3.1 Planta interna
- **Zonas:** recepción, zona A (racks), zona B (picking).
- **Lotes** con estado visual: normal (azul), bajo mínimo (naranja), próximo a vencer/bloqueado (rojo).
- **AMR** de picking posicionados en la zona correspondiente.

### 3.2 Planta externa
- **Muelles** con estado libre/ocupado/en espera.
- **Patio, acceso y zona de espera** con camiones.

## 4. Reglas de lectura (no de escritura)

- El dashboard **no** es la fuente de verdad del stock; **no** permite editar directamente existencias.
- Las **acciones** (aprobar una sugerencia, reservar stock) se dirigen a la **capacidad responsable** a través de la capa de aplicación.
- Los datos se muestran como **proyección de lectura** con su posible desfase indicado.

## 5. Criterios de aceptación de #15

- [x] Prototipo HTML navegable con vistas interna y externa.
- [x] Indicadores, alertas y flujo compartidos.
- [x] Explicación de cada vista y de la regla de solo lectura.
- [ ] Revisión por otro integrante.

**Relaciones:** [Versionamiento](16-VERSIONAMIENTO.md) · [Presentación](18-PRESENTACION.md) · [Requisitos de calidad](../sprint-3/13-REQUISITOS-CALIDAD.md).
