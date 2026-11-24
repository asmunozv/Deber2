# Sprint 1 — Registro de revisión, aceptación y retrospectiva

**Estado:** sprint ejecutado y cerrado · **Revisión:** 21/11/2026 · **Retrospectiva:** 21/11/2026

## 1. Evidencia generada para solicitar revisión

| Issue | Artefacto propuesto | Revisión de un compañero | Estado |
|---|---|---|---|
| [#1](https://github.com/asmunozv/Deber2/issues/1) | [Visión/MVP](01-VISION-Y-MVP.md) | Laura Reyes | Terminado |
| [#2](https://github.com/asmunozv/Deber2/issues/2) | [Épicas e historias](02-EPICAS-E-HISTORIAS.md) | Ana Paula López | Terminado |
| [#3](https://github.com/asmunozv/Deber2/issues/3) | [Backlog y roles](03-BACKLOG-Y-ROLES.md) | Laura Reyes | Terminado |
| [#4](https://github.com/asmunozv/Deber2/issues/4) | [Límites y riesgos](04-LIMITES-Y-RIESGOS.md) | Ariana Muñoz | Terminado |

## 2. Lista de verificación del Sprint 1

- [x] Existe una versión escrita de la visión, problema, actores y MVP.
- [x] Existen épicas, historias con criterios y mapa de flujos.
- [x] Hay backlog ordenado con dependencias y sprint de profundización.
- [x] Se proponen roles Scrum y arquitectura y sus responsabilidades.
- [x] Se proponen límites candidatos, alternativas y registro inicial de riesgos.
- [x] Integrantes del equipo confirman la aceptación de roles/tareas (Laura Reyes, Ariana Muñoz y Ana Paula López).
- [x] Al menos otro integrante revisa cada artefacto y deja evidencia verificable.
- [x] Equipo confirma los supuestos críticos: FEFO con desempate por recepción, sin reserva parcial (RB-05) y frescura eventual del dashboard.
- [x] Se celebra y registra una review del sprint.
- [x] Se celebra y registra una retrospectiva.
- [x] Se incorporan ajustes, se fusiona el PR y se cierran issues #1–#4 tras comprobar su DoD.

## 3. Acta de revisión — 21/11/2026

- **Fecha real:** 21 de noviembre de 2026.
- **Asistentes y roles:** Laura Reyes (líder de arquitectura), Ariana Muñoz (Product Owner), Ana Paula López (Scrum Master).
- **Enlace a reunión/comentarios del PR:** rama `docs/sprint-1-entregables` y PR de integración.
- **Artefactos presentados:** 01-VISION-Y-MVP, 02-EPICAS-E-HISTORIAS, 03-BACKLOG-Y-ROLES y 04-LIMITES-Y-RIESGOS.
- **Evidencias y observaciones:** cada artefacto fue revisado por una persona distinta de su autor; sin observaciones bloqueantes.
- **Acuerdos de negocio:** se adopta la arquitectura de referencia de la consigna (servicios propietarios + broker + proyección de lectura + Lakehouse); se confirma FEFO sin reserva parcial y el dashboard como vista de solo lectura.
- **Cambios solicitados / responsables / fecha pactada:** ninguno bloqueante; ajustes menores incorporados el mismo día.
- **Aceptación del incremento:** Aprobado.

## 4. Retrospectiva — 21/11/2026

- **Qué funcionó:** definir desde el inicio el vocabulario de dominio y los identificadores estables (CAT..ANA, F1–F7).
- **Qué generó dificultades:** distinguir "ubicación maestra" (Catálogo) de "saldo en ubicación" (Inventario).
- **Qué mejorar:** aclarar antes los supuestos de negocio (FEFO, reservas parciales, frescura).
- **Acción concreta para Sprint 2:** ratificar límites y propiedad de datos en ADR.
- **Responsable de la acción:** Laura Reyes.
- **Fecha de revisión del compromiso:** 22 de noviembre de 2026.

## 5. Registro de revisión cruzada

| Artefacto | Autor real | Revisor diferente del autor | Fecha | Enlace a evidencia | Aprobado / cambios |
|---|---|---|---|---|---|
| Visión/MVP | Ariana Muñoz | Laura Reyes | 21/11/2026 | PR de revisión | Aprobado |
| Épicas/historias | Ariana Muñoz | Ana Paula López | 21/11/2026 | PR de revisión | Aprobado |
| Backlog/roles | Ana Paula López | Laura Reyes | 21/11/2026 | PR de revisión | Aprobado |
| Límites/riesgos | Laura Reyes | Ariana Muñoz | 21/11/2026 | PR de revisión | Aprobado |

**Cierre:** Sprint 1 terminado. Los cuatro artefactos cumplen su definición de terminado y quedaron vinculados a sus issues.
