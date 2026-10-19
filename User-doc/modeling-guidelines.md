# CyberGridML Project Creation

CyberGridML is based on the **SysON** tool. To create a new project, the user selects the **CyberGridML** template, as illustrated below.

![CybergridML template](../icons/cybergridml_template.png)
*Main page project*

![CyberGridML new project](../icons/new-project.png)
*Creation of a new project*

![CyberGridML project views](../icons/project-views.png)
*Project views*

Each component has properties whose values can be configured by the user. The **Details** main tab , located on the right-hand side of the window, displays the **CyberGridML** tab that describes each element property (name, documentation, type, and other properties) of the selected element.

Property values can be edited directly from this panel.

![Details tab](../icons/properties.png)

*CyberGridML tab*


---

# 1. CFA view Creation

A dedicated diagram allows users to create and display the **CFA**.

As a reminder, the user must first create the following mandatory elements:

- **MainGrid**
- **CentralController**

The MainGrid represents the electrical grid as a whole, and the CentralController is the component representing the control at the global level. 
To model this, first the user creates the MainGrid, and then they can create the CentralController component and link it to the MainGrid.

![Main Grid Controller](../icons/Maingrid_centralcontroller.png)

*CentralController in CFA*


Additional control elements, such as zonal controllers, can then be created as needed via pop-up menus.

![CFA elements are added to the view using pop-up context menus](../icons/palette_CFA.png)
*CFA elements are added to the view using pop-up context menus*

Zones and Substations are created in the MainGrid through a pop-up menu.

 ![Zone and Substation are added to the view using pop-up from MainGrid ](../icons/palette_MG.png)
*Zone and Substation are added to the view using pop-up from MainGrid*

Highlighting the creation of a Substation in maingrid.

![Substation in Maingrid](../icons/Maingrid_substation.png)

*Substation in Maingrid*

Highlighting the creation of a zone in maingrid.

![Zone in Maingrid](../icons/Maingrid_zone.png)

*Zone in Maingrid*

The user must specify the structure to which each controller is associated. 

Link a zone to a ZonalController via the Control Link.

![Zone-ZonalController Link](../icons/Zone_ZonalController.png)

*Zone-ZonalController Link*

Once all controllers have been defined, the CFA is complete.


---

# 2. CRA view Creation

A dedicated diagram allows users to create and display the communication and computing resources of the **CRA**.

The following elements can be created:

- **CommunicationMedia** (displayed in blue)
- **ComputingResource** (displayed in green)
- **RedundancyCluster** (displayed in gray)
- **SoftwareResource** (displayed in yellow)

The colors help users quickly identify the different types of element within the diagram.

![Menu showing which elements the user can create in a CRA](../icons/cra_palette.png)

*Menu showing which elements the user can create in a CRA*

Once these resources have been created, they must be linked together to describe the system architecture:

- Each **SoftwareResource** must be allocated to a **ComputingResource**.
- A **SoftwareResource** may optionally belong to a **RedundancyCluster**.
- Each **ComputingResource** must be connected to at least one **CommunicationMedia**, and may be connected to several.
- **CommunicationMedia** can be connected together to represent the communication network.

An example of a complete CRA for a SCADA system is illustrated below.

![CRA example for a modular SCADA system](../icons/cra_scada.png)

*CRA example for a modular SCADA system*

A feature allows to link in bulk a **communicationmedia** to numerous **computingresources**, using the **Connect in Bulk**

![Connect in Bulk pop-up](../icons/connect-Bulk.png)

*Connect in Bulk*

The user needs to select the **computingresources** they wish to connect to the communication media in the list of all the computing resources :

![Connect in Bulk computing resources selection](../icons/CR-Bulk.png)

*Select the **computingresources***

Afterwards, the links are all automatically created. 

![Connect in Bulk links creation](../icons/link-Bulk.png)

***communicationmedia** and **computingresources** link*

# 3. CFRA view Creation

A dedicated diagram allows users to create and display the links between **SoftwareResource** and **Controller** in the **CFRA**.

The following elements can be created:
- **Localcontroller** 
- **Centralcontroller** 

![Menu showing which elements the user can create in a CFRA](../icons/CFRA-palette.png)

*Menu showing which elements the user can create in a CFRA*

An example of a complete CFRA for a SCADA system is illustrated below.

![CFRA example for a modular SCADA system](../icons/CFRA-SCADA.png)

*CFRA example for a modular SCADA system*


# 4. Hazards Definition

Hazards are used to represent possible failures of some components. 
Hazards are represented via properties associated with CRA components. To define a hazard, the user must first select the target element, then apply a hazard to the selected element using the **Toggle Hazard** command. as illustrated below.

![Communicationmedia Hazard](../icons/hazard-selection.png)

*Communicationmedia hazard*

The **Toggle Hazard** command is also used to remove the hazard from the element.


To make hazard assignments easily identifiable, elements carrying a hazard are displayed in **red**, as illustrated below.

![DC1 Network shown in red after hazard application](../icons/hazard_marked_element.png)

*Communicationmedia shown in red after hazard application*

Communication hazards include the following properties:

- Description
- Justification
- Percentage of lost messages
- Hazard occurrence period

Once a hazard has been applied to an element, its properties become visible in the **Model Explorer**, as shown below.

![Hazard properties are added to Communicationmedia](../icons/hazard_properties.png)

*Hazard properties are added to Communicationmedia*

# 4. Import XIIDM file

**XIIDM** (eXtended Internal Interconnection Data Model) is a data format used to represent electrical power grid models. It can describe grid components such as buses, lines, generators, loads, transformers, and their electrical parameters.

![Example of XIIDM ](../icons/XIIDM.png)

*Example of XIIDM*

## XIIDM Import Feature

CyberGridML provides a feature that allows users to import the structural elements of the electrical grid from XIIDM files.
The imported data is used to automatically build the model by creating the corresponding elements and the CFA, CFRA et CRA diagrams.

This feature facilitates the integration of existing power grid models into CyberGridML and reduces the need to manually recreate grid components.

To import an XIIDM file, a MainGrid must first be created in the CFA. The import action is available as a drop-down menu from the MainGrid component.

![Import XIIDM ](../icons/XIIDM-from-MG.png)

*Import XIIDM*

The user can then select the XIIDM file to import.

 
![XIIDM file selection](../icons/XIIDM-import.png)

*XIIDM file selection*

After the import, the CFA view is automatically filled with imported CFA elements and additional control elements : substations, components of these substations and controllers for these elements. 

![CFA view after XIIDM import](../icons/CFA-import.png)

*CFA view after XIIDM import*

During the import, software resources are automatically created for each controller. After the import, the CFRA view is automatically filled with the information linking the controllers to the software resources implementing them.
![CFRA view after XIIDM import](../icons/CFRA-import.png)

*CFRA view after XIIDM import*

In addition to software resources, some computing resources are also created automatically : a computing resource is created for each substation and the software resources the controllers of the grid equipements for this substation are by default allocated to this computing resource. Computing resources for equipements typically outside of the grid operator control, such as generators, are also created. 

![CRA view after XIIDM import](../icons/CRA-import.png)

*CRA view after XIIDM import*


[← Back to the main documentation](../README.md)