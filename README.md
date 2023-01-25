# Physical Design RTL2GDS using OpenLane/SKY130 workshop
### This repository contains all the information studied and created during the [Advanced Physical Design](https://www.vlsisystemdesign.com/advanced-physical-design-using-openlane-sky130/) Using [OpenLANE / SKY130](https://openlane.readthedocs.io/en/latest/) workshop. It is primarily foucused on a complete RTL2GDS flow using the open-soucre flow named OpenLANE. [PICORV32A](https://github.com/YosysHQ/picorv32) RISC-V core design is used for the purpose
# Table of Contents
*
    + [RTL to GDSII Flow](#RTL-to-GDSII-Flow)
    + [Skywater 130 PDK](#skywater-130-PDK)
    + [OpenLANE](#openLANE)
    + [List of all open source tool used](#List-of-all-open-source-tool-used)
    + [Setting up enviroment](setting-up-enviroment)
    * [Day 1](#day-1)
    
    
    





## RTL to GDSII Flow
RTL to GDSII Flow refers to the all the steps involved in converting a logical Register Transfer Level(RTL) Design to a fabrication ready GDSII format. GDSII is a database file format which is an industry standard for data exchange of IC layout artwork. The RTL to GSDII flow consists of following steps:
- RTL Synthesis
- Static Timing Analysis(STA)
- Design for Testability(DFT)
- FloorplanningRouting
- Placement
- Clock Tree Synthesis(CTS)
- Routing
- GDSII Streaming
### All the steps are further discussed in details in the repository.

## Skywater 130 PDK
#### It is a Open source PDK (Process Design Kit) which is released by the collabration of Google and SkyWater Technologies foundary. Currently this technology has a target node of 130 nm. It is open to everyone and can be accessed at [SkyWater Open Source PDK](https://github.com/google/skywater-pdk). This PDK is extremely flexible as it provides many optional featurs as standard features. Hence it povide designers with wide range of design choice.
## OpenLANE
It is an open-source VLSI flow created using open source tools. Basically it is collection of various scripts which invoke and execute these tools in right sequence, modifies inputs and outputs and gives an organised results.

## List of all open source tool used
|Name of Tool|Application / Usage|
|:---:|:---:|
|Yosys|Synthesis of RTL Design|
|ABC|Mapping of Netlist|
|OpenSTA|Static Timing Analysis|
|OpenROAD|Floorplanning, Placement, CTS, Optimization, Routing|
|TritonRoute|Detailed Routing|
|Magic VLSI|Layout Tool|
|NGSPICE|SPICE Extraction and Simulation|
SPEF_EXTRACTOR|Generation of SPEF file from DEF file|

# Setting up enviroment
The above list of tools shows that, many different tools are required for various tasks in Physical VLSI Design. Each tool in itself have number of system requirements and require various supporting tools to be installed. Installing each tool one-by-one seems in-efficient. This is made easy by some custom scripts that setup the required tools and environment for them in just a few easy steps. To install all the required tools, one can refer to the below mentioned repositories:
- [VSD Flow](https://github.com/kunalg123/vsdflow) - Installs Yosys, Magic, OpenTimer, OpenSTA and some other supporting tools
- [OpenLANE Build Script](https://github.com/nickson-jose/openlane_build_script) Install all required OpenROAD and some supporting tools

# Day 1
## Inception of open-source EDA, OpenLANE and Sky130 PDK

### Basic IC Design Terminologies
During the Physical Designing, one will come across multiple terminologies that are frequently used. Some of them are mentioned below:

- Package: 
It is a case that surrounds the circuit material to protect it from physical damage or corrosion and allow mounting of the electrical contacts connecting it to the printed circuit board (PCB). The below snippet shows an IC with 48 pins and Quad Flat No-Leads(QFN) package.
- Die:
A die is a small block of semiconducting material on which a given functional circuit is fabricated.
- Core:
It is the actual area of the IC where the logic resides.
- Pads:
These are the interfaces between the internal signals of a chip and the external pins


