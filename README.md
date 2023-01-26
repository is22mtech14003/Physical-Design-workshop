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

![Screenshot 2023-01-26 014347](https://user-images.githubusercontent.com/120499567/214679523-852431f1-af86-4b28-ab3c-8b4483347e5e.png)

## Introduction to RISC-V
RISC-V is a new ISA that's available under open, free and non-restrictive licences. RISC-V ISA delivers a new level of free, extensible software and hardware freedom on architecture.
- It is far simpler and smaller than other commercial ISAs available
- It avoids micro-architecture or technology dependent features.
- It has small standard base ISA and multiple standard extensions.
- It supports variable-length instruction encoding. A brief design for RISC-V core can be refered [here]()
- It has both 32-bit and 64-bit varients. It also support floating point instruction
### Software to Hardware
The flow shows how the high level language (at software end) gets converted to machine language (at hardware end) and then gets executed on the package.

### What happens when we run a program?
Suppose a C program needs to run on a hardware. So we nned to pass this C program to the hardware. So firstly the C program is compiled into assembly language (RISC-V assembly language program). Now this assmebly language is converted into the machine language program (basically 1's and 0's). Now this 1's and 0's are understanable by the hardware.

### How does an application run on a computer?
1. The application software enters the system software (major component of it are OS, Compiler and Assembler).
- The OS handles I/O operations, memories and many low level functions.
- hen the program passes to Compiler which changes the program to Assembly language (compiled into instructions depends upon the hardware).
- Now the instruction set goes to Assembler. Assembler converts the instruction set to machine language (binary numbers).
- The system software converts the apllication software into binary language.
- Now these binary numbers enter our chip layout and according the function is performed.

![Screenshot 2023-01-24 235105](https://user-images.githubusercontent.com/120499567/214681742-b6bc9b09-3d46-4210-a2ef-753ffaed6c64.png)

## SoC design and OpenLane

### Introduction to Digital design
For designing Digital ASIC ICs we require following components and some of it's opensource resources are also mentioned.
- RTL models (old IP's) {github.com, librecores.org, etc}
- EDA tool {OpenROAD, OpenLANE, etc}
- PDK Data {SKYWater 130}

In the workshop every component is used from sources which are open soucre. The following image gives an idea about each component as an open source resource.

![Screenshot 2023-01-26 015829](https://user-images.githubusercontent.com/120499567/214682842-b1c2f30a-ac99-4c40-88f3-ad3f56281a28.png)
### What is a PDK?
PDK stands for Process Design Kit, it is provided by foundaries and it consists of library or set of building blocks which are used to build ICs. Each component in the library is seperate building bolck and ae made following certain foundary rules.

PDKs acts as an inteface between the FABs and the designeers. PDKs have collection of files whcih are used to model a fabrication process for the EDA tools used to design an IC. PDK consists of tecnology node information, Process Design Rules (to verify DRC, LVC, PEX, etc), device model, I/O libraries, Standard cell libraries, macros files, lef files, etc..

Google along with SKYWater made the laters PDK opensource (130 nm node). The PDK only need data information for successful implementation.

### Environment Setup
The OpenLANE flow requires various open source tools as well as their supporting tools to be installed for the complete Physical design flow. Installing this tools one by one is tedious as well as one can get lost in the steps. Installation can be done easily using some set of scripts present in following repositories VSDFlow (for installing Yosys, OpenSTA, Magic, OpenTimer, netgent, etc) and OpenLANE Build Scripts.

## What is OpenLANE
[]OpenLANE](https://github.com/efabless/openlane)is an automated RTL to GDSII flow which includes various open-source components such as OpenROAD, Yosys, Magic, Fault, Netgen, SPEF-Extractor. It also facilitates to add custom design exploration and optimization scripts. The detailed diagram of the OpenLANE architecture is shown below:

![Screenshot 2023-01-26 020837](https://user-images.githubusercontent.com/120499567/214685048-4114d72c-5900-4dcb-b6bb-2e4accd612fa.png)
OpenLANE flow consists of several stages. By default all flow steps are run in sequence. Each stage may consist of multiple sub-stages. OpenLANE can also be run interactively as shown here.

1. Synthesis

- yosys - Performs RTL synthesis
- abc - Performs technology mapping
- OpenSTA - Pefroms static timing analysis on the resulting netlist to generate timing reports

2. Floorplan and PDN

- init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
- ioplacer - Places the macro input and output ports
- pdn - Generates the power distribution network
- tapcell - Inserts welltap and decap cells in the floorplan

3. Placement

- RePLace - Performs global placement
- Resizer - Performs optional optimizations on the design
- OpenPhySyn - Performs timing optimizations on the design
- OpenDP - Perfroms detailed placement to legalize the globally placed components

4. CTS
- TritonCTS - Synthesizes the clock distribution network (the clock tree)
5. Routing
- FastRoute - Performs global routing to generate a guide file for the detailed routeg
- TritonRoute - Performs detailed routing
- SPEF-Extractor - Performs SPEF extraction

6. GDSII Generation
- Magic - Streams out the final GDSII layout file from the routed def

7. Checks
- Magic - Performs DRC Checks & Antenna Checks
- Netgen - Performs LVS Checks
# Open-Source EDA Tools
### OpenLANE Initialization
For invoking OpenLANE in Linux Ubuntu, we should first run the docker everytime we use OpenLANE. This is done by using the following script:
![Screenshot 2023-01-26 124804](https://user-images.githubusercontent.com/120499567/214778306-ddf22299-1322-43f8-87d2-4628aea74724.png)
A custom shell script or commands can be generated to make the task simpler.
- To invoke OpenLANE run the ./flow.tcl script.
- OpenLANE supports two modes of operation: interactive and autonomous.
- To use interactive mode use -interactive flag with ./flow.tcl
![comand line](https://user-images.githubusercontent.com/120499567/214778912-9e6e6db0-2dc9-43b9-8c6e-4750353beedc.png)

![comand line2](https://user-images.githubusercontent.com/120499567/214796942-4dec9fc6-716d-4bf9-a22f-b31511929017.png)
![openlane](https://user-images.githubusercontent.com/120499567/214797582-7c8d2d86-73c8-43db-a997-e6d8e52b2b78.png)

### Design Preparation
The first step after invoking OpenLANE is to import the openlane package of required version. This is done using following command. Here 0.9 is the required version of OpenLANE.
package require openlane 0.9

The next step is to prepare our design for the OpenLANE flow. This is done using following command:

prep -design <design-name>
    Some additional flags that can be used while preparation are
    
    -tag <name-for-current-run> - All the files generated during the flow will be stored in a directory named <name-for-current-run>
-overwrite - If a directory name mentioned in -tag already exists, it will be overwritten.
    
    During the design preparation the technology LEF and cell LEF files are merged together to obtain a merged.lef file. The LEF file contains information like the layer information, set of design rules, information about each standard cell which is required for place and route.
    
    ### clock
     ![clock verilog file](https://user-images.githubusercontent.com/120499567/214799858-872faf0a-ae30-4e82-b302-bf91b50e5e83.png)

    ![clock](https://user-images.githubusercontent.com/120499567/214800028-43f9832e-246c-46e6-b07c-5bee64f4cd32.png)
    
![less opensta_main timing rpt](https://user-images.githubusercontent.com/120499567/214800475-fe968a0d-e558-485d-a239-e7785d280a27.png)
    
![less yosys_4 stat rpt](https://user-images.githubusercontent.com/120499567/214800629-58672672-f4de-493e-88c4-8ca797897072.png)
    
![metal layer](https://user-images.githubusercontent.com/120499567/214800761-6300c486-7a75-4e6e-b34e-215e316c39fe.png)
    
## Design Synthesis and Results
    The first step in OpenLANE flow is RTL Synthesis of the design loaded. This is done using the following command.
    run_synthesis
    
![Screenshot 2023-01-26 123533](https://user-images.githubusercontent.com/120499567/214801711-12b5dc49-d439-40ca-8f00-7b049d91c782.png)

![Screenshot 2023-01-26 123639](https://user-images.githubusercontent.com/120499567/214801842-73da5e44-c8ca-4caa-9f9d-96b69da21aeb.png)
   
 ## flop ratio calculation
    
 ![IMG20230126150238](https://user-images.githubusercontent.com/120499567/214803138-96810024-3747-42a3-9c20-4f11de769c59.jpg)
    
    
 # Day 2 Good floorplan vs bad floorplan and introduction to library cells
    
 ### Chip Floorplanning
Chip Floorplanning is the arrangement of logical block, library cells, pins on silicon chip. It makes sure that every module has been assigned an appropriate area and aspect ratio, every pin of the module has connection with other modules or periphery of the chip and modules are arranged in a way such that it consumes lesser area on a chip
    
    

    
    
    
    


