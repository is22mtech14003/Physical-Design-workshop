# Physical Design RTL2GDS using OpenLane/SKY130 workshop
### This repository contains all the information studied and created during the [Advanced Physical Design](https://www.vlsisystemdesign.com/advanced-physical-design-using-openlane-sky130/) Using [OpenLANE / SKY130](https://openlane.readthedocs.io/en/latest/) workshop. It is primarily foucused on a complete RTL2GDS flow using the open-soucre flow named OpenLANE. [PICORV32A](https://github.com/YosysHQ/picorv32) RISC-V core design is used for the purpose
# Table of Contents
*
    + [RTL to GDSII Flow](#RTL-to-GDSII-Flow)
    + [skywater 130 PDK](#skywater-130-PDK)
    + [openLANE](#openLANE)
    + [List of all open source tool used](#List-of-all-open-source-tool-used)
    + [setting up enviroment](setting-up-enviroment)
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

## skywater 130 PDK
#### It is a Open source PDK (Process Design Kit) which is released by the collabration of Google and SkyWater Technologies foundary. Currently this technology has a target node of 130 nm. It is open to everyone and can be accessed at [SkyWater Open Source PDK](https://github.com/google/skywater-pdk). This PDK is extremely flexible as it provides many optional featurs as standard features. Hence it povide designers with wide range of design choice.
## openLANE
It is an open-source VLSI flow created using open source tools. Basically it is collection of various scripts which invoke and execute these tools in right sequence, modifies inputs and outputs and gives an organised results.

## List of all open source tool used
|Name of Tool|Application / Usage|

