# Control de entrega y validaciones pendientes

**Corte de auditoría: 23/11/2026.** Los archivos existen, pero aprobación, revisión y cierre de los sprints requieren evidencia verificable. Los cuatro sprints de dos semanas son un plan de ocho semanas, no una ejecución demostrada en cuatro días.

## Matriz de rúbrica

| Criterio | Puntos | Evidencia | Pendiente |
|---|---:|---|---|
| Gestión de sprints | 1,5 | [Plan](SPRINTS.md) y [issues](https://github.com/asmunozv/Deber2/issues) | Revisiones y fechas reales, cierre conforme a DoD |
| Límites y C4 | 2,0 | [Arquitectura](sprint-2/05-C4-ARQUITECTURA.md), [datos](sprint-2/06-PROPIEDAD-DE-DATOS.md) | Revisión humana, exportaciones si usadas en informe |
| Flujos | 1,5 | [UML](diagrams/) y [matriz](sprint-3/10-MATRIZ-INTERACCIONES.md) | Cotejo final por equipo |
| Calidad | 1,0 | [Requisitos](sprint-3/13-REQUISITOS-CALIDAD.md) | Revisar umbrales y su justificación |
| Patrones | 1,0 | [Siete patrones](sprint-3/11-PATRONES.md) | Revisión independiente |
| SOLID | 1,0 | [Evidencias](sprint-3/12-SOLID.md) | Revisión independiente |
| Versionamiento | 1,0 | [Política](sprint-4/16-VERSIONAMIENTO.md), [ADR](adr/) | Corroborar etiquetas e historial de cambios |
| Trazabilidad y presentación | 1,0 | [README](../README.md), [presentación HTML](../presentacion.html), [Word](../INFORME-SmartInventory.docx) | Ensayo y QA visual del informe |

## Correcciones realizadas

- [x] Se documentaron Lau (líder y arquitectura), Ana (Scrum Master) y Ariana (Product Owner).
- [x] Se asignaron nominalmente responsables y horas estimadas a las 19 issues.
- [x] Presupuesto monetario previsto entre USD 0 y USD 20, con IA opcional.
- [x] Se conservó la duración formal de dos semanas por sprint, distinguiéndola de las 54 horas-persona estimadas.
- [x] Se corrigió el README y la planificación para no declarar cierres sin evidencia.
- [x] Se conservaron los diagramas fuente C4/UML, ADR y documentos técnicos.

## Acciones pendientes que no pueden declararse realizadas automáticamente

- [ ] **Revisión humana:** Lau, Ana y Ariana deben revisar artefactos de otra persona y comentar con nombre, fecha, hallazgos y aprobación real. Un PR fusionado no prueba por sí solo una review.
- [ ] **Fechas:** indicar inicio y fin efectivos si hubo cuatro ciclos de dos semanas; de lo contrario describirlos como planificación, no como sprints ejecutados.
- [ ] **Issues:** verificar criterios, comentarios, responsables y cerrar solo las que de verdad cumplan DoD. Los nombres de usuario GitHub de Lau y Ana no están confirmados; la asignación es textual.
- [ ] **Exportaciones:** guardar en docs/diagrams/exports las imágenes SVG/PNG de los diagramas que se inserten en el informe. Guía: [Mermaid](diagrams/README.md).
- [ ] **Versiones:** comprobar la existencia de etiquetas Git antes de decir que se crearon.
- [ ] **Informe Word:** verificar portada, autores, diagrama C4, UML, legibilidad y paginación. Se confirmó que el archivo existe, no su renderizado visual.
- [ ] **Presentación:** abrir y ensayar presentacion.html, con énfasis en recepción → stock → alerta → reposición.
- [ ] **Entrega:** subir enlace al repositorio e informe Word/PDF a la plataforma de la materia.

## Plantilla para comentario verificable en una issue

Autor del artefacto: ___  
Revisor (otra persona): ___  
Fecha real: ___  
Versión o commit: ___  
Criterios verificados: ___  
Hallazgos y correcciones: ___  
Resultado: aprobado / cambios solicitados.

## Estado de cierre

| Sprint | Documentos disponibles | Revisión y retrospectiva | Estado |
|---|---|---|---|
| 1 | Sí | Por corroborar | En validación |
| 2 | Sí | Por corroborar | En validación |
| 3 | Sí | Por corroborar | En validación |
| 4 | Sí | Por corroborar | En validación |

El deber de Diseño de Sistemas no exige endpoints, contratos técnicos, CI/CD, despliegue ni pruebas de software.