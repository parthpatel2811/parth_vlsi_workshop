# parth_vlsi_workshop
# contents
1.Introduction

2.Day1-Inception of open-sourceEDA,openLANE and sky130 PDK

3.Day2-Good floorplan vs bad floorplan and introdution to library cells

4.Day3-Design library cell using magic layout and ngspice charaterization

5.Day4-Pre-layout timing analysis and importance of good clock tress

6.Day5-Final steps for RTL2GDS using tritonRoute and openSTA
# Introduction
OpenLane is an open-source ASIC (Application-Specific Integrated Circuit) flow that facilitates the design and implementation of digital integrated circuits. It provides a complete RTL-to-GDSII (Register Transfer Level to Graphic Data System II) flow, leveraging various open-source EDA (Electronic Design Automation) tools. Developed by Efabless Corporation.
# Day-1 Inception of open-sourceEDA,openLANE and sky130 PDK

**The chip diagram**
![day1 theory 0 1](https://github.com/user-attachments/assets/5124a159-0281-47d4-9d88-fdd72ce69ad8)
![day1 theory 0 3](https://github.com/user-attachments/assets/6deff07e-0489-4fce-930a-5b42526c6016)

->**DIE :**
Die refers to the actual piece of silicon that contains the integrated circuit (IC).In the diagram, the die is represented by the central block that houses all the major components, such as the RISC-V SoC, GPIO bank, PLL, SRAM, and the ADC/DAC modules.

->**PADS :**
The contact points around the die that enable it to interface with external components, power supplies, and signals. They are crucial for connecting the internal circuitry of the die to the outside world.

->**CORE :**
The central processing unit (CPU) of the microcontroller that executes instructions.
![D1 T4](https://github.com/user-attachments/assets/98dc0803-55ab-4587-b94a-f2cb13f7675b)
**ISA (Instruction Set Architecture):** Defines the instructions a processor can execute (e.g., add x6, x10, x6).

**Assembler:** Converts assembly instructions into binary machine code.

**RTL (Register Transfer Level):** Describes hardware behavior in terms of data flow and operations, often using HDLs like Verilog or VHDL.

**Synthesized Netlist:** Translates RTL into a detailed list of logic gates and connections.

**Physical Design:** Converts the netlist into a physical chip layout, placing and routing the circuit elements on silicon.
![D1 T5](https://github.com/user-attachments/assets/1a4d8897-dc3b-4edc-b599-1b0b5408b77c)
![D1T6](https://github.com/user-attachments/assets/76b1db80-c6f9-4b6c-a00d-f5ce00242c7d)
**1.RTL (Register Transfer Level):** High-level digital circuit design written in HDLs like Verilog or VHDL.

**2.Synthesis (Synth):** Converts RTL code into a gate-level netlist, specifying logic gates and their connections.

**3.Floor/Power Planning (FP+PP):**

-Floorplanning (FP): Arranges circuit blocks on the chip.

-Power Planning (PP): Designs the power distribution grid.

**4.Placement (Place):** Positions standard cells within blocks to optimize space and performance.

**5.Clock Tree Synthesis (CTS):** Builds the clock distribution network to ensure even clock signal distribution.

**6.Routing (Route):** Connects cells with metal wires, creating the final layout while adhering to design rules.

**7.Sign Off:** Final checks and validations to ensure the design meets specifications. The result is a GDSII file for manufacturing.

**PDK (Process Design Kit):** Provides design rules and models used throughout the design process.

Follow this command

1.cd Desktop

2.cd work/tools/

3.cd openlane_working_dir/

4.cd openlane/
![introction](https://github.com/user-attachments/assets/72f09c6b-d728-41f0-9805-c07aa3bba69b)
step2: setting upopenlane environment
write below command

1->docker

2->./flow.tcl -interactive

3->package require openlane 0.9

4->prep -design picorv32a
![openlane](https://github.com/user-attachments/assets/41a44b71-9848-4f19-889d-1a9229ce3afd)
Now run synthesis. Enter below command

5->run_synthesis
![run_synthesis](https://github.com/user-attachments/assets/d100c8fe-3575-4f90-be48-2ea8d321c78e)
**Calculate the flop ratio**

-flop ratio is : 1613/14876 = 0.1084 (10.84%)
![count flip flop](https://github.com/user-attachments/assets/933f0fab-cc51-4271-bb8f-b8894986c3b5)
# Day-2 Good floorplan vs bad floorplan and introdution to library cells

![D2T2](https://github.com/user-attachments/assets/4de4d0c4-95aa-4a9d-b3c3-adc3baf1908f)

utilization factor = 1 (1 means core is fully utilized the area and no space left)

Aspect Ratio = Height / width = 2 unit / 2unit = 1

Aspect Ratio is 1 it signifies that chip is square shaped. When it is not 1 it means the chip is in rectangular shape.
![D2T3](https://github.com/user-attachments/assets/3ef9658e-aae9-4a88-899e-b60313521a6b)
![D2T4](https://github.com/user-attachments/assets/7f68182f-62c9-4a84-a013-f68b3f101818)
![D2T5](https://github.com/user-attachments/assets/2b5de0cf-edb5-4d84-9f06-8eb17a6d942b)
![D2T6](https://github.com/user-attachments/assets/7c5579df-daff-4238-86fa-39cf412a58c8)
![D2T7](https://github.com/user-attachments/assets/c6b8eea1-7e48-48f4-8f23-43d7a8f36ef2)
![D2T8](https://github.com/user-attachments/assets/716df12b-ff51-4816-8859-4860a5e81fb1)
![D2T11](https://github.com/user-attachments/assets/82df7295-5630-4284-8675-7b13e33d88ff)
Power planning in chip design focuses on efficiently distributing electrical power and managing heat to ensure reliable and efficient operation. Key aspects include:

**Power Grid Design:** Creates a network of metal layers (power rails) for delivering power and managing voltage drops.

**Power Domains and Gating:** Segments the chip into areas with independent power control to reduce overall power consumption.

**Power Analysis:** Evaluates static and dynamic power usage to ensure the power grid supports all operational conditions.

**Voltage Drop Analysis:** Ensures minimal voltage drops across power rails to avoid performance issues.
![D2T10](https://github.com/user-attachments/assets/2f90200e-78e7-4541-b18e-38383ee15205)

Running floorplan

command:- run_floorplan
![floorplan](https://github.com/user-attachments/assets/ea598ae5-92c9-4065-b82c-22fc30a924d4)
cell view of floorplan

```bash
magic -T  /Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![magic](https://github.com/user-attachments/assets/11b31eec-f027-4bb9-a4cd-9baa85bb5259)
cell zoom view of floorplan
![cell zoom view](https://github.com/user-attachments/assets/0f5c8e27-caae-4a22-8161-e7c0fb6b0ab8)
Metal layer detail in tkcon 
![tckon main](https://github.com/user-attachments/assets/998d17c3-2f84-49c1-91fb-5b4438a2e78b)
Running run placement

command:- run_placement
![run placement](https://github.com/user-attachments/assets/a672d093-e97d-440e-b4d4-0a95dfdeb34b)
File after run placement
![file after runplacement](https://github.com/user-attachments/assets/8d8d70a3-1c30-4c0e-a642-b77a460dbd71)
Magic view after placement
![after run placement](https://github.com/user-attachments/assets/820c9a06-28f3-4441-bf4d-f7f5091508ce)
magic tool view after the placement with tkcon screen
![after runplacement with tkcon](https://github.com/user-attachments/assets/db30dd8e-b384-4264-b472-1b388536bcca)
standard cells zoom view after placement
![std cell zoom view](https://github.com/user-attachments/assets/9f88ad14-63fb-4036-a2a0-e29335ec6bf8)

# Day-3 Design library cell using magic layout and ngspice charaterization
IO placer revision-change the IO parameters
![IO change](https://github.com/user-attachments/assets/7e43a8e2-e2c3-43dd-ba94-cd19db277383)
After change the IO parameter to view the layout
![IO change pin](https://github.com/user-attachments/assets/796a7699-882a-4864-b0b5-6fa54331d671)

Lab steps to git clone vsdstdcelldesign
![vsdstdcelldesign](https://github.com/user-attachments/assets/147c65bf-f085-4ece-a8f5-c2eec5a7d082)
![invetor command](https://github.com/user-attachments/assets/692d0de1-bbe7-4313-aed6-d32a40f386de)
![invertor](https://github.com/user-attachments/assets/03181039-4c6c-4280-b25c-f042981ea08d)
![invertor2](https://github.com/user-attachments/assets/0624e056-9853-4cd9-b95a-137c22ebfacd)

# Day -4 Pre-layout timing analysis and importance of good clock tress
->lab steps to convert grid info to track info
![D4P1](https://github.com/user-attachments/assets/daeda66b-aa84-4901-b365-8e36f290d7ab)
![D4P2](https://github.com/user-attachments/assets/52109cb9-f222-471c-981a-59dae04d8239)
![D4P4](https://github.com/user-attachments/assets/e58578e7-dc45-4594-98a2-29986081cd95)
![D4P5](https://github.com/user-attachments/assets/63fcfa16-3458-4d1c-90ee-6f8707ddfed5)
->lab steps to convert magic layout to std cell LEF

```bash
magic -T sky130A.tech sky130_vsdinv.mag &
```
![D4P6](https://github.com/user-attachments/assets/5ff11d8e-21b0-4678-8363-7f9bde2f798c)
![D4P7](https://github.com/user-attachments/assets/d6b3004c-b626-42df-a959-005b369ee24c)
![D4P8](https://github.com/user-attachments/assets/0bcca1d2-9417-41b9-84b9-740d262735c6)
![D4P10](https://github.com/user-attachments/assets/65a9fe5b-741a-46a9-83f6-d6cb4f65c0c9)


# Day-5 Final steps for RTL2GDS using tritonRoute and openSTA
