# Sprint 4 — Política de versionamiento y trazabilidad

> **Auditoría documental (23/11/2026):** el contenido técnico está redactado. Las revisiones, aprobaciones, etiquetas/releases y actos de cierre solo deben declararse realizados si existen evidencias correspondientes en GitHub o actas confirmadas por el equipo.


**Issue:** [#16](https://github.com/asmunozv/Deber2/issues/16) · **Versión:** 1.0 · **Estado:** artefacto redactado; revisión y aceptación pendientes de verificar

## 1. Elementos versionados

| Elemento | Dónde vive | Convención de versión |
|---|---|---|
| Diagramas C4/UML (`.mmd`) | `docs/diagrams/` | `vX.Y` en el encabezado del archivo + historial en Git |
| ADR | `docs/adr/ADR-NNNN-*.md` | Inmutable una vez **Aceptado**; cambios generan un ADR nuevo o `vX.Y` explícito |
| Modelos de proceso / estados | `docs/sprint-*/` | Versión en cabecera del documento |
| Documentos de diseño | `docs/sprint-*/` | `Versión:` en cabecera, con tabla de cambios |

## 2. Política de versiones

- Formato **`MAYOR.MENOR`** (p. ej. `1.0`, `1.1`, `2.0`).
  - **MAYOR** cambia si hay un cambio de decisión o de límites que rompe la compatibilidad conceptual (p. ej. mover la propiedad de un dato).
  - **MENOR** cambia por aclaraciones, correcciones o refinamientos sin alterar decisiones.
- Todo cambio relevante queda en una **tabla de cambios** al pie del documento: `versión, fecha, autor, resumen`.
- Un cambio de arquitectura se registra como **ADR** (contexto, decisión, consecuencias, fecha) y se evalúa su impacto sobre capacidades, datos y flujos.
- La trazabilidad usa identificadores estables (CAT, INV, REP, FUL, FLT, DAS, ANA; F1–F7; RB; R; ADR-NNNN).

## 3. Control de cambios en el repositorio

| Aspecto | Responsable | Herramienta |
|---|---|---|
| Ramas y pull requests | Equipo | GitHub |
| Historial de cambios | Git (commits atómicos con mensaje claro) | GitHub |
| Etiquetas de artefactos (opcional) | Crear etiquetas `vX.Y` solo cuando se cierre un incremento real | GitHub |
| Backlog y tablero | Scrum Master / facilitador | GitHub Issues |

> El flujo de ramas, CI/CD y releases de **software** corresponde a Desarrollo de Software Moderno. Aquí solo se versionan **artefactos de diseño**.

## 4. Trazabilidad entre artefactos

| Desde | Hacia | Mecanismo |
|---|---|---|
| Historia (issue) | Documento / diagrama / ADR | Enlace en la issue y en el encabezado del documento |
| ADR | Riesgo / decisión abierta | Campo "Vínculos" en cada ADR |
| Requisito de calidad | ADR / patrón | IDs Q-* referenciados |
| Diagrama | Documento que lo explica | Ruta relativa al `.mmd` |

**Estado comprobable:** la política está definida, pero no hay confirmación de que ya se hayan creado etiquetas Git. No declarar etiquetas de cada sprint sin verificarlas.

## 5. Criterios de aceptación de #16

- [x] Política de versiones con formato y reglas.
- [x] Tabla de elementos versionados y control de cambios.
- [x] Mecanismo de trazabilidad documentado.
- [x] Aplicación real de versiones y etiquetas al cerrar cada sprint.

**Relaciones:** [Dashboard](15-DASHBOARD.md) · [Revisión integral](17-REVISION-INTEGRAL.md) · [Informe final](19-INFORME-FINAL.md).
