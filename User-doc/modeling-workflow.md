# Modeling Workflow

To obtain the description of a control architecture of the electrical grid, the user has to carry out several steps :
* [Create a Control Functional Architecture](#control-functional-architecture-creation)
    * Import relevant information from other formats such as iidm
    * (Optional) Define zones for targeted control
* Create a Control Resources Architecture
    * Define the communication resources
    * Define the hardware and software resources
    * Precise how the resources are linked to one another
*	Allocate the CFA onto the CRA
*	(Optional) Create Communication Hazards

## Control Functional Architecture Creation

We assume that the power grid topology, and more generally the details about the components of the electrical grid, already exist outside of the tool. From this topology and those details, an initialization script allows to create elements of the model. These elements may also be created manually by the user. The grid topology in the model describes the electrical situation, so it must 
* Describe the graph of the power grid : substations and line identifiers 
* Provide the electrical characteristics necessary for each node, such as which production or storage equipments are linked to each substation
* Provide electrical characteristics associated to each power line

Once the physical elements of the power grid are defined, the user can model the controllers and their relationship in order to devise some principle of control, and link them to the relevant parts of the power grid.

![alt text](image.png)

Once the relevant elements of the power grid are modeled, the user can model the [CFA](../Principles/metamodels.md#control-functional-architecture). 

**Initial elements**
The user must create a MainGrid and its associated controller called a CentralController. The MainGrid can then be filled with Substations, and below, Buses. These can be imported via an external file, as explained above. 

**Equipments**
The user can associate batteries, generators, loads and terminals to each bus. For each Battery, the user must provide values for the MaxPowerInjection and capacity properties. For each Generator, the user must provide values for the maxPowerGeneration and voltage properties. A LocalController must be associated to each equipment. These can also be created automatically from the elements of the external file describing the grid structure.

**Control elements**
The user can then define additional control equipments. If they want to model a situation with control zones, they have to create one or several zones that correspond to a logical division of the grid, these zones are associated with a ZonalController, and reference the Substations they control. 
For each controller (central, zonal or local), the user can specify a behavior. 

## Control Resources Architecture Creation

The user can then create a CRA (CRA = Control Resources Architecture). A CRA defines the material resources that are involved in the control implementation : [computing resources](../Principles/metamodels.md#computing-resources) as well as [communicating resources](../Principles/metamodels.md#communication-architecture): 
* A ComputingResource is a generic representation for any type of computing device, such as a data center. 
* A SoftwareResource is a generic representation for any type of software entity, typically the implementation of a controller.
* A CommunicationMedia is a generic representation for any means of communication. The user indicates capacity and latency of this entity.

Lastly, the user connects CommunicationMedia between themselves, and ComputingResources to CommunicationMedia according to the situation they wish to represent.

## Allocating the CFA onto the CFRA

The functional architecture is allocated onto the physical architecture through the means of abstraction links between functions, such as controllers, and the software resources implementing those. More precisely, the user must allocate all the CentralController, ZoneController and LocalController onto SoftwareResources through a specialized link. The resulting concrete architecture of the CFA allocated onto a CRA is called CFRA. 

## Communication Hazard Creation

The communication hazards are optional, but they allow to represent scenarios of interest where some part of the power grid malfunctions. Several scenarios can be defined through the modeler, representing communication hazards for the elements of the CRA. All elements of the CRA can be targeted by these hazards : Software resources, Computing resources, Communication Media, and the links between these elements. This allows to represent a vast range of real incidents : loss of messages during transit, computing device malfunction, software resource bugs… From a technical point of view, what can be modeled are the following scenarios :
* Loss of a controller, through a hazard affecting the software resource implementing it
* Loss of a controller *during a given period only*
* Loss of a communication link
* Loss of a communication link *during a given period only*
* **Partial** loss of a communication link (a fraction of the transmited messages is lost)
* **Partial** loss of a communication link (a fraction of the transmited messages is lost) *during a given period only*

Communication hazards are described via the selection of a component, the definition of a failure percentage and the period during which this failure occurs.

## [User Interface](../User-doc/Modeling-guidelines.md)
CybergridML allows to represent the concepts of the [metamodel](../Principles/metamodels.md), while following this workflow. 