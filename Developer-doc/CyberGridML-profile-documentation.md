# CyberGridML Library Description

## Overview

CyberGridML is a [SysML v2 library](https://github.com/cybergridml/cybergrid-modeller/tree/main/CybergridML/src/main/resources/sysml.cybergridML.libraries).

The library combines three main aspects:

The library provides reusable datatypes and enumerations for representing technical properties such as voltage, power, latency, capacity, and energy.

## Library Structure

```text
CyberGridML
├── CyberGridMLEnum
├── CyberGridMLDatatypes
└── CyberGridMLProfile
    ├── CRA
    └── CFA
   

    
```

The packages are organized to separate common definitions from the architecture models.

## CyberGridMLEnum

The `CyberGridMLEnum` package contains the enumeration definitions used throughout the library.

### Electrical Units

The library defines enumerations for:

* `VoltageUnitKind`: `V`, `KV`, `MV`
* `PowerUnitKind`: `W`, `KW`, `MW`
* `EnergyUnitKind`: `J`, `KJ`, `Wh`, `KWh`, `MWh`
* `CurrentUnitKind`: `A`, `MA`
* `ReactivePowerUnitKind`: `VAR`, `KVAR`, `MVAR`

### Communication and Time Units

The following enumerations describe communication and time-related units:

* `LatencyUnitKind`: from nanoseconds to minutes
* `CapacityUnitKind`: from bytes to petabytes
* `TimeUnitKind`: seconds, milliseconds, microseconds, minutes, hours, days, and ticks

### Other Enumerations

`RedundancyKind` defines the supported redundancy mechanisms:

* `consensus`
* `hypervisor`
* `active_standby`

`VoltageLevel` defines the supported grid voltage levels, from `20` to `380`.

`ControlType` defines the control modes available in the library, such as `DefaultControl`, `Limiter`, and MPC-related control types.

## CyberGridMLDatatypes

The `CyberGridMLDatatypes` package provides reusable definitions for technical and non-functional properties.

### Non-Functional Properties

The library defines several `NFP` types:

| Type                | Description                       |
| ------------------- | --------------------------------- |
| `NFP_Latency`       | Communication latency             |
| `NFP_Capacity`      | Communication or storage capacity |
| `NFP_Voltage`       | Electrical voltage                |
| `NFP_Power`         | Active power                      |
| `NFP_Energy`        | Energy                            |
| `NFP_Current`       | Electrical current                |
| `NFP_ReactivePower` | Reactive power                    |

Each NFP generally contains a **unit** and a **value/precision** attribute.

For example:

```text
NFP_Voltage
├── unit
└── precision
```

These types are reused by the physical and cyber architectures.

### Period

`Period` represents a time interval using a start and finish value.

```text
Period
├── start
└── finish
```

It is used, for example, to describe software activation periods and execution delays.

### Hazard

`Hazard` is a metadata definition used to attach hazard-related information to model elements.

It contains:

* `description`
* `justification`
* `period`
* `percent`

This provides a way to associate additional safety or risk-related information with the model.

## CyberGridMLProfile

The `CyberGridMLProfile` contains the main architectural definitions.

It is divided into two packages:

* `CRA` —  Resource Architecture
* `CFA` —  Functional Architecture

## CRA — 

The `CRA` package represents the **infrastructure** of the system.

### ComputingResource

`ComputingResource` represents a computational platform capable of hosting software resources.

### SoftwareResource

`SoftwareResource` represents a software component running on a computing resource.

It includes:

* `Activation_period`
* `Execution_delay`

These properties can be used to describe when a software component is activated and its execution timing.

### RedundancyCluster

`RedundancyCluster` represents a set of redundant software resources.

It defines:

* An associated redundancy mechanism through `runtime`
* One or more active software resources
* One or more passive software resources
* An optional hypervisor

```text
RedundancyCluster
├── runtime
├── active
├── passive
└── hypervisor
```

### CommunicationMedia

`CommunicationMedia` represents a communication between resources.

It provides two main properties:

* `capacity`
* `latency`

Both properties use the reusable datatypes defined in `CyberGridMLDatatypes`.

### CRA Relationships

Three allocation/connection relationships are defined:

`Allocate` connects a `ComputingResource` with a `SoftwareResource`.

`Connect` connects a `ComputingResource` with a `CommunicationMedia`.

`Link` connects two `CommunicationMedia` elements.

Together, these relationships can be used to describe how software is deployed and how resources communicate.

## CFA — Functional Architecture

The `CFA` package represents the **electrical grid and its control system**.

### GridElement

`GridElement` is the base definition for grid-related elements.

Other elements such as `MainGrid` and `Zone` specialize this definition.

### MainGrid

`MainGrid` represents the overall electrical grid.

It can contain:

* Substations
* Zones
* Lines
* A central controller

```text
MainGrid
├── Substation
├── Zone
├── Line
└── CentralController
```

### Zone

`Zone` represents a section of the main grid.

A zone contains:

* A zonal controller
* One or more substations
* Lines

`Zone` also specializes `GridElement`.

### Substation

`Substation` represents an electrical substation.

It contains one or more buses and can reference one or more zones.

### Bus

`Bus` represents an electrical bus inside a substation.

It defines:

* `nominalLevel` — nominal voltage
* `connected` — connection status
* `equipments` — equipment connected to the bus
* `substation` — associated substation

### Equipment

`Equipment` is the base definition for electrical equipment.

It provides common properties such as:

* `connected`
* `p` — active power
* `q` — reactive power
* `activable`
* `localController`

Three specialized equipment types are defined:

```text
Equipment
├── Generator
├── Battery
└── Load
```

`Generator` represents a power generation unit.

`Battery` represents an energy storage device.

`Load` represents an electrical consumption unit.

### Controllers

The library defines a hierarchy of controllers.

```text
Controller
├── CentralController
├── ZonalController
└── LocalController
```

`Controller` provides the common `controlBehavior` property.

`CentralController` is associated with the `MainGrid`.

`ZonalController` is associated with a `Zone`.

`LocalController` is used at the equipment level.

### Line

`Line` represents an electrical line in the grid.

A line references:

* Its main grid
* One or two terminals

### Terminal

`Terminal` represents an endpoint of a line.

It specializes `Equipment` and provides electrical and structural information such as:

* `finish`
* `branch`
* `side`
* `ecr` — current
* `v` — voltage

A terminal also references its associated line.

### Control

`Control` represents a relationship between a grid element and a controller.

```text
GridElement ───── Control ───── Controller
```

This relationship allows the control architecture to be connected to the physical grid model.


## Package Dependencies

```text
CyberGridMLEnum
       │
       ▼
CyberGridMLDatatypes
       │
       ▼
CyberGridMLProfile
       │
    ┌──┴──┐
    ▼     ▼
   CRA   CFA
```

`CyberGridMLEnum` provides the enumerations used by the datatypes.

`CyberGridMLDatatypes` provides reusable technical properties.

`CyberGridMLProfile` uses these definitions to build the cyber and physical architectures.

## SysML v2 Concepts

CyberGridML uses several standard SysML v2 concepts:

* **Packages** to organize the library
* **Part definitions** to represent system elements
* **Attributes** to represent properties
* **References** to connect model elements
* **Allocations** to represent resource relationships
* **Enumerations** for predefined values
* **Metadata definitions** for additional information
* **Specialization** to create hierarchical definitions

## Conclusion

CyberGridML provides a modular SysML v2 framework for representing **cyber-physical power systems**.

The library separates:

* Common enumerations and datatypes
* Cyber resources and communication infrastructure
* Electrical grid components
* Control architecture
* Hazard-related metadata

This structure provides a foundation that can be extended to model more detailed electrical, cyber, communication, and control aspects of a power system.


[← Back to the main documentation](../README.md)