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
```
docker
pwd
ls -ltr

```
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/c43a6b9b-7834-4491-8394-1b8cde465a4f.png)

```
 ./flow.tcl -interactive
```

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b47c5a57-1182-4cf9-b78e-68b62e8c6f32.png)

```
package require openlane 0.9

```
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/1a837c32-fba5-4d88-9fe9-678d3883be97.png)

Design setup stage:

```
prep -design picorv32a

```
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/0dc4f544-07be-4cde-a89f-2687e7b0a736.png)


New files created :

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/56f78930-6edd-43f7-b529-d2a1d4e196bd.png)

Merge files created by merging LEFs:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/f6ea264c-722d-42f0-a952-4808a14b89ae.png)

```
run_synthesis
```

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b1f40bf3-f54b-49ab-a51e-543f3b5336da.png)


Finding Flop Ratio:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9670c194-bc66-4f7e-bb11-e96766c21d44.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/1b8a6571-733e-4603-8292-7ed1350ef935.png)

= 10.84 %


Statistics report:

```
less 1-yosys_4.stat.rpt
```

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9122d9f3-53c3-487a-8340-1facc7993b06.png)


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/8550d725-013c-4d29-baaa-4bc0c79edc48.png)

Timing report:
```
less 2-opensta.timing.rpt
```
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

``` 
~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-09_12-35/results/floorplan$ less picorv32a.floorplan.def

```
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

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/01caa690-63f0-4242-aeb0-55e701dee33f.png)

vertical cell:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/6d7daccd-cd55-47cf-bf18-551e481b121f.png)


decap cells:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/7d510914-3649-416a-b1da-6d4195f68bdc.png)


Standar cells in the lower left corner:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/0ed347c6-7c58-4898-8e53-53c78ab0609b.png)


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b7fccc04-bd5e-45c5-bd07-4a1ed0cb919d.png)

## 

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/229ea794-8fcf-404f-9714-b0a56c6abc9c.png)

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

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/7201d021-206c-46fa-a7f5-b60f8b6db63e.png)

 Standard cells which were initially in the bottom left have moved into the standard rows:

 ![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9b28532a-5987-4d56-bc10-779a6b8c6f75.png)

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

To change how the IO ports are placed:
4 stratergies supported by io placer:

After changing:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/3bc57e6e-1619-4f71-90a4-ae13a5c8989a.png)

* SKY_L0 - IO placer revision

* SKY_L1 - SPICE deck creation for CMOS inverter

* SKY_L2 - SPICE simulation lab for CMOS inverter

* SKY_L3 - Switching Threshold Vm

* SKY_L4 - Static and dynamic simulation of CMOS inverter

* SKY_L5 - Lab steps to git clone vsdstdcelldesign
 
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/8ff14b85-c428-4e5c-a750-3189bdedcc4a.png)

Different Layers used in building of the inverter:

1. Copying the tech file to the required place:

   ![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/3ae6b675-f0ee-41a6-8297-07d77a0991f6.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/d1a0f64b-b592-479a-b361-3ea6075981c4.png)


& => is the keep the next command promp free

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/78844dae-da18-4be8-a2d9-147e1fa81a79.png)



Red Line is the Poly

## SKY130_D3_SK2 - Inception of Layout and CMOS fabrication process

* SKY_L1 - Create Active regions

* SKY_L2 - Formation of N-well and P-well

* SKY_L3 - Formation of gate terminal

* SKY_L4 - Lightly doped drain (LDD) formation

* SKY_L5 - Source and drain formation

* SKY_L6 - Local interconnect formation

* SKY_L7 - Higher level metal formation

* SKY_L8 - Lab introduction to Sky130 basic layers layout and LEF using inverter

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/d4d4d33d-a1f0-4e0e-ba4a-661a306ea0c4.png)

The green coloured part is n-diffusion layer. This we can infer from the colour pallete.
Brown is p-diffusion.

When poly crosses n-diffusion, it is nmos

s![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/4433a966-d39b-482e-bd85-7dddcd8abb00.png)

When poly crosses p-diffusion it is pmos

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/090f3dce-6b4a-4584-915e-069ee2c6e784.png)

To check whether drain of pmos and nmos are connected:
Source of pmos should be connected to vdd
And source of nmos to ground

Press "S" twice while hovering the mouse over the part, to check what it is connected to:
In this case, we hovered over Y and presses "S" twice

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/703ae154-678b-4340-95ee-d1befcdda04a.png)

Connectivity of source of pmos to vdd:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/8af0e5a9-9183-4f4d-b8fa-b7f4342984b3.png)

Source of nmos to ground:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/fa97d04f-75c1-490d-9081-10d9d8086c4f.png)

