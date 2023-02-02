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
The `above list of tools` shows that, many different tools are required for various tasks in Physical VLSI Design. Each tool in itself have number of system requirements and require various supporting tools to be installed. Installing each tool one-by-one seems in-efficient. This is made easy by some custom scripts that setup the required tools and environment for them in just a few easy steps. To install all the required tools, one can refer to the below mentioned repositories:
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
    
### Netlist
Netlist basically defined the conectivity between all the components
    
 ### core
    A core is the section of the chip where the fundamental logic of the desine is placed.
 ### Die 
    which consist of more is small semiconducotor matrial specimen on which the fundamental circuit is fabricated 
![Screenshot 2023-01-26 155841](https://user-images.githubusercontent.com/120499567/214899864-ce3e3171-acb0-45b7-b137-806094cb5751.png)
    
![Screenshot 2023-01-26 160649](https://user-images.githubusercontent.com/120499567/214900208-ad9813d0-7b7b-4639-8943-d2a8f424d95d.png)

![Screenshot 2023-01-26 180600](https://user-images.githubusercontent.com/120499567/214900658-06b3f66a-f8d2-40ac-8984-5949c73e40a9.png)
    
|![Screenshot 2023-01-26 181140](https://user-images.githubusercontent.com/120499567/214901394-78af434b-3206-4937-8679-ae3dda7aedbd.png)
|![Screenshot 2023-01-26 184517](https://user-images.githubusercontent.com/120499567/214901979-d887b9ba-3fc8-40b7-8ef3-576defb2304a.png)
|
|:---:|:---:|
### Utilization Factor and Aspect Ratio
Utilization Factor is ratio of the area of core used by standard cells to the total core area. The utilization factor is generally kept in the range of 0.5-0.7 i.e. 50% - 60%. Maintaining a proper utilization factor facilitates placement and routing optimization.
    
### Power Planning
    
Power planning is a step in which power grid network is created to distribute power to each part of the design equally. This step deals with the unwanted voltage drop and ground bounce. Steady state IR Drop is caused by the resistance of the metal wires comprising the power distribution network. By reducing the voltage difference between local power and ground, steady-state IR Drop reduces both the speed and noise immunity of the local cells and macros.
    
### Pin Placement
    
Pin placement is a important part of floorplanning as the timing delays and number of buffers required is dependent on the position of the pin. There are multiple pin placement option available such as equidistant placement, high-density placemen
    
### Decoupling Capacitors to the pre placed cells
- The power lines can have some RLC component causing the voltage to drop at the node where it enters the Blocks or the ground of the cell can be at a higher potential than ideally 0V
    
- When this happens, there is a chance such that the logic transitions are not to the upper or lower noise margins but to the forbidden state causing the circuit to misbehave
    
- This is prevented by adding a capacitor in parallel with the power and ground node of the block such that the capacitor decouples the block from the power source whenever there is a logic transition
    
![Screenshot 2023-01-26 202139](https://user-images.githubusercontent.com/120499567/214905535-ad5fb7bc-e16c-4f50-a0ab-a3e9b9f59cad.png)
    
    
### Floorplan using OpenLANE

Floorplanning in OpenLANE is done using the following command.
        
- run_floorplane
    
Successful floorplanning gives a def file as output. This file contains the die area and placement of standard cells
    
![Screenshot 2023-01-27 011011](https://user-images.githubusercontent.com/120499567/215328132-ddcc13a5-6664-4255-aa07-c74eb7b42003.png)
    
##  Review Floorplan Layout in Magic
    
Magic Layout Tool is used for visualizing the layout after floorplan. In order to view floorplan in Magic, following three files are required: 1. Technology File (sky130A.tech) 2. Merged LEF file (merged.lef) 3. DEF File
    
    
![Screenshot 2023-01-27 015424](https://user-images.githubusercontent.com/120499567/215328468-ce3de7a1-274c-4193-8d11-2d29dfc9109d.png)

![Screenshot 2023-01-27 015734](https://user-images.githubusercontent.com/120499567/215328507-3b6f4a51-8c3e-46d6-9e72-43299c6953fd.png)

 ## Placement
    
### Placement and Optimization
The next step after floorplanning is placement. Placement determines location of each of the components on the die. Placement does not just place the standard cells available in the synthesized netlist. It also optimizes the design, thereby removing any timing violations created due to the relative placement on die.
    
### Placement using OpenLANE
    
Placement in OpenLANE is done using the following command.
    
- run_placement
    
## The DEF file created during floorplan is used as an input to placement. Placement in OpenLANE occurs in two stages:
    
- Global Placement
- Detailed Placement
    
 ## Placement is carried out as an iterative process till the value of overflow converges to 0.
 ![Screenshot 2023-01-27 211738](https://user-images.githubusercontent.com/120499567/215329020-a74c5135-33bc-4df3-92e8-9485c11cf141.png)

 ![Screenshot 2023-01-27 212034](https://user-images.githubusercontent.com/120499567/215329079-6862b031-a844-4b96-9f40-d4632c73b0a7.png)
   
## Cell Design and Characterization Flows    
    
### Cell Design Flow
In a border view Cell Design flow is are the stages or steps involved in the entire design of a standard cell. The figure below shows the input, output and design steps involved in cell design
    
![Screenshot 2023-01-29 185923](https://user-images.githubusercontent.com/120499567/215329469-e53d1c41-5071-4f8b-aefc-b5931bf109c1.png)   
    
##  Characterization Flow
    
 There are few problems of Standard Cells in polygon level format (GDSII). Some of them are:
- Extraction of functionality is complicated and unnecessary as it is known
- Functional/Delay simulation takes way too long
- Power extraction for a whole chip takes too long
- Automatic detection of timing constraints (e.g. Setup time) is difficult
    
A solution to above problems is Cell Characterization. It is a simple model for delay, function, constraints and power on cell/gate level. The Characterization Flow consists of the following stages:
    
1. Netlist Extraction - Transistors, resistances and capacitances are extracted with special tools and saved as SPICE netlist (or similar)
2. Specification of parameters - Library-wide parameters have to be specified: e.g. max Transition time
3. Model selection and specification - The used models determine the required data
4. Measurement - The cells are simulated with a SPICE-like tool to obtain the required data
5. Model Generation - The obtained data is fed into the models
6. Verification - Different checks are performed to ensure the correctness of the characterization
    
    
#  Day 3 - Design library cell using Magic Layout and ngspice characterization
    
Every Design is represented by equivalent cell design. All the standard cell designs are available in the Cell Library. A fully custom cell design that meets all rules can be added to the library. To begin with, a CMOS Inverter is designed in Magic Layout Tool and analysis is carried out using NGSPICE tool.    

## CMOS Inverter Design using Magic
    
The inverter design is done using Magic Layout Tool. It takes the technology file as an input (sky130A.tech in this case). Magic tool provide a very easy to use interface to design various layers of the layout. It also has an in-built DRC check fetaure. The snippet below shows a layout for CMOS Inverter with and without design rule violations.
    
![Screenshot 2023-01-28 130819](https://user-images.githubusercontent.com/120499567/215330221-465d5121-8a27-4c77-82f8-15e25736b483.png)

![Screenshot 2023-01-28 175141](https://user-images.githubusercontent.com/120499567/215330254-251235ee-cc05-4ede-be94-af3a2fd69e9b.png)

    
## Extract SPICE Netlist from Standard Cell Layout
    
 To simulate and verify the functionality of the standard cell layout designed, there is a need of SPICE netlist of a given layout. To mention in brief, "Simulation Program with Integrated Circuit Emphasis (SPICE)" is an industry standard design language for electronic circuitry. SPICE model very closely models the actual circuit behavior. Extraction of SPICE model for a given layout is done in two stages.
    
1.  Extract the circuit from the layout design.
-  extract all
    
2.  Convert the extracted circuit to SPICE model.
- ext2spice cthresh 0 rthresh 0
ext2spice

The extracted SPICE model like the first snippet shown below. Some modification are done to the SPICE netlist for the purpose of simulations, which is shown in the second snippet below.
    
![Screenshot 2023-01-28 182906](https://user-images.githubusercontent.com/120499567/215330518-452f9a0e-4ed7-4d5f-9ed4-b2215b092ab0.png)

![Screenshot 2023-01-28 184603](https://user-images.githubusercontent.com/120499567/215330633-8583053f-c131-47a4-b438-d6189b25a0de.png)
    
## Transient Analysis using NGSPICE
    
The SPICE netlist generated in previous step is simulated using the NGSPICE tool. NGSPICE is an open-source mixed-level/mixed-signal electronic spice circuit simulator. The command used to invoke NGSPICE is shown below.
    
- ngspice <name-of-SPICE-netlist-file>
    
Following command is used to plot waveform in ngspice tool.
    
- ngspice 1 -> plot Y vs time A
![Screenshot 2023-01-28 212826](https://user-images.githubusercontent.com/120499567/215330755-60cb45e8-2360-4046-b886-d51e54c5aa5e.png)

Below figure shows the waveform of Inverter output vs input w.r.t. time. Many timing parameters like rise time delay, fall time delay, propagation delay are calculated using this waveform.

![Screenshot 2023-01-28 224427](https://user-images.githubusercontent.com/120499567/215330811-927c4076-a868-4eae-8936-c3197adccd96.png)


        
# Day 4 - Pre-layout timing analysis and importance of good clock tree    
    
In order to use a design of standard cell layout in OpenLANE RTL2GDS flow, it is converted to a standard cell LEF. LEF stands for Library Exchange Format. The entire design has to be analyzed for any timing violations after addition or change in the design  
    
## Magic Layout to Standard Cell LEF
    
Before creating the LEF file we require some details about the layers in the designs. This details are available in a tracks.info as shown below. It gives information about the offset and pitch of a track in a given layer both in horizontal and vertical direction. The track information is given in below mentioned format.
    
- <layer-name> <X-or-Y> <track-offset> <track-pitch>
![Screenshot 2023-01-28 235208](https://user-images.githubusercontent.com/120499567/215331047-67c765e3-89c9-449d-9eb1-7a50b70c2319.png)
    
To create a standard cell LEF from an existing layout, some important aspects need to be taken into consideration. 
    
1. The height of cell be appropriate, so that the VPWR and VGND properly fall on the power distribution network
2. The width of cell should be an odd multiple of the minimum permissible grid size.
3. The input and ouptut of the cell fall on intersection of the vertical and horizontal grid line.
    
    
![Screenshot 2023-01-29 001931](https://user-images.githubusercontent.com/120499567/215331167-47906834-07b4-4ce6-8dbd-4b4a8eee87d1.png)
    
## Timing Analysis using OpenSTA
    
 The Static Timing Analysis(STA) of the design is carried out using the OpenSTA tool. The analysis can be done in to different ways.
    
- Inside OpenLANE flow: This is by invoking openroad command inside the OpenLANE flow. In the openroad OpenSTA is invoked. 
- Outside OpenLANE flow: This is done by directly invoking OpenSTA in the command line. This requires extra configuration to be done to specific the verilog file, constraints, clcok period and other required parameters.
    
OpenSTA is invoked using the below mentioned command.    
    
- sta <conf-file-if-required>    
    
The above command gives an Timing Analysis Report which contains:
    
1. Hold Time Slack
2. Setup Time Slack
3. Total Negative Slack (= 0.00, if no negative slack)
4. Worst Negative Slack (= 0.00, if no negative slack)
    
![Screenshot 2023-01-29 004723](https://user-images.githubusercontent.com/120499567/215331746-104f02f6-6939-47f5-981a-c034f7cbbae4.png)
![Screenshot 2023-01-29 032355](https://user-images.githubusercontent.com/120499567/215331789-6b2de745-6797-4a11-a505-26e615724b66.png)
    
![Screenshot 2023-01-29 225342](https://user-images.githubusercontent.com/120499567/215345922-5ff05c86-fd22-4897-8b4d-e72a910fe9e5.png)
## Floorplane
    
![Screenshot 2023-01-29 231559](https://user-images.githubusercontent.com/120499567/215345995-a85f3373-1e85-4d27-935f-584c1034c484.png)
![Screenshot 2023-01-29 232144](https://user-images.githubusercontent.com/120499567/215346075-82d6f814-179d-4650-8136-796d6e577c62.png)
    
### placement
global placement
![Screenshot 2023-01-29 232144](https://user-images.githubusercontent.com/120499567/215346423-a09d37e7-3624-46a1-ab66-f9b046143515.png)
    
Detailed placement
    
   
![Screenshot 2023-01-29 233727](https://user-images.githubusercontent.com/120499567/215346501-46276e0a-f321-4858-8719-7368cc9780e3.png)
    
 ```
 magic -T /home/kunalg123/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![Screenshot 2023-01-30 014139](https://user-images.githubusercontent.com/120499567/215353627-873e355c-b53f-44d8-a4ba-e05c3e867b27.png)
![image](https://user-images.githubusercontent.com/120499567/215354149-2ab50b76-db68-46b8-ab45-391baf39ca22.png)
![Screenshot 2023-01-30 020856](https://user-images.githubusercontent.com/120499567/215354600-c850fe3c-5bbb-4623-82db-afc0308223fb.png)


    
 ### decupling capacitor
    
- tap_decap_or
    
![Screenshot 2023-01-29 234051](https://user-images.githubusercontent.com/120499567/215346716-91b400df-5f0a-45b9-9058-420e32e65076.png)
    
### detaieled placement
- detailed_placement
![Screenshot 2023-01-29 234051](https://user-images.githubusercontent.com/120499567/215350611-177a40e2-97ab-46b9-8766-b5a4159eb1bb.png)
    
    
    
### Generate power distribution network
    
- gen_pdn
    
![Screenshot 2023-01-30 005351](https://user-images.githubusercontent.com/120499567/215350805-69c08bfc-988b-4ce8-8f94-0b8f228eba41.png)
   
    
    
    
## Clock Tree Synthesis using TritonCTS
    
Clock Tree Synthesis(CTS) is a process which |makes| sure that the clock gets distributed evenly to all sequential elements in a design. The goal of CTS is to minimize the clock latency and skew. There are several CTS techniques like:
    
1. H - Tree
2. X - Tree
3. Fish bone
    
In OpenLANE, **clock tree synthesis** is *carried* out using TritonCTS tool. CTS should always be done after the floorplanning and placement as the CTS is carried out on a placement.def file that is created during placement stage.  
 
 The command used for running CTS in OpenLANE is given below.
    
- run_cts
    
![Screenshot 2023-01-30 043138](https://user-images.githubusercontent.com/120499567/215360639-0f623b97-8666-4616-8187-994ef1a15d5d.png)
    
    
### Openroad

- This will open the open road. Our objective to do the analysis of the entire circut where clock tree has been build now. Now we will open OpenSTA here. For timing alnalysis.
    
![Screenshot 2023-01-30 093439](https://user-images.githubusercontent.com/120499567/215385296-5a7f95c5-9ffe-41f9-88dc-0110265582e0.png)

Setup Slack constrains are met
    
![Screenshot 2023-01-30 093304](https://user-images.githubusercontent.com/120499567/215481912-8f0dfd92-034d-4dc8-bb4e-c019e8571efb.png)


    
# Day 5
## What is routing
[Routing is the process of creating physical connections based on logical conectivity](http://vlsibegin.blogspot.com/p/routing.html)    
or best possible conection between source to target
it should be very less zig zag path and it should be L or Z saphe
    
- Global route is done by fast route and detailed route is done by triton route. 
- Fast route is folowed by detailed route
- intera layer routing means within the router
    
### Maze Routing:
One simple routing algorithm is Maze Routing or Lee's routing:
    
The Maze Routing algorithm is an algorithm to find connections between the terminals and the Lee algorithm is one possible solution for Maze routing problems. Lee algorithm searches for the shortest path between two terminals and guarantees to find a route between two points if the connection exists.    
    
- The shortest path is one that follows a steady increment of one (1-to-9 on the example below). There might be multiple path like this but the best path that the tool will choose is one with less bends. The route should not be diagonal and must not overlap an obstruction such as macros.   
    
- This algorithm however has high run time and consume a lot of memory thus more optimized routing algorithm is preferred (but the principles stays the same where route with shortest path and less bends is preferred)
    
It takes more time because first create the maze and then do leveling and then make the connection from source to target
    
![Screenshot 2023-01-30 214501](https://user-images.githubusercontent.com/120499567/215531941-57393182-b53e-4538-805d-55c4b0e1ea9c.png)

## [DRC](https://www.synopsys.com/glossary/what-is-design-rule-checking.html#:~:text=Design%20Rule%20Checking%20(DRC)%20verifies,result%20in%20a%20chip%20failure.)
    
DRC cleaning is the next step after routing. DRC cleaning is done to ensure the routes can be fabricated and printed in silicon faithfully. Most DRC is due to the constraints of the photolitographic machine for chip fabrication where the wavelength of light used is limited. There are thousands of DRC and some DRC are:
    
    
1. Minimum wire width
2. Minimum wire pitch (center to center spacing)
3. Minimum wire spacing (edge to edge spacing)
4. Signal short = this can be solved my moving the route to next layer using vias. This results in more DRC (Via width, Via Spacing, etc.). Higher metal layer must be wider than lower metal layer and this is another DRC.
    
## [Power Distribution Network](https://vlsi-backend-adventure.com/powerplan.html#:~:text=Power%20Plan,also%20includes%20Power%20Via%20insertion):
    
This is just a review on PDN. The power and ground rails has a pitch of 2.72um thus the reason why the customized inverter cell has a height of 2.72 or else the power and ground rails will not be able to power up the cell. Looking at the LEF file runs/[date]/tmp/merged.nom.lef, you will notice that all cells are of height 2.72um and only width differs.
    
As shown below, power and ground flows from power/ground pads -> power/ground ring-> power/ground straps -

![Screenshot 2023-01-30 210442](https://user-images.githubusercontent.com/120499567/215533149-875e2638-7698-455b-a220-5ae23b8c8e8b.png)

    
## Routing Stage and TritonRoute:
OpenLane routing stage consists of two stages:
    
- Global Routing - Form routing guides that can route all the nets. The tool used is FastRoute
- Detailed Routing - Uses the global routing's guide to actually connect the pins with least amount of wire and bends. The tool used is TritonRoute
    
 ## Triton Route
- Performs detailed routing and honors the pre-processed route guides (made by global route) and uses MILP based (Mixed Integer Linear Programming algorithm) panel routing scheme(uses panel as the grid guide for routing) with intra-layer parallel routing (routing happens simultaneously in a single layer) and inter-layer sequential layer (routing starts from bottom metal layer to top metal layer sequentially and not simultaneously). 
    
- Honors preferred direction of a layer. Metal layer direction is alternating (metal layer direction is specified in the LEF file e.g. met1 Horizontal, met2 Vertical, etc.) to reduce overlapping wires between layer and reduce potential capacitance which can degrade the signal.
    
![Screenshot 2023-01-30 215408](https://user-images.githubusercontent.com/120499567/215534363-a54e9292-0ef7-48c4-b069-ea831cf964f5.png)

    
# Run PDN(Power Distribution Network)
    
## The command to load the previous files (basically whatever you have done).
    
cd work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a -tag 29-01_18-06
// if we include new configuration i.e., edit the config file then we have to do overwrite
prep -design picorv32a -tag 29-01_18-06 -overwrite 

// to check the last def file created i.e., last def
echo $::env(CURRENT_DEF)
    
## Routing Stage
    
We will now finally do the routing, simply run run_routing. This will do both global and detailed routing, this will take multiple optimization iterations until the DRC violation is reduced to zero. The zeroth iteration has 27426 violations and only at the 8th iteration was all violations solved. The whole routing took 1 hour and 10 mins in my Linux machine with 2 cores. A fun fact: the die area is just 584um by 595um but the total wirelength used for routing spans to 0.5m!!!
    
![routin1](https://user-images.githubusercontent.com/120499567/215535269-84fec0cb-151b-4fde-9359-b5a6b3efe575.png)

![routing](https://user-images.githubusercontent.com/120499567/215535431-78153588-805c-4def-94e0-207d3e84955d.png)
    
![Screenshot 2023-01-30 213510](https://user-images.githubusercontent.com/120499567/215535568-333ab1ea-48d0-4bcc-86e5-634e8d8d912f.png)

![Screenshot 2023-01-30 215739](https://user-images.githubusercontent.com/120499567/215535709-e6a77fa2-48dc-4407-9e7c-5a4b851710e9.png)
    
    
    
## Extraction of GRSII file
    
- Finally do run_magic in the openlane to generate gds file.
    
### Generated GDSII file picrrv32a.gds.png file    
    
![Screenshot 2023-01-30 214008](https://user-images.githubusercontent.com/120499567/215537188-5e15ab69-542b-42d2-b58f-11f5b5efc1b9.png)

### All commands to run in openlane
    
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a

echo $::env ([Varible]) // our case = SYNTH_STRATEGY
// change the STRATEGY

set ::env(SYNTH_STRATEGY) "DELAY 0"

run_synthesis
init_floorplan
place_io
global_placement_or
detailed_placement
tap_decap_or
detailed_placement
run_cts
gen_pdn
run_routing
run_magi
    
## References
    

    
    
    
    
## Acknowledgement
Finally, I would like to express my sincere gratitude to Kunal Ghosh{Co-founder of VLSI System Design (VSD) Corp. Pvt. Ltd.} and Nickson Jose, VLSI Engineer {ASoC Physical Design Engineer} for tremendous assistance in planning and presenting this workshop on Advanced-Physical-Design-using-OpenLane-SKY130. The workshop was excellent and well designed, this workshop taught me a lot of new things about the design of GDSII file from RTL using OpenLANE, open source tool.  
    
    
    
