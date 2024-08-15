# parth_vlsi_workshop
# contents
1.Introduction

2.Day1-Introduction to open source eda tool(openlane) and PDK(skywater130nm) and synthesis of RTL

3.Day2-Floorplan and Powerplan.

4.Day3-Cell design using Magic Layout and Ngspice characterization.

5.Day4-Pre-layout timing analysis and importance to good clock tress(i.e minimum skewness).

6.Day5-Final steps for RTL2GDS flow.
# 1.Introduction
OpenLane is an open-source ASIC (Application-Specific Integrated Circuit) flow that facilitates the design and implementation of digital integrated circuits. It provides a complete RTL-to-GDSII (Register Transfer Level to Graphic Data System II) flow, leveraging various open-source EDA (Electronic Design Automation) tools. Developed by Efabless Corporation.
# 2.Day1-Introduction to open source EDA tool(openlane)
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
Calculate the flop ratio

flop ratio is : 1613/14876 = 0.1084 (10.84%)
![count flip flop](https://github.com/user-attachments/assets/933f0fab-cc51-4271-bb8f-b8894986c3b5)

