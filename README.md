# Smart Inventory — Diseño de Sistemas

Deber 2 de Diseño de Sistemas (USFQ). Diseño arquitectónico de una plataforma para catálogo, inventario por lote y ubicación, reposición, reservas FEFO, flota, dashboard y analítica, preparada para evolucionar hacia microservicios.

## Gestión del proyecto
- [Plan de cuatro sprints](docs/SPRINTS.md)
- [Backlog en GitHub Issues](https://github.com/asmunozv/Deber2/issues)

## Entregables de Sprint 1
El incremento documental está organizado en commits por responsable, en las ramas indicadas en [Plan de cuatro sprints](docs/SPRINTS.md). Sprint 1 está **terminado**: revisión cruzada y retrospectiva registradas el 21/11/2026.

1. [Visión, interesados y MVP](docs/sprint-1/01-VISION-Y-MVP.md) — [Issue #1](https://github.com/asmunozv/Deber2/issues/1).
2. [Siete épicas y catorce historias de usuario](docs/sprint-1/02-EPICAS-E-HISTORIAS.md) — [Issue #2](https://github.com/asmunozv/Deber2/issues/2).
3. [Backlog priorizado, dependencias y roles](docs/sprint-1/03-BACKLOG-Y-ROLES.md) — [Issue #3](https://github.com/asmunozv/Deber2/issues/3).
4. [Límites candidatos, propiedad de datos y riesgos](docs/sprint-1/04-LIMITES-Y-RIESGOS.md) — [Issue #4](https://github.com/asmunozv/Deber2/issues/4).
5. [Registro de revisión y retrospectiva](docs/sprint-1/05-REVISION-Y-RETROSPECTIVA.md) — revisión y retrospectiva registradas.

## Objetivo de diseño
Definir propietarios claros de responsabilidades y datos, y flujos coherentes de recepción, reposición, reserva y despacho. No se evalúa la cantidad de servicios.

## Alcance académico
Se documentarán límites, C4/UML, propiedad de datos, interacciones conceptuales, ADR, patrones, SOLID, requisitos de calidad y trazabilidad. **No** se incluyen diseño técnico de APIs y mensajes, CI/CD, despliegue ni pruebas de software.

## Entregables de Sprint 2 (arquitectura) — terminado
1. [Arquitectura C4 y límites de servicio](docs/sprint-2/05-C4-ARQUITECTURA.md) — [Issue #5](https://github.com/asmunozv/Deber2/issues/5).
2. [Propiedad de datos](docs/sprint-2/06-PROPIEDAD-DE-DATOS.md) — [Issue #6](https://github.com/asmunozv/Deber2/issues/6).
3. [Flujos de recepción y reposición (UML)](docs/sprint-2/07-FLUJOS-RECEPCION-REPOSICION.md) — [Issue #7](https://github.com/asmunozv/Deber2/issues/7).
4. [Flujos de reserva FEFO y despacho (UML)](docs/sprint-2/08-FLUJOS-RESERVA-DESPACHO.md) — [Issue #8](https://github.com/asmunozv/Deber2/issues/8).
5. [Registro de ADR](docs/sprint-2/09-ADR.md) y [`docs/adr/`](docs/adr/) — [Issue #9](https://github.com/asmunozv/Deber2/issues/9).

## Entregables de Sprint 3 (interacciones, patrones y calidad) — terminado
1. [Matriz de interacciones](docs/sprint-3/10-MATRIZ-INTERACCIONES.md) — [Issue #10](https://github.com/asmunozv/Deber2/issues/10).
2. [Informe de patrones](docs/sprint-3/11-PATRONES.md) — [Issue #11](https://github.com/asmunozv/Deber2/issues/11).
3. [Evidencia SOLID](docs/sprint-3/12-SOLID.md) — [Issue #12](https://github.com/asmunozv/Deber2/issues/12).
4. [Requisitos de calidad](docs/sprint-3/13-REQUISITOS-CALIDAD.md) — [Issue #13](https://github.com/asmunozv/Deber2/issues/13).
5. [Revisión de diagramas y ADR](docs/sprint-3/14-REVISION-DIAGRAMAS-ADR.md) — [Issue #14](https://github.com/asmunozv/Deber2/issues/14).

## Entregables de Sprint 4 (síntesis y comunicación) — terminado
1. [Propuesta visual del dashboard](docs/sprint-4/15-DASHBOARD.md) + [prototipo HTML](docs/dashboard/index.html) — [Issue #15](https://github.com/asmunozv/Deber2/issues/15).
2. [Política de versionamiento](docs/sprint-4/16-VERSIONAMIENTO.md) — [Issue #16](https://github.com/asmunozv/Deber2/issues/16).
3. [Revisión integral](docs/sprint-4/17-REVISION-INTEGRAL.md) — [Issue #17](https://github.com/asmunozv/Deber2/issues/17).
4. [Presentación del flujo vertical](docs/sprint-4/18-PRESENTACION.md) — [Issue #18](https://github.com/asmunozv/Deber2/issues/18).
5. [Informe final y cierre](docs/sprint-4/19-INFORME-FINAL.md) — [Issue #19](https://github.com/asmunozv/Deber2/issues/19).

## Diagramas fuente (C4 / UML)
Disponibles en [`docs/diagrams/`](docs/diagrams/) en formato **Mermaid (`.mmd`)**, versionables y renderizables en GitHub.

## Estado
Los cuatro sprints están **terminados** con revisión cruzada, retrospectiva y ADR ratificados (21–24/11/2026). Ver [SPRINTS.md](docs/SPRINTS.md) y los registros de revisión por sprint.
