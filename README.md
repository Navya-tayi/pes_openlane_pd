# pes_openlane_pd
## Day 1 - Inception of open-source EDA, OpenLANE and SKY130 PDK
### How to talk to computers
* SKY_L1 - Introduction to QFN - 48 Package, chip, pads, core, die and IPs:
A typical electronic board:
Our focus is on the chip:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/99631da3-df06-4443-a565-bef72a526ba5.png)

Along with processor there are interfaces.

Typical Board diagram:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/78df634a-1c62-4496-b799-3aa1f4699f31.png)

If you open up the IC, what we see is the "package"
Pin locations are driven by the arduino board.  Chip sits at the center of the package 

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/d89d2c0f-fd81-43cf-856d-cc993e6874ec.png)

The chip is connected to package using wire bonds

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/6c10930f-7264-4e0e-8798-020b1c7ff245.png)

When you open up the chip:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/a6c88ed9-89a1-4543-9d03-5ea1da2c5e85)

PADS are used to send signal to inside the chip. Any signal which is inside the chip can go outside and vice versa.
Core is where all the digital logic gates are present

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/2ad08704-57c9-4876-89b5-2b0e51a1c7e8.png)

RISC V SOC:
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/310406a5-08c6-48e0-ab6e-f706891342cc.png)

A core consists of Soc, SRAM, ADC, DAC, PLL

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/74e6b2c2-bb94-4583-a343-2f5c2e7081ff.png)

Foundry : All devices depend on a foundry. A factory which has a set of machines where chips are manufactured. Lithogrpahy systems are also present here. VLSI design engineers communicate with the foundry with some interface.

Foundry IPs: Foundry intellectual properties

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b5208262-a5d9-4786-a870-511c0793b087.png)


There is a clear distinction between IPs and Macros : Macros are pure digital logic. IPs are something which require some amount of intelligent techniques to build. 
To manufacture the chip you need to communicate with foundry. TO communicate you have to use interface files. 

* SKY_L2 - Introduction to RISC_V
  RISC V ISA - Instruction set architecture.

  If you have a C program and it needs to be run on a hardware with a particular layout, you need to pass th einformation to the hardware in certain terms.
  The C program is compiled in its assembly language program which is the RISC v assembly language program. This assembly language program is converted into machine language program, which is binary language ie, 1s and 0s.

Another interface is the Hardware Description Language which you have to implement using RTL.
And then from RTL to layout.

* From Software Applications to Hardware

Apps run on laptop Hardware:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/1f368291-a7d4-4570-9dc0-e9eab4d9e4b7.png)

These apps or software enter the system software, and SS converts the application program into binary langyage.
There are various layers of system software, ie the operating system, Compiler and Assembler.

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/56b21264-7a94-452c-8a6f-090d0ba7474e.png)

### SKY130_D1_SK2 - SoC design and OpenLANE
* SKY_L1 - Introduction to all components of open-source digital asic design
Designing ASIC requires:
RTL IP's

### SKY130_D1_SK3 - Get familiar to open-source EDA tools

* SKY_L1 - OpenLANE Directory structure in detail
Open Lane - complete RTL to GDS
You put in RTL Netlisk, Foundry PDKs and what you have is the GDS File
pdks => Process design kit (Skywater 130nm PDK- used for this workshop)
Skywater => Foundry level PDK
Foundry files are made to work with commercial EDA tools
open_pdks is a set of scrips and files which convert these foundry level pdks to be compatible with the open source EDA tools

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/a59a98aa-cc70-4d5d-9d0e-7181b2fb1d5d.png)

sky130A is a PDK variant => made compatible for open source

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/7ca37dfb-d073-4fe3-badb-77b182e27581.png)


libs.ref => contains all process specific files like timing
 
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/6e28d1d6-edda-410a-838d-62e0cc57854e.png)

sky130 =>process name
fd=> abbreviated foundry name (fd is for skywater foundry)
sc=> standard cell
hd => high density


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/8d8550b4-7ba4-4375-bec7-80a49170eb03.png)

techlef => are the files which contain layer information
lib => has the timing files

ff => fast fast
ss => slow slow
100C => temperature 
1v80 => voltage


libs.tech => contails files specific to the tool

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/732a5eea-e062-4fce-8eb9-d8d88afa797b.png)

* SKY_L2 - Design Preparation Step
'''
docker
pwd
ls -ltr

'''
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/c43a6b9b-7834-4491-8394-1b8cde465a4f.png)

'''
 ./flow.tcl -interactive
'''

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b47c5a57-1182-4cf9-b78e-68b62e8c6f32.png)

'''
package require openlane 0.9

'''
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/1a837c32-fba5-4d88-9fe9-678d3883be97.png)

Design setup stage:

'''
prep -design picorv32a

'''
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/0dc4f544-07be-4cde-a89f-2687e7b0a736.png)


New files created :

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/56f78930-6edd-43f7-b529-d2a1d4e196bd.png)

Merge files created by merging LEFs:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/f6ea264c-722d-42f0-a952-4808a14b89ae.png)

'''
run_synthesis
'''

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b1f40bf3-f54b-49ab-a51e-543f3b5336da.png)


Finding Flop Ratio:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9670c194-bc66-4f7e-bb11-e96766c21d44.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/1b8a6571-733e-4603-8292-7ed1350ef935.png)

