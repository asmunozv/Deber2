# Control de entrega y validaciones pendientes

**Corte de auditoría: 24/11/2026.** Los artefactos principales están versionados y enlazados. El paquete todavía tiene pendientes de revisión cruzada, actas/retrospectivas y validación del archivo final Word. El plan de cuatro sprints de dos semanas no demuestra por sí solo que se hayan ejecutado ocho semanas de trabajo.

## Matriz de rúbrica

| Criterio | Puntos | Evidencia | Pendiente |
|---|---:|---|---|
| Gestión de sprints | 1,5 | [Plan](SPRINTS.md) y [issues](https://github.com/asmunozv/Deber2/issues) | Revisiones faltantes, fechas reales y retrospectivas |
| Límites y C4 | 2,0 | [Arquitectura](sprint-2/05-C4-ARQUITECTURA.md), [datos](sprint-2/06-PROPIEDAD-DE-DATOS.md) | Revisión final humana; exportaciones solo si se insertan en el informe |
| Flujos | 1,5 | [UML](diagrams/) y [matriz](sprint-3/10-MATRIZ-INTERACCIONES.md) | Revisión de UML de recepción/reposición y matriz |
| Calidad | 1,0 | [Requisitos](sprint-3/13-REQUISITOS-CALIDAD.md) | Confirmar umbrales propuestos con el equipo |
| Patrones | 1,0 | [Siete patrones](sprint-3/11-PATRONES.md) | Revisión cruzada registrada; validar coherencia final |
| SOLID | 1,0 | [Evidencias](sprint-3/12-SOLID.md) | Revisión cruzada registrada; validar coherencia final |
| Versionamiento | 1,0 | [Política](sprint-4/16-VERSIONAMIENTO.md), [ADR](adr/) | Revisar la trazabilidad; etiquetas Git son opcionales según la política |
| Trazabilidad y presentación | 1,0 | [README](../README.md), [presentación HTML](../presentacion.html), [Word](../INFORME-SmartInventory.docx) | QA visual del Word, ensayo y entrega en plataforma |

## Correcciones realizadas en la auditoría del 24/11

- [x] Roles y responsables: Lau (@crazylilypad0801), Ana (@anypau) y Ariana (@asmunozv).
- [x] Se asignaron nominalmente responsables a las 19 issues.
- [x] Presupuesto monetario previsto entre USD 0 y USD 20, con IA opcional.
- [x] Se conservó la duración formal de dos semanas por sprint, distinguiéndola de las 54 horas-persona estimadas.
- [x] Se corrigió el README y la planificación para no declarar sprints cerrados sin evidencia.
- [x] Se corrigió el porcentaje del gráfico de stock normal del dashboard (68 %, consistente con 8.486 de 12.480 unidades).
- [x] Se alineó la descripción del dashboard con sus secciones reales y sus datos ilustrativos.
- [x] Se corrigió el índice ADR: los siete ADR permanecen Propuestos, no Aceptados; se añadieron alternativas a ADR-0004..0007.
- [x] Se sustituyó la etiqueta “API / puerto de entrada” por “Puerto de entrada” en los diagramas C4 y se sincronizó el exportador Mermaid.
- [x] Se aclaró la ubicación del patrón Outbox en los diagramas y su aplicación conceptual en Reposición.
- [x] Se actualizaron los registros de revisión con los comentarios cruzados que sí aparecen en GitHub.

## Estado de GitHub al 24/11/2026

- **12 issues cerradas y 7 abiertas** (#1, #2, #7, #10, #14, #16 y #19).
- Las issues #3 y #4 tienen comentarios cruzados de Ariana.
- Las issues #5, #6, #9, #11, #13 y #17 tienen comentarios cruzados de Ariana.
- Las issues #8, #12, #15 y #18 tienen comentarios cruzados de Lau.
- **#1 y #2 fueron reabiertas porque no se identificó un comentario de revisión independiente**. Deben revisarse antes de cerrar el Sprint 1.
- Las issues #7, #10, #14, #16 y #19 siguen abiertas y sin comentario de revisión observado.
- La ratificación de los ADR continúa pendiente: están correctamente marcados como Propuestos.

## Acciones pendientes antes de la entrega final

- [ ] **Issues #1 y #2:** obtener revisión independiente y regularizar el cierre, porque se reabrieron para completar la revisión cruzada.
- [ ] **Issues #7, #10, #14, #16 y #19:** completar revisión por otra persona, comprobar criterios y cerrar solo cuando se cumpla el DoD.
- [ ] **Diagramas exportados:** generar SVG/PNG únicamente si se van a insertar en el informe; guardar los archivos realmente usados en docs/diagrams/exports. El visor [exportar.html](diagrams/exportar.html) descarga imágenes localmente, no las sube a GitHub.
- [ ] **ADR:** el equipo debe ratificar o mantener explícitamente como propuestas las decisiones; no cambiar a Aceptado sin evidencia.
- [ ] **Fechas y ceremonias:** registrar fechas reales de inicio/fin, Sprint Review y retrospectiva; no inventar fechas ni asistentes.
- [ ] **Informe Word:** verificar portada, autores, contenido, diagramas, legibilidad y paginación. Se confirmó la existencia del archivo, pero no se pudo inspeccionar su renderizado visual desde el conector de GitHub.
- [ ] **Presentación:** abrir presentacion.html en navegador y ensayar el flujo recepción → stock → alerta → reposición.
- [ ] **Entrega:** subir el enlace del repositorio y el archivo Word o PDF final a la plataforma de la materia.

## Plantilla para comentario verificable en una issue

Autor del artefacto: ___  
Revisor (otra persona): ___  
Fecha real: ___  
Versión o commit: ___  
Criterios verificados: ___  
Hallazgos y correcciones: ___  
Resultado: aprobado / cambios solicitados.

## Estado de cierre

| Sprint | Documentos disponibles | Revisión cruzada | Review/retro formal | Estado |
|---|---|---|---|---|
| 1 | Sí | Parcial: #3 y #4; #1 y #2 abiertas para revisión | Pendiente | En validación |
| 2 | Sí | Parcial: #5, #6, #8, #9; #7 pendiente | Pendiente | En validación |
| 3 | Sí | Parcial: #11, #12, #13; #10 y #14 pendientes | Pendiente | En validación |
| 4 | Sí | Parcial: #15, #17, #18; #16 y #19 pendientes | Pendiente | En validación |

El deber de Diseño de Sistemas no exige endpoints, contratos técnicos, CI/CD, despliegue ni pruebas de software.
