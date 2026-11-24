# Sprint 2 — Arquitectura C4 y límites de servicio

> **Estado verificado (auditoría 23/11/2026):** archivo de diseño disponible. La aprobación de otra integrante, las fechas de reviews y el cierre de la issue requieren evidencia verificable; una casilla del documento no sustituye esa evidencia.


**Issue:** [#5](https://github.com/asmunozv/Deber2/issues/5) · **Versión:** 1.0 · **Estado:** artefacto redactado; validación documental pendiente

## 1. Decisión de arquitectura de referencia

Siguiendo la **Figura 1** del enunciado, Smart Inventory se modela como una plataforma empresarial integrada que **puede evolucionar hacia microservicios**. La arquitectura combina:

- **Interacciones síncronas** para consultas y comandos inmediatos (reservar, ajustar, consultar disponibilidad).
- **Mensajería asíncrona** (broker) para comunicar hechos de negocio (stock actualizado, pedido creado, despacho en ruta).
- **Cada servicio es propietario de sus datos**: ninguna capacidad modifica directamente datos de otra.
- Una **capa de aplicación** coordina las consultas y acciones del dashboard.
- El **broker** alimenta la **proyección de lectura** (dashboard) y el **Lakehouse** (analítica).

La regla de diseño no premia la cantidad de servicios: premia que **cada responsabilidad tenga un dueño claro**, que **los datos no se modifiquen de forma cruzada** y que las interacciones sean **coherentes con los flujos de negocio**.

## 2. C4 — Nivel 1: contexto del sistema

Fuente: [`c4-contexto.mmd`](../diagrams/c4-contexto.mmd).

```mermaid
flowchart LR
    subgraph USU["Personas (actores internos)"]
        OPR["Operador de recepción"]
        ALM["Encargado de almacén"]
        PLA["Planificador de compras"]
        FULP["Coordinador de pedidos"]
        FLO["Coordinador de flota"]
        SUP["Supervisión / gerencia"]
    end
    SI["Smart Inventory<br/>Plataforma de inventario,<br/>fulfillment y operación logística"]
    subgraph EXT["Sistemas externos"]
        ERP["ERP / proveedores<br/>(órdenes de compra)"]
        TRS["Transportistas<br/>(estado de entregas)"]
    end
    OPR -->|"registra recepción"| SI
    ALM -->|"consulta y ajusta stock"| SI
    PLA -->|"revisa y aprueba reposición"| SI
    FULP -->|"reserva y despacha pedidos"| SI
    FLO -->|"asigna vehículos y AMR"| SI
    SUP -->|"lee indicadores"| SI
    SI -->|"sincroniza compras"| ERP
    SI -->|"notifica despachos"| TRS
```

## 3. C4 — Nivel 2: contenedores

Fuente: [`c4-contenedores.mmd`](../diagrams/c4-contenedores.mmd).

```mermaid
flowchart TB
    subgraph SYS["Smart Inventory — contenedores"]
        direction TB
        APP["Capa de aplicación<br/>(orquesta consultas y acciones del dashboard)"]
        subgraph NEG["Capacidades de negocio (propietarias de sus datos)"]
            CAT["Catálogo<br/>y ubicaciones"]
            INV["Inventario<br/>(stock, lotes, movimientos)"]
            REP["Reposición<br/>y compras"]
            FUL["Fulfillment<br/>y pedidos"]
            FLT["Flota<br/>y operación"]
        end
        subgraph LEC["Lectura y análisis"]
            DAS["Dashboard"]
            ANA["Analítica"]
            PROY[("Proyección<br/>de lectura")]
            LAKE[("Lakehouse")]
        end
        BROKER{{"Broker de eventos"}}
    end
    DBCAT[("BD<br/>Catálogo")]
    DBINV[("BD<br/>Inventario")]
    DBREP[("BD<br/>Reposición")]
    DBFUL[("BD<br/>Fulfillment")]
    DBFLT[("BD<br/>Flota")]
    APP -->|"consulta / comando inmediato"| CAT
    APP -->|"consulta / comando inmediato"| INV
    APP -->|"consulta / comando inmediato"| REP
    APP -->|"consulta / comando inmediato"| FUL
    APP -->|"consulta / comando inmediato"| FLT
    INV -->|"valida SKU y lote"| CAT
    FUL -->|"reserva / salida de unidades"| INV
    REP -->|"consulta disponibilidad"| INV
    FUL -->|"asigna recurso logístico"| FLT
    CAT --- DBCAT
    INV --- DBINV
    REP --- DBREP
    FUL --- DBFUL
    FLT --- DBFLT
    INV -. "hecho: stock actualizado" .-> BROKER
    FUL -. "hecho: pedido / reserva / despacho" .-> BROKER
    REP -. "hecho: sugerencia / orden de compra" .-> BROKER
    FLT -. "hecho: telemetría / progreso" .-> BROKER
    BROKER -.->|"proyecta lecturas"| PROY
    BROKER -.->|"carga histórico"| LAKE
    DAS -->|"consulta vista optimizada"| PROY
    ANA -->|"consulta histórico"| LAKE
    DAS -->|"aprobar sugerencia / reservar"| APP
```

### Contenedores y su responsabilidad

| Contenedor | Responsabilidad | Dato propietario (resumen) |
|---|---|---|
| **Catálogo** | Información maestra de producto y ubicaciones | SKU, categorías, bodegas, zonas, ubicaciones |
| **Inventario** | Stock físico y comprometido, lotes, movimientos | Saldos por lote/ubicación, recepciones, salidas, transferencias, ajustes, historial |
| **Reposición** | Señales y decisiones de abastecimiento | Umbrales, alertas, sugerencias, proveedores, órdenes de compra |
| **Fulfillment** | Ciclo de vida del pedido y su preparación/despacho | Pedidos, líneas, estados |
| **Flota** | Operación logística de AMR, camiones y muelles | Vehículos, AMR, rutas, telemetría, asignaciones |
| **Dashboard** | Lectura operativa agregada | Preferencias de vista y proyección derivada |
| **Analítica** | Interpretación histórica | Modelos y series históricas derivadas |
| **Capa de aplicación** | Orquestar consultas y acciones | Sin datos de negocio propios |
| **Broker** | Transportar hechos de negocio | Colas/tópicos (infraestructura) |
| **Proyección de lectura** | Vista optimizada para el dashboard | Estado proyectado (derivado) |
| **Lakehouse** | Conservar histórico para análisis | Datos históricos (derivados) |

> Las bases de datos se representan como **propiedad lógica** de cada servicio. Pueden compartir infraestructura física **si** se mantienen aisladas por esquema y permisos.

## 4. C4 — Nivel 3: componentes (límites sensibles)

Se detallan los dos contenedores con mayor riesgo de consistencia: **Inventario** y **Fulfillment**.

### 4.1 Inventario — [`c4-componente-inventario.mmd`](../diagrams/c4-componente-inventario.mmd)

```mermaid
flowchart TB
    subgraph INV["Contenedor: Inventario"]
        direction TB
        API["API / puerto de entrada<br/>(consulta, reserva, ajuste)"]
        REC["Gestión de recepciones"]
        MOV["Gestión de movimientos<br/>(salidas, transferencias, ajustes)"]
        RES["Reserva FEFO<br/>(compromiso de lotes)"]
        DISP["Servicio de disponibilidad<br/>(físico − reservado)"]
        DOM["Núcleo de dominio<br/>(lote, saldo, movimiento, reserva)"]
        OUT["Outbox<br/>(publica hechos de stock)"]
        REPO["Repositorios<br/>(lotes, saldos, movimientos, reservas)"]
    end
    DB[("BD<br/>Inventario")]
    API --> REC
    API --> MOV
    API --> RES
    API --> DISP
    REC --> DOM
    MOV --> DOM
    RES --> DOM
    DISP --> DOM
    DOM --> REPO
    REPO --> DB
    DOM --> OUT
    OUT -. "hecho: stock actualizado" .-> BROKER{{"Broker de eventos"}}
```

### 4.2 Fulfillment — [`c4-componente-fulfillment.mmd`](../diagrams/c4-componente-fulfillment.mmd)

```mermaid
flowchart TB
    subgraph FUL["Contenedor: Fulfillment"]
        direction TB
        API["API / puerto de entrada<br/>(pedidos, reservas, despacho)"]
        PED["Gestión de pedidos<br/>(estado del pedido)"]
        PREP["Preparación<br/>(tareas de picking)"]
        DES["Despacho<br/>(intención de salida y confirmación)"]
        DOM["Núcleo de dominio<br/>(pedido, línea, estado)"]
        OUT["Outbox<br/>(publica hechos de pedido)"]
        REPO["Repositorios<br/>(pedidos, líneas, estados)"]
    end
    DB[("BD<br/>Fulfillment")]
    INV["Inventario<br/>(reserva / salida)"]
    FLT["Flota<br/>(asignación logística)"]
    API --> PED
    API --> PREP
    API --> DES
    PED --> DOM
    PREP --> DOM
    DES --> DOM
    DOM --> REPO
    REPO --> DB
    DOM --> OUT
    DOM -->|"solicita reserva / salida"| INV
    DOM -->|"solicita asignación de vehículo"| FLT
    OUT -. "hecho: pedido / reserva / despacho" .-> BROKER{{"Broker de eventos"}}
```

## 5. Límite sensible: pedido versus compromiso físico

| Concepto | Propietario | Explicación |
|---|---|---|
| **Pedido** y sus estados | Fulfillment | Ciclo de vida comercial del pedido |
| **Compromiso de unidades en lotes** (reserva física) | Inventario | Evita sobreasignar el mismo lote a dos pedidos |

**Invariante de coherencia:** una reserva confirmada en Fulfillment **sin** unidades comprometidas en Inventario es una inconsistencia. Por eso la reserva es una interacción síncrona `Fulfillment → Inventario` que confirma o rechaza de forma atómica (ver [08-FLUJOS-RESERVA-DESPACHO.md](08-FLUJOS-RESERVA-DESPACHO.md)).

## 6. Criterios de aceptación de #5

- [x] Diagramas C4 niveles 1, 2 y 3 en fuente Mermaid versionable.
- [x] Cada contenedor tiene responsabilidad y dato propietario explícito.
- [x] Interacciones síncronas y asíncronas diferenciadas.
- [x] Límite pedido/reserva física documentado.
- [ ] Revisión por otro integrante.
- [ ] Ajustes y ratificación en ADR (enlace desde el issue).

**Relaciones:** [Propiedad de datos](06-PROPIEDAD-DE-DATOS.md) · [Flujos recepción/reposición](07-FLUJOS-RECEPCION-REPOSICION.md) · [Flujos reserva/despacho](08-FLUJOS-RESERVA-DESPACHO.md) · [ADR](09-ADR.md).
