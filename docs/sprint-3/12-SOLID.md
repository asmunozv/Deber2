# Sprint 3 — Evidencia de principios SOLID

> **Auditoría documental (23/11/2026):** el contenido técnico está redactado. Las revisiones, aprobaciones, etiquetas/releases y actos de cierre solo deben declararse realizados si existen evidencias correspondientes en GitHub o actas confirmadas por el equipo.


**Issue:** [#12](https://github.com/asmunozv/Deber2/issues/12) · **Versión:** 1.0 · **Estado:** artefacto redactado; revisión y aceptación pendientes de verificar

La evidencia debe estar **visible en un diagrama o pseudocódigo** e indicar **qué cambio futuro facilita** cada decisión. Se usa el componente Inventario como referencia.

## S — Responsabilidad única (SRP)

El **cálculo de reposición** se separa del **registro de movimientos**.

```text
Inventario:
  registrarRecepcion(...)        -> registra movimiento y saldo
  reservarFEFO(...)              -> compromete unidades
  confirmarSalida(...)           -> descuenta y libera

Reposicion:                       (otro contenedor)
  evaluarUmbral(...)             -> detecta necesidad
  calcularSugerencia(...)        -> propone cantidad
```

**Cambio que facilita:** cambiar la fórmula de sugerencia (Reposición) **no toca** el registro de movimientos (Inventario).

## O — Abierto/cerrado (OCP)

Agregar una **nueva estrategia FEFO o de reposición** sin modificar el flujo principal.

```text
interface PoliticaSeleccionLotes {
  seleccionar(lotesElegibles, cantidad): LotesAsignados
}

class FEFOPorVencimiento implements PoliticaSeleccionLotes { ... }
class FEFOPorRecepción implements PoliticaSeleccionLotes { ... }   // futura

// El caso de uso reservaFEFO depende de la interfaz, no de la clase concreta.
```

**Cambio que facilita:** introducir un criterio de desempate distinto (o FEFO para no perecibles) **sin tocar** `reservaFEFO`.

## L — Sustitución de Liskov (LSP)

Sustituir un **adaptador de transportista** sin romper el contrato usado por Flota.

```text
interface NotificadorTransportista {
  notificarDespacho(despacho): void
}

class AdaptadorTransportistaA implements NotificadorTransportista { ... }
class AdaptadorTransportistaB implements NotificadorTransportista { ... }
// Flota usa NotificadorTransportista; cualquiera de los dos es sustituible.
```

**Cambio que facilita:** cambiar de transportista **no altera** el flujo de Flota.

## I — Segregación de interfaces (ISP)

Separar interfaces de **consulta**, **reserva** y **ajuste** en lugar de una interfaz general de Inventario.

```text
interface ConsultaInventario {  consultarDisponibilidad(...)  }
interface ReservaInventario  {  reservarFEFO(...)             }
interface AjusteInventario   {  registrarAjuste(...)          }
```

**Cambio que facilita:** un consumidor (p. ej. Reposición) depende solo de `ConsultaInventario`, sin verse forzado a conocer reservas ni ajustes.

## D — Inversión de dependencias (DIP)

Los casos de uso del dominio dependen de **puertos/interfaces**, no de clientes concretos (base de datos, broker, ERP).

```text
class RegistrarRecepcion {
  constructor(puertoStock: RepositorioStock, puertoEventos: PublicadorEventos) { ... }
}

// RegistrarRecepcion no depende de PostgreSQL ni de Kafka: depende de puertos.
```

**Cambio que facilita:** sustituir la base de datos o el broker por otra tecnología **sin cambiar** el caso de uso.

## Evidencia en diagrama

Los puertos de entrada/salida del dominio están representados en [`c4-componente-inventario.mmd`](../diagrams/c4-componente-inventario.mmd) (API de entrada, repositorios, Outbox), que muestra la separación entre dominio e infraestructura (SRP y DIP) y la interfaz única de selección de lotes (OCP/LSP).

## Criterios de aceptación de #12

- [x] Los cinco principios con evidencia en pseudocódigo y vínculo al diagrama.
- [x] Cada principio indica el cambio futuro que facilita.
- [ ] Revisión por otro integrante.

**Relaciones:** [Patrones](11-PATRONES.md) · [C4](../sprint-2/05-C4-ARQUITECTURA.md).