for PNR placement of any cell/macro, you dont need logic information. You only need to know the boundry and pins.
LEFs also protect the IPs.

* SKY_L9 - Lab steps to create std cell layout and extract spice netlist
Always make sure the DRC error is 0. It cannot be manufactured if DRC error is present.

How do we know the logical functioning?
1. To extract it on spice, got to tkcon window
2. Create an extraction file

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/39ded6af-02d0-4942-99b4-46dd44e49117.png)

To check if ti has been created:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/396a6e9d-2b64-4bf4-8ef5-72f0c48e0276.png)

ext2spice => extract to spice, and we are also extracting the parasitic capacitances also
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/58477c46-3925-4e78-a09e-87dd65829159.png)


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/2e21ccc5-7e16-44a9-a9c6-588ec92e3fb8.png)

Spice file has been created:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/c15b18d8-8a00-4d70-864a-622ef34bb3f3.png)

Inside the spice file:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/53807526-ca30-4004-b502-d6d849d36c9b.png)

## SKY130_D3_SK3 - Sky130 Tech File Labs

* SKY_L1 - Lab steps to create final SPICE deck using Sky130 tech

  Understanding the spice deck:

  pshort =>PMOS
  nshort =>NMOS

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/f8cf8f23-6d87-4eab-8e86-cb514b64db2c.png)

We need to define VDD, VSS AND VG for transient analysis

To find dimensions of the box, enable the grid by going to windo -> grid on
Right click on the grid you want to select, and type box in the tkcon window to see the dimensions

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/2ddee9d7-629f-4b6f-8c9e-4455a27f4317.png)


Changing the scale to 0.01u:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/6c911aca-7190-48bb-ad49-70ddda00597c.png)

Creating the flow for the spice deck:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/27b26325-8333-4b8e-a70c-6131dc358806.png)

model file:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/13302e5b-5975-4c0e-a8a9-7f15e77a88fc.png)

In the spice model file the pshort is named as pshort_model.0
Hence, we need to change its name in the spice deck.

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/d66f32f8-8433-49b9-87e3-9df7fc8cd0bd.png)

Install ngspice:
```
sudo apt install ngspice
```

Run the spice simulation and pass the spice deck as the source file:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9226ceda-21c1-4d72-a7b1-5e159f211ca7.png)

* SKY_L2 - Lab steps to characterize inverter using sky130 model files

Plotting the simulation:

```
plot y vs time a // plot the output vs time sweeping the input
```

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/aca05dc4-1734-4482-8631-50f115361db0.png)

Plot:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/03e9e91f-1cc8-406b-8bb1-15614703b59a.png)

Charecterize the cell:

To find the value of 
1. Rise transition (time taken for o/p waveform to transit from 20% to 80% of max value)
20% of the rising waveform is at: 2.164 ns at 0.66 V

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/140684fd-6819-4b4d-8f41-7d12635f1a11.png)

80% of rising waveform is at : 2.205 ns at 2.64 V

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/fe81d32d-90f5-44b8-9c11-5e5261e77c0b.png)

Rise time = 2.205-2.164 = 0.041 ns


2. Fall transition time (time taken for o/p waveform to fall from 80% to 20% of max value)
3. Cell Rise delay  (time diff between 50% of output and 50% of input rise time) : at 1.65 V

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/f849ac4e-0603-4b38-b1c6-4f4015e8ae30.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/0552c004-ae9d-4929-810f-179fc04122b6.png)

Calculation:
2.18 -2.15 = 0.03 ns

4. Cell fall delay (time diff between 50% of output and 50% of input fall time)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/0d77e584-6c60-4daf-890e-865172744259.png)

Calculation:
4.08 -4.04 = 0.04 ns

* SKY_L3 - Lab introduction to Magic tool options and DRC rules
Website to understand magic: http://opencircuitdesign.com/magic/

The technology file is one single magic file that tells MAGIC, everything it needs to know about the process. It declares all layer types in colours and patterns but it also defines electrical connectivity, DRC Rules, GDS generation rules, device extraction rules for extracting netlists, LEF, DEF etc...

SkyWater Documentation: https://skywater-pdk.readthedocs.io/en/main/
Github site: https://github.com/google/skywater-pdk

* SKY_L4 - Lab introduction to Sky130 pdk's and steps to download labs
Get drc_tests.tgz

```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests

```
![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/e9a29468-74c4-4364-9b01-731ce4627ebb.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/8e0f98f4-7e44-44a8-b1ef-a702cc02f6de.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/56f9b980-214a-4366-a51b-bc5e0eb47acb.png)

* SKY_L5 - Lab introduction to Magic and steps to load Sky130 tech-rules

```
magic -d XR
```
Open met3:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/cf29f7b4-76a0-46c2-8442-fad8f9fe5424.png)