= 10.84 %


Statistics report:

'''
less 1-yosys_4.stat.rpt
'''

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9122d9f3-53c3-487a-8340-1facc7993b06.png)


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/8550d725-013c-4d29-baaa-4bc0c79edc48.png)

Timing report:
'''
less 2-opensta.timing.rpt
'''
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/90f32b82-c2b2-491b-8f10-50c1f7352cb6.png)

## Sky130 Day 2 - Good floorplan vs bad floorplan and introduction to library cells

### SKY130_D2_SK1 - Chip Floor planning considerations

* SKY_L1 - Utilization factor and aspect ratio:

How do we come up with values of width and height:

Begin with a netlist: Netlist edines connectivity between different components

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/0405f17e-8ee3-41af-91bf-0edaf4c1fc1b.png)

* SKY_L2 - Concept of pre-placed cells

* SKY_L3 - De-coupling capacitors

* SKY_L4 - Power planning

* SKY_L5 - Pin placement and logical cell placement blockage

* SKY_L6 - Steps to run floorplan using OpenLANE
  Standard cell placement dosen't happen in floor plan

  ![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9e2902dc-f1ba-4568-9ad4-8c66d8e27fc0.png)


  README File contains the variables required for each stage:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/be80cb1c-8647-4327-9245-32694aa3eb6d.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/bb5837f9-2eb9-4b9a-9da9-82c3b17fb619.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/51fb8e1f-e890-4e10-9b94-7fe8212d8dac.png)

FP_CORE_UTIL :
FP stands for floorplanning
CORE_UTIL => total area of the netlist to the total area of cell, by default set to 50
FP_ASPECT_RATIO => height to width of the core
PDN stands for power distribution network

It is not necessary to set all the variables. You can set any of them based on where you are in the flow.

Placement Variables:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/88d5f9f5-986b-4d99-a947-e256ddc23719.png)

TARGET_DENSITY: How close or How spread out you want the cells to be packed
Initially, you might want lesser congestion

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/92f297d8-5f26-458b-9e2c-03d36922b6a8.png)


default parameters for floorplan stage:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/4e8ef862-0b1f-4a10-a818-cd014e30de90.png)

FP_IO MODE: Pin configurations around the core
- 1 means we want it to be equidistant


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9b3d4c3a-5372-4224-b363-073534e81aa5.png)

In openlane flow, the vertical and horizontal metal will be one more than what you have specified

''' 
~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-09_12-35/results/floorplan$ less picorv32a.floorplan.def

'''
def file => design exchange format
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/47a7cd00-e265-4a19-ae7d-cf0cee66b408.png)

DIE AREA is the are of complete die
(0,0) is the lower left x and y value
(660685, 671405) is the upper right x and y value
 1 micron = 1000 database units

Die area= (660685/1000) * (671405/1000) um = 0.44358 um  (um =>micro meter)

To see the floor plan: Using MAGIC

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b7d29b72-a3d3-4360-bbcb-292ffc506672.png)

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/616538bc-f75b-4411-b995-a77f609cb06c.png)

* SKY_L8 - Review floorplan layout in Magic


Use "Z" to zoom in 
and to choose a cell, hover over it and press "S"

in the tkcon console type "what" to find which layer it is in

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/01caa690-63f0-4242-aeb0-55e701dee33f)

vertical cell:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/6d7daccd-cd55-47cf-bf18-551e481b121f)


decap cells:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/7d510914-3649-416a-b1da-6d4195f68bdc)


Standar cells in the lower left corner:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/0ed347c6-7c58-4898-8e53-53c78ab0609b)


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b7fccc04-bd5e-45c5-bd07-4a1ed0cb919d)


## ![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/229ea794-8fcf-404f-9714-b0a56c6abc9c)

* SKY_L1 - Netlist binding and initial place design
  
* SKY_L3 - Final placement optimization

* SKY_L4 - Need for libraries and characterization

* SKY_L5 - Congestion aware placement using RePlAce

  Global placement => coarse placeemnt, no legalization
  legalization : Standard cells are placed exactly inside standard rows, there should be no overlaps

  objective of global placement is to reduce wire length

  ```
  run_placement
  ```

After placement :

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/7201d021-206c-46fa-a7f5-b60f8b6db63e)

 Standard cells which were initially in the bottom left have moved into the standard rows:

 ![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9b28532a-5987-4d56-bc10-779a6b8c6f75)

 ![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/c06481ee-e021-4fca-8b3a-35daac7ea10b.png)


 usually power distribution netwrok is also gets created during floor plan but in open lane the flow is a little different
 Floor plan does not create power distribution

 We do it before routing and post CTS

 ## SKY130_D2_SK3 - Cell design and characterization flows

 * SKY_L1 - Inputs for cell design flow

 * SKY_L2 - Circuit design step

 * SKY_L3 - Layout design step

 * SKY_L4 - Typical characterization flow

## SKY130_D2_SK4 - General timing characterization parameters

* SKY_L1 - Timing threshold definitions

* SKY_L2 - Propagation delay and transition time


# Sky130 Day 3 - Design library cell using Magic Layout and ngspice characterization

## SKY130_D3_SK1 - Labs for CMOS inverter ngspice simulations

* SKY_L0 - IO placer revision

  


