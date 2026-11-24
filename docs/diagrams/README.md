# Diagramas fuente (Mermaid)

Diagramas de arquitectura y procesos en formato **Mermaid (`.mmd`)**. Son texto versionable que GitHub renderiza directamente. Las **exportaciones (PNG/SVG)** usadas en el informe deben generarse aparte (ver [16-VERSIONAMIENTO.md](../sprint-4/16-VERSIONAMIENTO.md)).

## C4

| Nivel | Archivo | Descripción |
|---|---|---|
| 1 — Contexto | [`c4-contexto.mmd`](c4-contexto.mmd) | Sistema y actores/externos |
| 2 — Contenedores | [`c4-contenedores.mmd`](c4-contenedores.mmd) | Capacidades + broker + proyección + Lakehouse |
| 3 — Componente (Inventario) | [`c4-componente-inventario.mmd`](c4-componente-inventario.mmd) | Puertos, dominio, repositorios, Outbox |
| 3 — Componente (Fulfillment) | [`c4-componente-fulfillment.mmd`](c4-componente-fulfillment.mmd) | Pedidos, preparación, despacho |

## UML

| Tipo | Archivo | Descripción |
|---|---|---|
| Secuencia | [`uml-secuencia-recepcion.mmd`](uml-secuencia-recepcion.mmd) | Flujo A (F1) recepción → stock |
| Secuencia | [`uml-secuencia-reposicion.mmd`](uml-secuencia-reposicion.mmd) | Flujo B (F3) alerta → reposición |
| Secuencia | [`uml-secuencia-reserva-fefo.mmd`](uml-secuencia-reserva-fefo.mmd) | Flujo C (F4) reserva FEFO |
| Secuencia | [`uml-secuencia-despacho.mmd`](uml-secuencia-despacho.mmd) | Flujo C (F5) despacho → flota |
| Estado | [`uml-estados-pedido.mmd`](uml-estados-pedido.mmd) | Máquina de estados del pedido |
| Estado | [`uml-estados-reserva.mmd`](uml-estados-reserva.mmd) | Máquina de estados de la reserva |
| Estado | [`uml-estados-orden-compra.mmd`](uml-estados-orden-compra.mmd) | Máquina de estados de la orden de compra |
| Actividad | [`uml-actividad-flujo-vertical.mmd`](uml-actividad-flujo-vertical.mmd) | Recorrido integral recepción → stock → alerta → reposición |

## Exportador visual de los 12 diagramas

Se agregó [exportar.html](exportar.html), un visor de los archivos fuente Mermaid de este repositorio. Para utilizarlo, descarga el HTML, ábrelo en un navegador con conexión a Internet (Mermaid se carga desde un CDN), selecciona el diagrama y pulsa **Exportar SVG** o **Exportar PNG**. Guarda las imágenes que utilices en el informe en una carpeta `docs/diagrams/exports/` del repositorio. El exportador **no** sube automáticamente los archivos exportados a GitHub.

## Cómo exportar a imagen

- **Mermaid CLI:** `npx -y @mermaid-js/mermaid-cli -i c4-contenedores.mmd -o c4-contenedores.png`
- **Mermaid Live Editor:** pegar el contenido y exportar PNG/SVG en <https://mermaid.live>.