The white patches show the DRC error

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/5aafa453-0e7e-45d5-bcef-9d2a9b0ea02d.png)

The erros can be observed in the tkcon window:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/1b1fdb7a-1c07-4bf9-9d40-cb7a355616d8.png)

From the documentation:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/81338bc0-eae9-4908-b5c4-5102a70776f6.png)

MAke a small section in an empty space and choose m3contact from the paint pallete, then in tkcon type "cif see VIA2"


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/ebf81f74-cf7b-485c-8dd7-95e05ae17e9e.png)

The black spaces which appear are the contact cuts. They don't actually exist in the drawn layout view, but what they represent is 
the mask layer for via2 that will end up in the output GDS when you geenrate GDS from the layout.

They are created form the rules in the sif output section of the tech file. Which tells how to draw contact cuts.

To snap the selection box close to the cut use
```
snap int
box
```

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/ce244ff1-5e4c-41e4-b9db-38c3a3c1470f.png)

To find distance from edge:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b7c2d696-ec57-42c9-ade9-13424fd5eefb.png)


* SKY_L6 - Lab exercise to fix poly.9 error in Sky130 tech-file

* SKY_L7 - Lab exercise to implement poly resistor spacing to diff and tap

* SKY_L8 - Lab challenge exercise to describe DRC error as geometrical construct


# sky130 Day 4 - Pre-layout timing analysis and importance of good clock tree

## SKY130_D4_SK1 - Timing modelling using delay tables

* SKY_L1 - Lab steps to convert grid info to track info

Extract LEF file out of this mag file and plug it into picorv32

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/3605eca9-a69a-488b-b291-8c2f4a41d408.png)


Tracks are used during routing stage:
Where all you want your routes to go.
Requirement 1: Ports should be on the intersection of the horizonal and vertical tracks.

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/9ac9bee1-5910-4179-bed3-2e450d1af159.png)

Ports should be on the intersection of the li1 tracks, intersection of horiizontal and vertical tracks:

We change the grid size to match the track information:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/6ffc4f01-e0ce-4e1c-b069-a967ec03781f.png)

The input and output ports are at the intersections of the horizontal and vertical tracks:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/ffa87ba2-0dd1-4f41-9ac6-cc85872ab1d9.png)

* SKY_L2 - Lab steps to convert magic layout to std cell LEF

Requirement 2: The width of the standard cell should be in the odd multiples of the x pitch

xpitch from the track info is 0.46

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/077c1bb8-7021-48ec-b250-2767956bc727.png)

There is a total of 3 boxes (1+1+1/2+1/2) ie, width of the standard cell is in the odd multiples of the x pitch.

Whenever you make the layout there are no ports. When you extraxt the LEF file, the ports are deifned as pins

To define ports for diffferent layers:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/89921f9b-706b-474b-aeeb-e4e26636ffb2.png)

After defining ports, we have to define the purpose of the port

After these two paramters have been set, we are ready to extract the LEF file

To create the LEF file:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/d6799258-f87a-429a-ae81-9ee901c47a67.png)

It has been created:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/81d35d2a-7bc2-48bf-ad18-7395a4605a5c.png)

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/bc326d0e-9cdd-4143-aaed-3ebbdcee265f.png)

Next, plug this lef file into picorv32 flow

* SKY_L3 - Introduction to timing libs and steps to include new cell in synthesis

* SKY_L4 - Introduction to delay tables

* SKY_L5 - Delay table usage Part 1

* SKY_L6 - Delay table usage Part 2

* SKY_L7 - Lab steps to configure synthesis settings to fix slack and include vsdinv

Copying the lef file and sky130 library file to src folder of picorv32a:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/2b6038c3-b25f-4795-9f14-1029cc61e069.png)

Editing config.tcl to be able to use our custom cell:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/b0287f5d-98b8-4996-8518-58a335260ec4.png)


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/caf1ed92-babe-4055-98ce-e463b8fa7426.png)


The lef file contains the cell that we created:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/1732c137-193d-4618-a803-48209acb7d17.png)


Make sure to type the following commands after the prep -design picorv32a step:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/3a9cbe45-a807-4d53-a261-14e40f1a438d.png)

And then as usual, run_synthesis
to run floorplan and placement:

```
init_floorplan
run_placement
```

Open the recent placements file:

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/83229b6d-2f37-4983-a558-1c9af6aba1ec.png)


![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/c8264cbe-f295-451c-94f6-6ecd5ae709b5.png)


After floorplanning and placement using custom cell:

![image](https://github.com/Navya-tayi/pes_openlane_pd/assets/79205242/d8092ebf-41e7-4230-8621-46b0de866e50.png)







