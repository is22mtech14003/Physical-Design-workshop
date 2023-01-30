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
    
![Screenshot 2023-01-30 093304](https://user-images.githubusercontent.com/120499567/215385694-df563b30-a7a6-468f-9568-344220b5f40b.png    
    
    
    
### After run routing
    

