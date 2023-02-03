# PNR-Labs
# Advance Physical Design using OpenLANE/Sky130
# Day 1 -Inception of open-source EDA, OpenLANE and sky130 PDK

	To perform the intruction, which are given externaly in computers, some hardware is there which convert our external instruction into understandable language of computers. Arduino consists of both a physical programmable circuit board (often referred to as a microcontroller) and a piece of software, or IDE (Integrated Development Environment) that runs on the computer, used to write and upload computer code to the physical board.Basically microcontroller is made from package, inside the package chip is there.Chip is made by pads, core, die and foundary IP's.

![image](https://user-images.githubusercontent.com/123365842/216225495-063556cb-8a79-46e5-a8b4-d3f11ed41031.png)

# Package

The package is a case that surrounds the circuit material to protect it from corrosion or physical damage and allow mounting of the electrical contacts connecting it to the printed circuit board (PCB).

![image](https://user-images.githubusercontent.com/123365842/216225639-e63b3f9c-b3ef-4de0-9ee2-cd49a5ec240c.png)

# Chip

Inside the Package, chip is available which contains, foundary IP's (for example, RISC-V Soc, PLL, ADC, DAC, SRAM, SPD), core (core contains AND, OR etc. all gates and digital logics), pads (through which input and output signals are communicates).

![image](https://user-images.githubusercontent.com/123365842/216225721-122f7b4d-dad5-4481-ab33-6680138ea959.png)

# What is RISC-V?

RISC-V, where five refers to the number of generations of RISC architecture that were developed at the University of California, Berkeley. RISC is an open standard instruction set architecture (ISA) based on established RISC principles. A number of companies are offering or have announced RISC-V hardware, open source operating systems with RISC-V support are available, and the instruction set is supported in several popular software toolchains.

The instruction set is designed for a wide range of uses. The base instruction set has a fixed length of 32-bit naturally aligned instructions, and the ISA supports variable length extensions where each instruction can be any number of 16-bit parcels in length. The instruction set specification defines 32-bit and 64-bit address space variants. The specification includes a description of a 128-bit flat address space variant, as an extrapolation of 32 and 64 bit variants, but the 128-bit ISA remains "not frozen" intentionally, because there is yet so little practical experience with such large memory systems.

# How software communicate with Hardware?

Between apps or software (in our mobilephones and computers or laptops) and Hardware (in our mobilephones and computers or laptops), One full channel is there, which contains O.S. (operating system), compiler and assembler. This channel proccesses the inputs from the apps and gives the outputs to the Hardware. And according to the output of assembler, the hardware will perform.

![image](https://user-images.githubusercontent.com/123365842/216226235-be875ef2-5c5a-489d-863c-7d9317a91abe.png)

So, this inputs goes throuth the system software cahnnel, where O.S. handles the input/output operations, it allocates the memory to for the codes and low level systems functions are there in O.S. Then program goes to the compiler, where program will compile and generate the HDL program.This HDL program is basically the sets of Instructions which can hardware is able to understand. The instructions are basically depends on what kind of hardware we are using. For example if we are using Mips processor then instruction formaate will be according to the Mips processor, if Hardware is RISC-V then the instruction formate will be according to the RISC-V and similerly for Arm and intel processors also.

This sets of instrusctions is now given to the Assembler. here according to the instruction set, assembler will generate the Binary code (contains only 0s and 1s). this binary code can be understandable for hardware. And according to this code, hardware will gives the output.

# How to design Digital ASIC?

To design Digital ASIC, few tools or things which are required from the day one. These are

    RTL Design

    EDA tools

    PDK data

# what is RTL design?

In digital circuit design, register-transfer level (RTL) is a design abstraction which models a synchronous digital circuit in terms of the flow of digital signals (data) between hardware registers, and the logical operations performed on those signals.for this designs many open sorces are available. like, librecores.org, opencores.org, github.com, etc...

# What is EDA tools?

The term Electronic Design Automation (EDA) refers to the tools that are used to design and verify integrated circuits (ICs), printed circuit boards (PCBs), and electronic systems, in general. many open sorces tools are available like Qflow, OpenROAD, OpenLANE, etc...
# What is PDK Data?

PDK is process design kit. It is interface between FAB and design. This data is collections of files like,

    process design rules: DRC, LVS, REX

    Digital standerd cell libreries

    i/o librerirs

    etc.....

which are used to model a fabrication process for the EDA tools used to design an ICs. for example, in 2020, google release the open source PDK for FOSS 130nm production with the skywater technology. But right now it is at cutting age of the 5 nm also. But in many applications, the advance node is not required, and the cost of advanced node is also high as compared to 130nm processors. This 130nm processors are also fast processor. for example,

    intel: P4EE @3.46 GHz(Q4'o4)

    sky130_OSU (single cycle RV32i CPU) pipeline version can achieve more than 1 GHz clock

# Simplified RTL to GDSII flow

![image](https://user-images.githubusercontent.com/123365842/216226635-9d4e88b5-fe21-4107-9fb6-3fb0b37704c9.png)

### Synthesis In the synthesis, the design RTL is translated to a circuit out from the SCL. The resultant circuit is describes in HDL and usualy refered to the gate level netlist. the gate level netlist is functionaly equivelent to the RTL. "standard Cells" have regular layouts.
Floor planning and Power planning

The main objective here is that to plan silicon area and distribute the power to the whole circuit. In the chip floor planning, the partition chip die between different system building blocks and place the i/o pads. In micro floor planning, we define the dimensions, pin locations, rows.

![image](https://user-images.githubusercontent.com/123365842/216226778-a2a0a56d-b229-4bd8-9137-1d5ea74a91d9.png)


In power planning, the power network is connstructed. tipically, the chip is power by multiple VDD and GND. so, total components are connected to power supply horizontaly and vertically by metal streps. here parallel structures are used to reduce the resistance. To address the electromagnetization problem, power distribution network uses upper metal leyers, which are thicker than lower metal layers. Hence have less resistance.

![image](https://user-images.githubusercontent.com/123365842/216226914-399c08f5-1382-48a9-baf5-98a57379459e.png)

# Placement

In this process, we place the gate level netlist on the floor planning rows, alligned with the sites. cells should be placed very closed to eachother to reduce the interconnnect delay. Usually placement is done in 2 steps:

    Global placement

    Detailed placement
    
![image](https://user-images.githubusercontent.com/123365842/216227008-996f1c81-d198-476d-9a4a-21090c5a5b98.png)

Global placement

Global placement is very first stage of the placement where cells are placed inside the core area for the first time looking at the timing and congestion. Global Placement aims at generating a rough placement solution that may violate some placement constraints while maintaining a global view of the whole Netlist.
Detailed placement

In detailed placements, we determined the exact route and layers for each netlist. the objective of detailed placement is valid routing, minimize area and meet timing constrains. Additional objective is minimum via and less power.
Clock tree synthesis (CTS)

Before routing the signals, we have to route the clock. In the process of clock synthesis, we have distribute the clock to the every sequential elements. for example flipflops, registers, ADC, DAC ete. basically clock netwroks looks likes a tree. where the clock source is roots and the clock elements are end leaves. Synthesization should be done in a manner that with minimum skew and in a good shape.To minimize the clock skew by using the low-skew global routing resources for clock signals.Microsemi devices provide various types of global routing resources that significantly reduce skew.Usually a tree is a H tree, X tree etc.

![image](https://user-images.githubusercontent.com/123365842/216227551-936be733-39d6-43cf-b6c2-3020d1175320.png)

# Routing

After routing the clock, the signal routing comes. Making physical connections between signal pins using metal layers are called Routing. Routing is the stage after CTS and optimization where exact paths for the interconnection of standard cells and macros and I/O pins are determined. There are two types of nets in VLSI systems that need special attention in routing:

    Clock nets

    Power/Ground nets

The sky130 PDK defines the 6 routing leyers. the lowest leyer is called local interconnect layer (titanium nitride layer). Other five layers are alluminium layers.

![image](https://user-images.githubusercontent.com/123365842/216227685-73e8c995-fb5f-4d8c-8dc4-6520ca7f0524.png)

In the proccess of routing, metal trackes forms a routing grids and these grids are huge. so, devide and conquer approach is use for routing. The two types of routing is used:

    Global routing: Generates the routing guides

    Detailed Routing: Uses the routing guides to implement the actual wiring

# Sign off

Once the routing is done, we can construct the final layout. This final layout will goes under the verification. Two types of verifications are there:

    Physical verification: Here design rule checking will done and it will check the final layout and owners layout

    Timing Verification: Here Static Timing Analysis will done

# Introduction to OPENLANE:

OPENLANE is an automated RTL to GDSII flow that is composed of several tools such as OpenROAD, Yosys, Magic, Netgen, Fault, CVC SPEF-Extractor, CU-GR, Klayout and a number of scripts used for design exploration and optimization. It is started as an Open-source flow for a true Open Source tape-out Experiment. striVe is a family of open everything SoCs:

    Open PDK

    Open EDA

    Open RTL

# striVe SoC Family

![image](https://user-images.githubusercontent.com/123365842/216228007-1de27c57-c048-4fe7-b5de-26c83ad232e1.png)

The main goal of OPENLANE is to produce a clean GDSII with no human intervation (no-human-in-the-loop). here the meaning of clean is that:

    No LVS violations

    No DRC Violations

    No timing Violations

OPENLANE is tuned for skyWter130nm open PDK. it can be used to harden Macros and chips.there is two mode of operation

    Autonomus : it is the push botton flow. with the push botton , it is a some time base design and due to this push botton, we get final GDSII

    interactive : here we can run comamds and steps one by one.

It has large number of design examples(43 designs with their best configurations).

# OpenLANE ASIC Flow (Detailed)

![image](https://user-images.githubusercontent.com/123365842/216228146-74544a37-7128-49f0-bd8e-e534e4da298a.png)

The design exploration utility is also used for regression testing(CI). we run OpenLANE on ~ 70 designs and compare the results to the best known ones.
# DFT(Design for Test)

it perform scan inserption, automatic test pattern generation, Test patterns compaction, Fault coverage, Fault simulation.

![image](https://user-images.githubusercontent.com/123365842/216228218-6f391beb-3ce3-4ea4-b70c-73ec500a5f03.png)

After that physical implementation is done by OpenROAD app. physical implementation involves the several steps:

    Floor/Power Planning

    End Decoupling Capacitors and Tap cells insertion

    Placements: Global and Detailed

    Post Placement Optimization

    Clock Tree synthesis (CTS)

    Routing: Global and Detailed

Every time the netlist is modified.(CTS modifies the netlist and Post Placements optimization also modifies the netlist).so for that verification must be performed. The LCE(yosys) is used to formally confirm that the function did not change after modifying the netlist. 
Dealing with antenna rules Violation: when a metal wire segment is fabricated, it can act as antenna.as an antenna, it collect charges which can demaged the transister gates during the fabrication.

![image](https://user-images.githubusercontent.com/123365842/216229009-a1fd97cc-e17d-4c0f-b86f-00543f1393a1.png)

To address this issue, we have to limit the lenght of the wire. usually this is the job of the router. If router fails to do this, then there are two solutions:

    Bridging attaches a higher layer intermediary

![image](https://user-images.githubusercontent.com/123365842/216229074-61538ad8-aabc-4408-9a5e-3ebb49a9fcd7.png)

image

    Add antenna diode cell to leak away charges.(Antenna diodes are provided by the SCL)

![image](https://user-images.githubusercontent.com/123365842/216229129-30d8d9a0-6bff-400d-b8ff-0ee318ba49dc.png)

With OpenLANE, we took a preventive approach. here we add fake antenna diode next to every cell input after placement. Then run the Antenna checker on the routed layout. If the checker reports a violation on cell input pin, replace the fake diode cell by a real one.

![image](https://user-images.githubusercontent.com/123365842/216229221-3fc98a37-4a65-45a2-9207-7140f1f09eee.png)

# Static Timing analysis(STA)

It involves the interconnect RC Extraction(DEF2SPEF) from the routed layout, followed by STA on OpenSTA(OpenROAD) tool. resulting report will shows the timing violations if any violations is there.

# Physical Verification (DRC and LVS)

Magic is used for design Rules checking and SPICE Extraction from Layout. Magic and Netgen are used for LVS.

# Open source EDA tools
# OpenLANE Directory Structure in detail
# cd command

cd means change directory. this command will help us to go inside the directory.

# ls command

ls means listing the directory. It is used to find the list of total details of directory.

# ls --ltr

This command will help to list the details in cronological order.

Working in Sky130_fd_sc_hd PDK varient. where, "sky130" is process name or node name."fd" is a foundary name (skyWater foundary)."sc" means standerd cell librery files and the last one "hd" stands for high density(basically one type of varient).

Sky130_fd_sc_hd varient contains many technology files like verilog, spice, techlef, meglef,mag,gds,cdl,lib,lef,etc. (techlef file contains the layer information).

# Design Preparation Step

when we enter in the OpenLANE, we have to use flow.tcl because as a name says, it will goes with the flow using the script. And by using interactive switch, we will do step by step process. without interactive switch, it will run complete flow from RTL to GDSII. Now OpenLANE is open and we can see that prompt will change now. 

Write the Command is

$ cd Desktop/work/tools/openlane_workind_dir/openlane
$docker
$./flow.tcl -interactive

So, show the following figure:

![image](https://user-images.githubusercontent.com/123365842/216230707-e1f97470-1673-4a0b-b8c1-cb16841a9247.png)

Now, here we are ready to execute the command.

Now, if we are going into the design folder in openlane, there are nearly 30-40 designs are already builted. Out of them we can open any of the design. for example, here we are opening the picorv32a.v design. In this design we can see many files are available. i.e., scr, config.tcl, etc. This config.tlc file contains every details about the design. for example, details about enrollment, clock period, clock period port etc.

![image](https://user-images.githubusercontent.com/123365842/216231741-d64401fb-a0c7-43a9-90aa-f55854831a86.png)

Here we can see that the time period is set to the 5.00 nsec. but is we see in the openlane sky130_fd_sc_hd folder, the period is set about 24 nsec. so it is not override to the main file. If it override then give first priority to the main folder. 

Write the command is 

%package require openlane 0.9
%prep –design picorv32a

![image](https://user-images.githubusercontent.com/123365842/216232349-c3cb30de-d18b-43f3-9165-c4bec71eefc3.png)

Now, in openlane, we are going to run the synthesis, but before synthesis, we have to prepare design setup stage. for that command is " prep -design picorv32a".

Write the command is
$ cd work/tools/openlane_working_dir/openlane/designs/picorv32a
Now we have to input all the packages which required to run the flow.Here we are ready to execute the command.

Write the command is

$less config.tcl

![image](https://user-images.githubusercontent.com/123365842/216235412-f185b66f-995c-42a5-980c-4ff599cafc12.png)

Write the command is
Less sky130A_sky130_fd_sc_hd_config.tcl
![image](https://user-images.githubusercontent.com/123365842/216235549-b0d17780-7070-4b2e-bff2-f0eb58b4016d.png)
so, here it is shown that preparation is completed.

Review after design preparation and run synthesis

After completing the preparation, in the picorv32a file, the run terictory is created. Inside the folder, Today's date is created. so in this terictory some folders are available which is required for openlane.

To Review is the write command
cd work/…../picorn32a/$ runs/01-02-09-25/
01-02-09-25 $ cd tmp 
tmp $ ls
$ cd tmp
temp $ cd ..
01-02-09-25$ ls –ltr
$ cd tmp
tmp $ less merged.lef

![image](https://user-images.githubusercontent.com/123365842/216235854-3e7a4c52-7284-4258-867c-7dbeb5ab6d83.png)


![image](https://user-images.githubusercontent.com/123365842/216236125-c6566ada-9f6d-42fe-ad2c-8d31f97145ce.png)

In the temp file, merged.lef file is available which was created in preparation time. if we open this merged.lef file, we get all the wire or layer level and cell level information.

Write the command is 

$Less merged.lef
![image](https://user-images.githubusercontent.com/123365842/216236247-85c52e12-ae12-48f2-bfb3-ca561d9f771f.png)

![image](https://user-images.githubusercontent.com/123365842/216236472-3cec7431-f914-4d36-b03b-6db87ec74b3b.png)
While, in the result folder is empty because till we have not run anything and in the report folder all the folders are there about synthesis, placement, floorplanning,cts,routing,magic,lvs.

![image](https://user-images.githubusercontent.com/123365842/216236562-26690ff7-c5c8-4115-860f-714287301cdf.png)
now here also one config.tcl file is available similar like design folder. But this config.tcl file contains all default parameter taken by the run.

![image](https://user-images.githubusercontent.com/123365842/216236623-4b3871fa-8146-4db9-9eec-5ef606b955b9.png)

when we make some change in the origional configuration and then we run, for example if we make a change in core utilization in the floorplanning and then we run the floorplanning, at this time in the congig.tcl file, the core utility will change and by cross checking it we can check that the modification is reflected in the exicution or not.

Now, cmds.log file takes all the record of the commands, what we have fab.

![image](https://user-images.githubusercontent.com/123365842/216236767-173120a5-fa1a-4a74-85e4-4816dbb43c7e.png)

To Openlane
%run_synthesis

![image](https://user-images.githubusercontent.com/123365842/216236818-ff26a1d2-95ad-4f5e-94e7-209d667b25a0.png)
So, the flop ratio = (number of flip flops)/(number of total cell).

So, the flop ratio is 10.84%.

Before run, we saw that the result folder is empty. but now, after running the synthesis, we can see that all the mapping have been done by ABC.

![image](https://user-images.githubusercontent.com/123365842/216236856-f51c765d-53c9-40f2-b47b-df452af8dc30.png)

And in the report, we can see when the actual synthesis has done. and the actual statistics synthesis report is showing below, which is same as what we have seen before.
![image](https://user-images.githubusercontent.com/123365842/216238201-a14f19b2-7d93-4a64-b621-c2f70e85b508.png)
From the data of synthesis, total number of counter D_flip-flops is 1613. and the number of cells is 14876.
![image](https://user-images.githubusercontent.com/123365842/216238254-6340238a-2bb8-4372-92d5-c79d8c174d2d.png)
So, the flop ratio = (number of flip flops)/(number of total cell).

So, the flop ratio is 10.84%.

Before run, we saw that the result folder is empty. but now, after running the synthesis, we can see that all the mapping have been done by ABC.

![image](https://user-images.githubusercontent.com/123365842/216238319-8d3b9867-a3f4-49f6-a42a-6a98711037dd.png)

And in the report, we can see when the actual synthesis has done. and the actual statistics synthesis report is showing below, which is same as what we have seen before.

![image](https://user-images.githubusercontent.com/123365842/216238440-08ef691f-46f9-4f7c-aacf-d9901b10efe7.png)

# Advance Physical Design using OpenLANE/Sky130
# Day 2 -Good floorplanning Vs Bad floorplanning and introduction to library cells
# Chip floorplanning considerations
# Utilization factor and aspect ratio
# 1)defining the width and height of core and Die
![image](https://user-images.githubusercontent.com/123365842/216497139-9fc3bc28-bbfc-4007-91e8-51d3ecf0c315.png)
let's begin with netlist( Netlist describes the connectivity of an electronic designs). Considering a netlist with 2 flops and 2 gates.
![image](https://user-images.githubusercontent.com/123365842/216497239-eb25762f-2a40-4225-96b8-980b608af398.png)
lets giving the height and width of standerd cell is 1 unit. So, area of standerd cell is 1 square unit. And assuming the same area for the flip flops also.

Now lets calculate the area occupied by the netlist on a silicon wafer by arranging them together. The total area occupied by netlist in silicon wafer is 4 square units.
![image](https://user-images.githubusercontent.com/123365842/216497314-38be173d-8ddf-4b1b-b505-160c41fc5b57.png)

# what is the core and die?

A 'core' is the section of the chip where the fundamental logic of the design is placed.

A 'Die', which is consist of core, is small semiconductor material specimen on which the fundamental circuits is fabricated.

![image](https://user-images.githubusercontent.com/123365842/216497412-0b47e03c-5c58-40d6-a8ac-2c8730e70490.png)
If we put the 'arranged netlist' in the core, then whole core is occupied by netlist. that means utilization of core is 100%.
![image](https://user-images.githubusercontent.com/123365842/216497511-c54c2411-d246-425f-8f03-b8c3d234a3fa.png)

# Utilization factor

it is defined as, 'the area occupied by netlist' devided by the 'total area of core'.

so, in above case, the utilization factor is 1.

practically, we don't go with 100% uti;ization. practically utilization factor is about 50%-60% to add other extra cells (like buffer) in the core after netlist is placed.

# Aspect Ratio

it is defined as (height)/ (width). here in above example the aspect ratio is 1.
# Concept of pre-placed cells
# 2) Define locations of preplaced cells

to define the preplaced cells, let's take a combinational logic i.e., mux, multiplier, clock devider, etc. and assuming that the output of the circuit is huge and assuming that the circuit has some 100k gates. so let devides in two blocks of 50k gates.
![image](https://user-images.githubusercontent.com/123365842/216497694-8a8e2645-464d-4f72-989e-cb3d42eabdab.png)
This both blocks are implimented separatly. Now, extending the input and output pins from the both blocks. now, let's detached these box. we will black box the boxes and detached them. After black boxing, the upper portion is invisible from the top or invisible to the one , who is looking into the main netlist. now we make separate them out.
![image](https://user-images.githubusercontent.com/123365842/216497747-eaac9452-80c0-4de7-8301-6991645ee807.png)

This blocks are implemented in netlist once and then we can reuse it multiple time. Similarly, there are other modules or IPs also readily available.i.e.,memory, clock gating cell, comparater, mux. these all are part of the top level netlist.They recieve some signals, they perform some functions, they deliver the outputs but the functionality of the cell is implemented only once. That what we called as preplaced cells.

The arrangement of these ip's in a chip is refferd as floorplanning.These IP's have user-defined locations, and hence are placed in chip before automated placement and routing are called "preplacement cells".These cells are place din such fashion that, the placement and routing tool not touch the location of the cell.

![image](https://user-images.githubusercontent.com/123365842/216497877-04b33ae5-e97f-4092-975d-9bfd199c6b33.png)

Let consider memory as a preplaced cells as a block 'a', block 'b' and block 'c'. Memory of any device is implemented once and reused multiple times. these preplaced cells are located as per the design bacckground. the location of the cells are never touched.

# De-coupling capacitors
# 3) surround pre-placed cells with Decoupling capacitors

Let consider some circuit, which is part of the blocks which were defined above. When some gate (let consider AND gate) switched from 0 to 1 ot 1 to 0, considered amount of the switching current required because of small capacitance is available there. this capacitor should be completely charged to represent logic 1 and completly discharged to represent logic 0. the required amount of the charge is suplied from the Vdd and absorb from the Vss. during supplying the current, wire has some drop of voltage due to resistence and inductunce of the physical wire.

![image](https://user-images.githubusercontent.com/123365842/216498023-478e280e-d1ae-4800-98be-9e69fc9f1718.png)

So, due to this if ideal logic 1 = 1 volt then here practically it can be less then 1 volt i.e., 0.97 volts (Vdd'). So, for any signal to be considered as Logic '0' and '1' in the NM low and NM high range. It is danger case.

![image](https://user-images.githubusercontent.com/123365842/216498080-bfe00810-8542-47fa-8b94-968584c56322.png)

To solve this problem,, we have to put De-coupling capacitor in parallel with the circuit. Every time the circuit switches, it draws current from Cd, whereas, the RL network is used to replacenish the charge into Cd.

![image](https://user-images.githubusercontent.com/123365842/216498230-a19749a0-e510-4128-9b11-a3c69a4e7e77.png)

![image](https://user-images.githubusercontent.com/123365842/216498256-f4e3ab25-5dd8-40ae-9ec0-92caf450588c.png)

# Power Planning
# 4) How to do power planning?

Up to here, we have taken care of local communication. Now let consider that local circuitory as a black box and it can be repeat multiple times and power supply is also connected to all of them as shown below,

![image](https://user-images.githubusercontent.com/123365842/216498336-e2debdcf-81dd-4c38-a4bf-9cf119353c52.png)

Now 16 bit bus has to retain the same signal from driver to the load. so it should get the sufficient power from the supply. But at this bus, there is no de-coupling capacitor is available because it is not physible to put capacitor at all over the place. now, power supply is far away from the bus, that is why some drop between them will definalty occurs.

Let consider this 16 bit bus connected to inverter. So, all capacitor are initially charged will get discharged and vice-versa due to inverter.

![image](https://user-images.githubusercontent.com/123365842/216498433-f96323ee-b3a2-425e-af42-52161def28bf.png)

But the problem is occurs due to all capacitor is connected to the single ground. This will cause a bump in 'ground' tap point during discharging.

![image](https://user-images.githubusercontent.com/123365842/216498474-885afa8c-0e9b-4118-8f8b-aebd3110078a.png)

Same problem will occurse during the charging time also. at that time lowering of voltage occurse at 'Vdd' tap point.

![image](https://user-images.githubusercontent.com/123365842/216498551-84387c34-790f-483a-bcbf-ffd1e92917d5.png)

The solution of the problem is use multiple power supply. So, every block will take charge from neartest power supply and similarly dump the charge to the nearer ground. this type of power supply is called mesh.

![image](https://user-images.githubusercontent.com/123365842/216498635-097bc5c7-3e54-4e2f-a00e-99a5d10bb9b5.png)

And the power planning is shown below,

![image](https://user-images.githubusercontent.com/123365842/216498733-45299293-f07a-4af5-8bac-1f7ab9a5fee7.png)

# Pin placement and Logic floor planning considerations
# 5) Pin Placement

Lets take below designs for example that needs to implemented.

![image](https://user-images.githubusercontent.com/123365842/216498870-4e753678-e24d-4dbc-999f-ef080ebc32f1.png)

Both the sections has different inputs like Din1 and Din2 and operated from different clocks like clock 1 and clock 2. along with that we have preplaced cells as well. So, basically now we have 4 input ports and 3 output ports.

let's have one more design that needs to be implemented. this types of circuits are very much helpful to understand the timing analysis of inter clocks.

now complete design becomes like given below which has 6 input ports and 5 output ports. it is called the 'Netlist'.

![image](https://user-images.githubusercontent.com/123365842/216498934-415b69e9-5c3b-4ff0-98d0-927f14eaee9d.png)

Let's put this netlist in the core which we have designed before and let's try to fill this empty area between core and die with the pin information. The frontend team who decides the netlist input and output and the backend team who done the pin placements. So according to the pin placements, we have to locate the preplaced blocks nearer to the inputs of the preplaced blocks.

![image](https://user-images.githubusercontent.com/123365842/216499001-a855dd76-345d-48ce-be01-cb8eb5adcea5.png)

Here one thing that we noticed is that clock-in and clock-out pins are bigger in size as compared to input and output pins. reason behind this is that, input clocks are conntinuously provides the signal to the every elements of the chip and output clock should out the signal as fast as possible. So, we need least resistance path for the clocks inputs and clocks outputs. So, bigger the size, lower the resistance.

One more thing is need to take care about is that, this pin placement area is blocked for routing and cell placements. so we nned to do logical cell placement blockage. this blockage is shoown in above image in between pins.

So, floor plan is ready for Placement and Routing step.

# Steps to run floorplan using OpenLANE

Before run the floorplanning, we required some switches for the floorplanning. these we can get from the configuration from openlane.

![image](https://user-images.githubusercontent.com/123365842/216499709-7aa46e0f-4bdc-4359-ac18-dae90b83cd3f.png)

Here we can see that the core utilization ratio is 50% (bydefault) and aspect ratio is 1 (bydefault). similarly other information is also given. But it is not neccessory to take these values. we need to change these value as per the given requirments also.

Here FP_PDN files are set the power distribution network. These switches are set in the floorplane stage bydefault in OpenLANE.

![image](https://user-images.githubusercontent.com/123365842/216500065-80732e6e-3148-4465-8938-453a9ba33e01.png)

Here, (FP_IO MODE) 1, 0 means pin positioning is random but it is on equal distance.

In the OpenLANE lower priority is given to system default (floorplanning.tcl), the next priority is given to config.tcl and then priority is given to PDK varient.tcl (sky130A_sky130_fd_sc_hd_congig.tcl).

Now we see, with this settings how floorplan run.
Reviewing floorplan files and steps to view floorplan

In the run folder, we can see the connfig.tcl file. this file contains all the configuration that are taken by the flow. if we open the config.tcl file, then we can see that which are the parameters are accepted in the current flow.

![image](https://user-images.githubusercontent.com/123365842/216500316-3d83f796-1d61-46bc-a86c-5a72debf62f3.png)

here we can see that, the core utilization is 35%, aspect ratio is 1 and core margin is taken as 0. while in default the core utilization is 50%. this is the issue. because this design is override the system. but it is the taken from PDK varient.tcl file. so priority vise it is true.

To watch how floorplane looks, we have to go in the results. in the result, one def( design exchange formate) file is available. if we open this file, we can see all information about die area (0 0) (660685 671405), unit distance in micron (1000). it means 1 micron means 1000 databased units. so 660685 and 671405 are databased units. and if we devide this by 1000 then we can get the dimensions of chips in micrometer.

![image](https://user-images.githubusercontent.com/123365842/216500398-5b6845f0-b45a-4263-9b3e-8fd99f775154.png)

so, the width of chip is 660.685 micrometer and height of the chip is 671.405 micrometer.

To see the actual layout after the flow, we have to open the magic file by adding the command magic -T /home/kunalg123/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

And then after pressing the enter, Magic file will open. here we can see the layout.

![image](https://user-images.githubusercontent.com/123365842/216500522-2a0958e1-ce3d-4045-87b2-1424483ee7cb.png)

# Reviewing floorplan layot with magic.

In the layout we can see that, input output pins are at equal distance.

![image](https://user-images.githubusercontent.com/123365842/216500790-fa196b1f-2f8e-458c-9621-9a64387e7e91.png)

after selecting (To select object, first click on the object and then press 's' from keyboard. the object will hight lited. to zoom in the object, click on the object and then press 'z' and for zoom out press 'sft+z') one input pin, if we want to check the location or to know at on which layer it is available, we have to open tkcon window and type "what". it will shows all the details about that perticular pin.

![image](https://user-images.githubusercontent.com/123365842/216501273-a7ab1bb5-d7a1-4c9d-9ef7-1cc353e09d9b.png)

![image](https://user-images.githubusercontent.com/123365842/216501382-8e51996c-e3be-408e-8e7d-0efabd2ef7c4.png)

so, it show that the pin is in the metal 3.similarly doing for the vertical pins, we find that this pin is at metal 2.

![image](https://user-images.githubusercontent.com/123365842/216501774-e86b5881-607e-49b8-8caa-1ede0e807ddc.png)

Along with the side rows,the Decap cells are arranged at the border of the side rows.

![image](https://user-images.githubusercontent.com/123365842/216501601-cddf8697-4114-4683-8f24-f320cdc38274.png)

Another cells also placed here, which is a tap cells. these cells are meant to avoide the latch-up problems in the CMOS devices. it connect N-well to the Vdd and substrate to the Ground. these tap cells are placed at diagonally equal distance.

![image](https://user-images.githubusercontent.com/123365842/216501884-cae9cf3b-28f7-4aaf-8967-ec214870d16f.png)

In the floorplane, standerd cells are not placed but here standerd cells are available in the left side of the floorplan. we can see few boxes are there.

![image](https://user-images.githubusercontent.com/123365842/216502114-dfd0b486-34da-4aed-ace6-4dc1b59e79a1.png)

here we can see that first standerd cells is for buffer 1. similarly other cells are for buffer 2, AND gate etc.
Library building and Placement
Netlist binding and initial place design
1) bind netlist with physical cells

Taking netlist as what we taken before,

![image](https://user-images.githubusercontent.com/123365842/216502199-1c2e32d5-4066-4802-ac90-3f42ababfb56.png)

Here, we can see that every gate or flip-flops have a shape to understand the functionality of the element. But practically, this cells are square or rectangular boxes which has internally some logic to perform. So, here we are taking all the elements from netlist and giving them a perfact height and width with perticular dimention. These all cells together are called 'self'. And this self are stored in the lybrary. Library have all the innformation about all the blocks, like height, width , time delay, conditional innformation, etc. library also have a option for the similar cells (with same functionality) like this with different height and width. According to our space available at floorplanning we can choose out of them.

![image](https://user-images.githubusercontent.com/123365842/216502240-9e99a04d-d34b-43cb-a9b5-ae3b8c6681ca.png)

After giving size and shape to each and every box, next step is to take the boxes or element from library and placed in the floorplan. This is called placements of the cells.According to the design of the netlist, we have to put physical blocks in the floorplan which we have design before.Put all the blocks according to the input and output of that perticular blocks.

![image](https://user-images.githubusercontent.com/123365842/216502303-40314d80-e89e-445d-9180-4e5626e9571d.png)

up to here we have done stage one and stage two placement. Now we will going for stage 3 and 4. here we have to place FF1 of stage 3 nearer to the Din3 and FF2 of stage 3 nearer to the Dout3. But Din3 and Dout3 are at somme distance from eachother. same thing is there for FF1 and FF2 of stage 4. Let's we placed these all element in such manner that all elements are closed to it's input and output pins.

![image](https://user-images.githubusercontent.com/123365842/216502368-316f9ac4-c908-428c-b8c6-ffc88fb5cdf7.png)

But, the distance of FF1 of Stage 4 and Din4 is still far them others. By optimizing the placement, we can solve this problem.

# Optimize placement using estimated wire lenght and capacitance
# 2) Optimize Placement

As we seen that the distance from Din2 to FF1 of stage 2 is higher. so if we connect the wire between them then resistance and capacitance of the wire comes in to the picture. and due to this the signal integrity can not maintain.

To maintain the integrity of the signal out from Din2 to FF1, we have to put some repeaters like buffers on between Din2 and FF1. But it will cause of loss of area.

In the stage 1, there is no need of any repeater to transmit the signal. But in stage 2, due to high distance, the lenth of wire is high and signal is not transmitted in perticular range. so we required repeater.

![image](https://user-images.githubusercontent.com/123365842/216502492-716b2949-09ed-4f5b-931b-bee50e785b1b.png)

# Final Optimization

Similar as stage 2, in Stage 3 also we required the buffer between gate 2 and FF2.

![image](https://user-images.githubusercontent.com/123365842/216502577-cdf59d48-5951-4739-9e71-248835a41907.png)

Stage 4 is bit tricky as compared to other stages. ![image](https://user-images.githubusercontent.com/123365842/216502610-821a867c-daf0-4e52-8fb7-db576f5357f9.png)

Now we have to check that, what we have done is correct or not. For that we need to do Timing analysis by considering the ideal clocks and according to the data of analysis, we will understand that, the placement is correct or not.

# Need for libraries and characterization.
# Library charactorization and modelling

In whole IC design, we have to go through synthesis, floor/power planning, placement, routing , STA. In all this steps one thing remain common, which is "Gates or Cells". That is where the library charactorization becomes very important.

# Congestion aware placement using RePLAce

Right now we are not constrain about timing, but constrain about the congestion. so, we are making the congrstion is less.

The placement is donne in two stages. Global and detailed. In global placement, legalization is not happened but after detailed placement legalization will be done.

When we run the placement, first Global placement is happens. main objective of glibal placement is to reducing the length of wires.

Now opening the Magic file to see actual view of standerd cells placement.And the actual view in the magic file is given below,

![image](https://user-images.githubusercontent.com/123365842/216502874-e0dea5f3-825b-4784-98e8-25ef755df615.png)

If we zooom into this, we find the buffers, gates, flip flops in this.

![image](https://user-images.githubusercontent.com/123365842/216502959-6bdd549e-9840-4b34-897a-552f11d6ad3a.png)

# Cell design and characterization flows
# Inputs for cell design flow
# Cell design flow

As we know that standerd cells are placed in the library. And in the library many other cells are available which have same functionality but the size is different. As size is different the parameters like hVt, Ivt also different for each standerd cells.

If we take one of the standerd cells called inverter, it has their own design flow by this it can be understandable to EDA tool.

The cell design flow is devided into three part.

    Inputs

    Design steps

    Outputs
    
 ![image](https://user-images.githubusercontent.com/123365842/216503071-3e0e1ce4-0e42-4221-ab7c-aaccf0396d5b.png)
 
 # 1)inputs

inputs required for cell design is PDKs, DRC and LVS rules SPICE models, library and user defined specs.
Circuit design steps
# 2)design steps

steps are circuit design, layout design, characterization
# 3)Outputs

The typical output what we get from the circuit design is CDL(circuit description language) file,GDSII,LEF,extracted spice netlist(.cir).
# Layout design steps

    implement function
    
![image](https://user-images.githubusercontent.com/123365842/216503198-b126e2c6-ec8a-4f7a-85b0-6b01ec507f1c.png)
 
Derive the NMOS and PMOS network graph

![image](https://user-images.githubusercontent.com/123365842/216503252-6e0d4e37-6e08-475c-b0ef-c85f2a1349a0.png)

Obtain the Euler's path

![image](https://user-images.githubusercontent.com/123365842/216503321-ed693d03-9f80-4bde-be48-c6560d61e6c8.png)

Stick diagram
![image](https://user-images.githubusercontent.com/123365842/216503397-1101d1c9-a003-4cb8-8e86-7c95af73ea73.png)

Convert stick diagram into proper layout

![image](https://user-images.githubusercontent.com/123365842/216503446-733d0fb0-3f45-482a-93ed-ee1820a957b1.png)

After layout design, we have to ecxtract the layout and characterize it. In characterization step, we can get the information about Timing, Noice,power.libs and function.

# Characterization Flow

As of now, from the circuit design and layout design, we have final layout of buffer cell. where two buffers are connected in series with each other.

![image](https://user-images.githubusercontent.com/123365842/216503543-775a5aeb-1604-47e3-bbff-d2ae4117d899.png)

Now steps of flow is:

    Read the model file

    read the extracted spice netlist

    reconize the behavior of buffer

    Read the subcircuit of the inverter

    Ateched the neccessory power source

    Apply the stimulus

    Provide the necessory of output capacitance

    Provide the necessory simulatin command

This all steps we have to give in "GUNA" software. and this software will give the timing, noise, power.libs and functions.

# General Timing characterization parameters
# Timing threshold defination

![image](https://user-images.githubusercontent.com/123365842/216503672-a61a6172-45a0-433a-a46f-93e982085d41.png)

Let we take the waveform from the output of the first buffer and it will be input of the second buffer and taking output of the second buffer also.

![image](https://user-images.githubusercontent.com/123365842/216503723-68684529-16d3-488f-ba05-13c15182716d.png)


    slew_low_rise_thr

here low means nearer to the ground, and rise tresold means we want to measer the slope of the increasing graph. typical value of slew low rise thr is around 20-30%. 

![image](https://user-images.githubusercontent.com/123365842/216503788-25f8f5b2-84c6-4404-942a-bddc643f61c6.png)


    slew_high_rise_thr

same as above, high means nearer to high value. 

![image](https://user-images.githubusercontent.com/123365842/216503860-8f27dc65-230c-4bfc-8067-64b36806f028.png)

whenever we want to calculate the slew, take the point at 20% from the low and take the point at 20% from the high. according to these point, take the time data and the time difference between them will helps to calculate the slew.

    slew_low_fall_thr

![image](https://user-images.githubusercontent.com/123365842/216503899-fd9d2ef3-027d-45d8-a84c-223fc38fd8f6.png)

    
    slew_high_fall_thr
    
![image](https://user-images.githubusercontent.com/123365842/216503981-8ce5700d-064f-4fb0-a88c-c1acecfa3092.png)

NOw, taking the waveform of input stimulus which is input of the first buffer and with that taking output of the first buffer.

Similar as a slew, thresolds are for delay also available. for that same as slew, we have to take some rise and fall points from the waveforms. this tresolds are almost 50%.

    in_rise_thr

![image](https://user-images.githubusercontent.com/123365842/216504041-12eb18a3-cd32-44d5-ad7a-6fd430095bf9.png)

    in_fall_thr
    
![image](https://user-images.githubusercontent.com/123365842/216504093-d2cb59d8-2455-4bce-9ceb-89d1f104d57b.png)

    out_rise_thr
    
![image](https://user-images.githubusercontent.com/123365842/216504149-d6b167ba-9b7a-4dbc-a047-0e44931967ac.png)

    out_fall_thr
    
![image](https://user-images.githubusercontent.com/123365842/216504229-e74fd8fe-fe1d-41c0-931c-931205cd1564.png)

So, according to rise and fall theresold we can find the rise delay and fall delay of the buffer.

![image](https://user-images.githubusercontent.com/123365842/216504277-fe6633af-09b2-4cc2-805f-5b8874932da6.png)

# Propogation delay and Transition time
# propogation delay

let's take the same setup for understand the propogation delay. Time delay = Time(out_thr)-time(in_thr).

Let's take waveform on which we can apply above formula.

![image](https://user-images.githubusercontent.com/123365842/216504353-14cfefec-7441-4ec6-9afd-7ecd7d8927fe.png)

In any case if thresold point move at the top, at that time we get negative delay because output comes before input. so reason behind the negative delay is the poor choice of the tresold points. which is not acceptable. so, choosing the thresold point is very important.

![image](https://user-images.githubusercontent.com/123365842/216504406-79528228-8238-4995-81e2-c38ed90d3cf0.png)

Taking another example where the wire delay is very high because of high distance between two elements. so, here by choosing correct thresold point then also we get the negative delay.

![image](https://user-images.githubusercontent.com/123365842/216504505-5ccf0c3b-d611-4340-a1b9-7b1ccc252dc3.png)

# Transition time

transition time = time(slew_high_rise_thr)- time(slew_low_rise_thr)

or

transition time = time(slew_high_fall_thr)- time(slew_low_fall_thr)

let's take waveform for understand the slew calculation.

![image](https://user-images.githubusercontent.com/123365842/216504574-50355add-91a8-465e-b7bb-a8fa4d6c59f9.png)
