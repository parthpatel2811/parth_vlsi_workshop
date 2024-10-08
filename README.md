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
**CELL DESIGN FLOW**</p>
Standard cells are present in the library . Library consists of cells of different functionality,sizes and thresholds.Larger the size,Largest the drivestences.</p>
![D2T12](https://github.com/user-attachments/assets/a62afbcc-5e06-4569-984f-2725b9859661)
![D2T13](https://github.com/user-attachments/assets/563ed3f4-4698-4ddd-a46d-ddeea665d8a1)

- Circuit design
![D2T14](https://github.com/user-attachments/assets/f378b2c3-78da-4945-aee9-0f2b82610fe0)
![D2T15](https://github.com/user-attachments/assets/da46e441-6944-4beb-887c-3e0e4931193e)

- Layout design</p>
Art of Layout: EULER'S GRAPH , STICK DIAGRAM
![D2T16](https://github.com/user-attachments/assets/4b683a59-9839-4a31-bb07-e2be54000503)
![D2T17](https://github.com/user-attachments/assets/df100778-f3de-48e5-8792-b7fca3bfec58)

**Characterization Flow**
![D2T18](https://github.com/user-attachments/assets/072ba240-66e6-4215-82d3-059e5c0a24b2)

- lew Low Rise Threshold: Start point of the rising edge transition.

- Slew High Rise Threshold: End point of the rising edge transition.

- Slew Low Fall Threshold: Start point of the falling edge transition.

- Slew High Fall Threshold: End point of the falling edge transition.

- Input Rise Threshold: Voltage level where input is considered 'high'.

- Input Fall Threshold: Voltage level where input is considered 'low'.

- Output Rise Threshold: Voltage level where output is considered 'high'.

- Output Fall Threshold: Voltage level where output is considered 'low'.

**TRANSITION TIME**

time(slew_high)-time(slew_low)
![D2T19](https://github.com/user-attachments/assets/3fb80320-a686-4543-97d6-95834b4da6b6)

# Day-3 Design library cell using magic layout and ngspice charaterization
# SPICE DECK FOR CMOS INVERTER
![D3T1](https://github.com/user-attachments/assets/f5051187-9bb1-4bf4-a244-69927f1cc25a)
![D3T2](https://github.com/user-attachments/assets/328e4403-6dd2-4b1c-a374-638bda6f4811)
- **M1 MOSFET:** The drain is connected to the out node, the gate is connected to the in node, and both the source and substrate of the PMOS transistor are connected to the Vdd node.

- **M2 MOSFET:** The drain is connected to the out node, the gate is connected to the in node, and both the source and substrate of the NMOS transistor are connected to ground (node 0).

- **CLOAD:** This capacitor is connected between the out node and ground (node 0) with a value of 10fF.

- **Supply Voltage (Vdd):** The supply voltage is connected between the Vdd node and ground (node 0) with a value of 2.5V.

- **Input Voltage (Vin):** The input voltage is connected between the Vin node and ground (node 0) with a value of 2.5V.
![D3T3](https://github.com/user-attachments/assets/9b4d3798-d4c4-4d05-85bb-8bb508cf7037)
![D3T4](https://github.com/user-attachments/assets/434b8bf4-cd82-4ce0-bdb3-b1f3516f5599)

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
![D4T1](https://github.com/user-attachments/assets/839fcb6d-bd03-4f20-be31-f675637ec30c)

**AND Gate**

- **Function:** The AND gate outputs a high signal (1) only when all of its inputs are high. If any input is low (0), the output is low.

**OR Gate**

- **Function:** The OR gate outputs a high signal (1) when at least one of its inputs is high. The output is low (0) only when all inputs are low.
![D4T2](https://github.com/user-attachments/assets/07c3ac36-8b47-4975-b4fa-28e812b48642)

In this photo capacitor C1, C2, C3 ,C4 are assuming the same value.

C1=C2=C3=C4=25fF

Here at node A creating buffer tree.

Let  assume Cbuf1=Cbuf2= 30fF

Total capacitance at node A is 60fF.

Total capacitance at node B and C is 50fF.

- **Observations**

  - 2 level of buffering
  - At every level, each node driving same load
  - Identical buufer at same level

**Delay table for CBUF1 and CBUF2**
![D4T3](https://github.com/user-attachments/assets/dc4c17f7-932d-40e2-aea9-81efd380efcc)

- **For CBUF1**
![D4T4](https://github.com/user-attachments/assets/53b484c5-1655-499d-8c5b-93af31164ff2)

- **For CBUF2**
![D4T5](https://github.com/user-attachments/assets/c6791d98-a48c-4596-9c72-0c91168e0fff)

```bash
vim config.tcl
```
![D4P12](https://github.com/user-attachments/assets/c5dc9a2e-56ce-4e2d-a221-d5e21422b667)
![D4P13](https://github.com/user-attachments/assets/97fd6a3b-5b80-48e7-b3e7-823e27098c7d)
![D4P14](https://github.com/user-attachments/assets/441fade2-80bf-4483-9a11-1746a75f2634)

```bash
run_synthesis
```
![D4P16](https://github.com/user-attachments/assets/2614ba06-36fa-49af-9653-0a8e631f7d89)
![D4P17](https://github.com/user-attachments/assets/02efe44d-336e-4ee7-b546-9fd8af0c1b5d)

```bash
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) 1
echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1
```
![D4P18](https://github.com/user-attachments/assets/3fa205c7-b9a6-453d-9f8d-cfa7656a5f1f)
![D4P19](https://github.com/user-attachments/assets/373f3f88-fb6a-4528-af20-348bf9c3ef39)
![D4P20](https://github.com/user-attachments/assets/d03e7ab1-69b2-4ccf-94c1-3fed333b7282)
![D4P21](https://github.com/user-attachments/assets/80a91961-69a0-4237-969b-68ac73161ea7)
![D4P22](https://github.com/user-attachments/assets/8e1084ab-c3c7-4d16-9a36-ebb478cadb0e)
![D4P23](https://github.com/user-attachments/assets/c78a59fd-a323-405c-990e-50d42f1e8194)
![D4P24](https://github.com/user-attachments/assets/a83d0fdf-a1b6-4375-ae70-ea42ae27476e)
![D4P25](https://github.com/user-attachments/assets/57c1005d-5397-49c1-82ad-0a30bd396e72)
![D4P26](https://github.com/user-attachments/assets/7f410c69-a09f-4c25-963a-767a2651df95)
![WhatsApp Image 2024-08-18 at 6 34 54 PM](https://github.com/user-attachments/assets/0c85c925-0776-498a-ab1a-a3db2dfb421c)
![WhatsApp Image 2024-08-18 at 6 34 54 PM (1)](https://github.com/user-attachments/assets/653a4df4-7b5b-40c6-8d8a-2c513baa8099)
![WhatsApp Image 2024-08-18 at 6 34 54 PM (2)](https://github.com/user-attachments/assets/956fd217-cf16-4a84-b3bf-8f03381b5b85)
![WhatsApp Image 2024-08-18 at 6 34 55 PM](https://github.com/user-attachments/assets/cf4daf28-635d-47f8-895f-887b5f09d5c8)
![WhatsApp Image 2024-08-18 at 6 34 55 PM (1)](https://github.com/user-attachments/assets/9e8fc890-6aaa-4c1d-9af4-00a9129b03c5)
![WhatsApp Image 2024-08-18 at 6 34 55 PM (2)](https://github.com/user-attachments/assets/2401ec28-24d2-4d3b-bda6-49c23e9c8fa3)
![WhatsApp Image 2024-08-18 at 6 34 56 PM](https://github.com/user-attachments/assets/8760509c-c1b7-4bf5-80b9-c4b363ad3a6d)
![WhatsApp Image 2024-08-18 at 6 34 56 PM (1)](https://github.com/user-attachments/assets/1bfc47ab-5930-4296-8b57-c6ade7bac897)
![WhatsApp Image 2024-08-18 at 6 34 57 PM](https://github.com/user-attachments/assets/bd8430e9-d443-4516-b1df-7552ee2c2b95)

# Clock tree synthesis (H-Tree)
- **For CLK1**
![WhatsApp Image 2024-08-18 at 9 05 06 PM](https://github.com/user-attachments/assets/d8a52736-5d43-4040-b8ed-3f1906f4f3d0)

- **For CLK2**
![WhatsApp Image 2024-08-18 at 9 05 06 PM (1)](https://github.com/user-attachments/assets/d3c2e771-b7cc-428a-8320-d1bde4d637e8)
![WhatsApp Image 2024-08-18 at 9 05 06 PM (2)](https://github.com/user-attachments/assets/8f001cb2-efd2-41db-be41-6c8ae5400a11)
![WhatsApp Image 2024-08-18 at 9 05 07 PM (1)](https://github.com/user-attachments/assets/b03f0e27-507e-4a62-8789-bc2fd3a3bda8)

- **Imapct of crosstalk delta delay**
![WhatsApp Image 2024-08-18 at 9 05 07 PM (2)](https://github.com/user-attachments/assets/3bb9ace5-4932-4c10-9ace-7bf6e948147d)

- **Time analysis with real clocks**
![WhatsApp Image 2024-08-18 at 9 05 08 PM](https://github.com/user-attachments/assets/05c83e5a-ce38-48bf-886a-ec3b9d81098c)

# Day-5 Final steps for RTL2GDS using tritonRoute and openSTA

- **Maza routing**
![WhatsApp Image 2024-08-18 at 9 29 56 PM](https://github.com/user-attachments/assets/14495bbb-b199-4f57-b2e5-36a68e44c096)
![WhatsApp Image 2024-08-18 at 9 29 57 PM](https://github.com/user-attachments/assets/fb09ddb3-5f5e-40fa-acd2-e22f4752899a)
![WhatsApp Image 2024-08-18 at 9 29 57 PM (1)](https://github.com/user-attachments/assets/4c237fa3-d4f8-41ac-9916-b9e42de3c6de)
![WhatsApp Image 2024-08-18 at 9 29 56 PM (1)](https://github.com/user-attachments/assets/0373f790-a63b-42aa-9360-7b924854738a)
![WhatsApp Image 2024-08-18 at 9 29 58 PM](https://github.com/user-attachments/assets/7ef682ee-0865-4bbe-ae63-2e3cfaec367d)
![WhatsApp Image 2024-08-18 at 9 29 58 PM (1)](https://github.com/user-attachments/assets/eca32dbf-f5d0-480e-bf1b-82e2163d9943)

- **DRC clean**
![WhatsApp Image 2024-08-18 at 9 29 58 PM (2)](https://github.com/user-attachments/assets/2d412c9d-f397-4542-87e4-493723f88a72)
![WhatsApp Image 2024-08-18 at 9 29 59 PM](https://github.com/user-attachments/assets/bef67325-2e97-45fc-81ca-6ba2b1a71207)
![WhatsApp Image 2024-08-18 at 9 29 59 PM (1)](https://github.com/user-attachments/assets/eceb6db3-8a1d-4c7a-8817-dcd600b2d5c0)

- **Parasitics extraction**
![WhatsApp Image 2024-08-18 at 9 29 59 PM (2)](https://github.com/user-attachments/assets/ad3a1c99-0b09-4045-8d31-969a37121dfa)

# TritonRoute
Performs initial detail route.

Honors the preprocessed route guides (obtained after fast route),i.e., attempts as much as possible to route within route guides.

Assumes route guides for each net satisfy inter-guide connectivity.

Works on proposed MILP-based panel routing scheme with intra-layer parallel and inter-layer sequential routing framework.
![WhatsApp Image 2024-08-18 at 9 38 54 PM](https://github.com/user-attachments/assets/24ba85af-45c1-4ef3-a269-7112f102ebf4)

-> **Problem Statement:**

► INPUTS: LEF, DEF, Preprocessed route guides

► OUTPUT: Detailed routing solution with optimized wire-length and via count

► CONSTRAINTS: Route guide honoring, connectivity constraints and design rules
![WhatsApp Image 2024-08-18 at 9 40 51 PM](https://github.com/user-attachments/assets/4978afa3-f9d8-471a-be7c-f3ee7b91bd65)

# Maza routing rules
**Signal Integrity:** Maintain proper spacing and controlled impedance to minimize interference.

**Power Distribution:** Use wide traces and place decoupling capacitors close to power pins.

**Via Usage:** Minimize via use, and ensure appropriate sizes to reduce resistance.

**Layer Management:** Utilize multiple layers for signals, power, and ground to enhance performance.

**Trace Widths:** Design trace widths based on current and thermal needs.

**Design Rule Checks (DRCs):** Follow minimum width, spacing, and clearance rules to ensure manufacturability.

**Signal Routing Optimization:** Keep signal paths short and avoid narrow traces.

**Thermal Management:** Consider heat dissipation to avoid hot spots.

**Critical Signals:** Pay special attention to high-speed or sensitive signals, including differential pairs.

**Manufacturability:** Ensure the design is feasible for manufacturing and includes test points for verification.
