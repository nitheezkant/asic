<img width="1207" alt="Screenshot 2024-11-04 at 11 45 31 PM" src="https://github.com/user-attachments/assets/484bf1d9-5fdb-4ffc-a855-b1a13fd054e2">

# Task 1 
## Compiling a C program using GCC and RISC-V

### 1. Compiled C code using GCC

Wrote a simple c program and compliled it uising standard C compiler. This is shown in the below screenshot.


![WhatsApp Image 2024-08-08 at 12 58 12 AM](https://github.com/user-attachments/assets/dadfe501-57c0-471e-a89f-761435f1706b)


### 2. Compiled C code using RISCV compiler.

Next the same c file was comipled using RISCV compiler. The below command is used to do the same. 

```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

Next the follwing command is used to view the assembly level code of the same.

```
riscv64-unknown-elf-objdump -d sum1ton.o | less
```

The below screenshot shows the terminal excecution of the same.

![WhatsApp Image 2024-08-08 at 1 10 46 AM](https://github.com/user-attachments/assets/8d950175-1c82-4488-a23f-2440d26aa02b)

The below screenshot shows the main function of the program.

![WhatsApp Image 2024-08-08 at 1 43 57 AM](https://github.com/user-attachments/assets/dbabd528-d71d-4cc9-b0c4-73292376b4d5)
![WhatsApp Image 2024-08-08 at 1 44 57 AM](https://github.com/user-attachments/assets/7d44442d-aae2-40dc-9d85-dcd4272c2c91)


Next the following command is used to compile using the Ofast 
option.

```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

The main function is now seen to have lesser instruction as seen in the screenshot.


![WhatsApp Image 2024-08-08 at 1 31 26 AM](https://github.com/user-attachments/assets/ebc55c84-91a9-4bbf-9b95-4b2f9b8f0a9c)




# Task 2

## Viewing Program output and Debugging the program


### 1. Program Output


Once compiled using the RISCV compiler, the follwing command can be used to view the output. 

```
spike pk sum1ton.o
```

The follwing screenshot shows the result and verifies that both gcc and RISCV compiler give same output.

![WhatsApp Image 2024-08-08 at 3 12 35 AM](https://github.com/user-attachments/assets/ccd41dc6-cfb4-4f7b-b733-b62a9b8d0e2b)



## 2. DEBUGGING

To debug instruction by instruction, the follwing commands can be used to go to a perticular instruction and then excecute command by command. 

```
spike -d pk sum1ton.o
until pc 0 100b0
```

Further after each instruction the values of the registers can be obtained in the follwing way.

```
reg 0 a0
```

These are demonstrated in the below screenshot.

![Screenshot from 2024-08-08 02-20-30 (1)](https://github.com/user-attachments/assets/96270044-7944-4a86-a01c-5ac7fb7cf7df)


# Task 3

## Instruction type identification

The follwing table shows the analysis of the instructions given in the assignment.

| **Instruction**   | **Explanation**                                    | **Type** | **Hex Code** | **32-bit Format**                  |
|-------------------|---------------------------------------------------|----------|--------------|------------------------------------|
| **ADD r6, r7, r8** | Adds the values in r7 and r8, and stores the result in r6. | R-Type   | `0x00C38333` | `0000000 01000 00111 000 00110 0110011` |
| **SUB r8, r6, r7** | Subtracts the value in r7 from r6, and stores the result in r8. | R-Type   | `0x40E30333` | `0100000 00111 00110 000 01000 0110011` |
| **AND r7, r6, r8** | Performs a bitwise AND on r6 and r8, storing the result in r7. | R-Type   | `0x00C37333` | `0000000 01000 00110 111 00111 0110011` |
| **OR r8, r7, r5**  | Performs a bitwise OR on r7 and r5, storing the result in r8. | R-Type   | `0x00A3A333` | `0000000 00101 00111 110 01000 0110011` |
| **XOR r8, r6, r4** | Performs a bitwise XOR on r6 and r4, storing the result in r8. | R-Type   | `0x00A32333` | `0000000 00100 00110 100 01000 0110011` |
| **SLT r10, r2, r4** | Sets r10 to 1 if r2 is less than r4, otherwise sets it to 0. | R-Type  | `0x00A10333` | `0000000 00100 00010 010 01010 0110011` |
| **ADDI r12, r3, 5** | Adds the immediate value 5 to r3, storing the result in r12. | I-Type  | `0x00518193` | `000000000101 00011 000 01100 0010011`  |
| **SW r3, r1, 4**   | Stores the word in r3 at the memory address calculated as r1 + 4. | S-Type   | `0x00418223` | `0000000 00100 00011 010 00001 0100011` |
| **SRL r16, r11, r2** | Performs a logical right shift on r11 by the number of bits specified in r2, storing the result in r16. | R-Type | `0x0025B393` | `0000000 00010 01011 101 10000 0110011` |
| **BNE r0, r1, 20** | Branches to the address PC + 20 if r0 is not equal to r1. | B-Type   | `0x00A0B0E3` | `0000000 01010 00001 001 00000 1100011` |
| **BEQ r0, r0, 15** | Branches to the address PC + 15 if r0 is equal to r0. | B-Type   | `0x00F08063` | `0000000 01111 00000 000 00000 1100011` |
| **LW r13, r11, 2** | Loads the word from the memory address calculated as r11 + 2 into r13. | I-Type   | `0x0025A293` | `000000000010 01011 010 01101 0000011`  |
| **SLL r15, r11, r2** | Performs a logical left shift on r11 by the number of bits specified in r2, storing the result in r15. | R-Type | `0x0025D193` | `0000000 00010 01011 001 01111 0110011` |


##Waveform generation

### Hardcoded instruction's waveform screenshot is given below:

`ADD R6, R2, R1`


![1](https://github.com/user-attachments/assets/65d3cc6d-3117-4f15-b9e3-d2ac11155402)

`SUB R7, R1, R2`

![Screenshot from 2024-08-13 14-13-27](https://github.com/user-attachments/assets/d10b1df6-22be-40be-84a0-9bf05a92c0d9)


`AND R8, R1, R3`

![3](https://github.com/user-attachments/assets/6db988b3-68cc-43b2-b9a8-f5b902b2dcb5)


`OR R9, R2, R5`

![4 (1)](https://github.com/user-attachments/assets/e9c4415b-c5bd-4ec7-8550-fa2be426733e)


`XOR R10, R1, R4`

![5](https://github.com/user-attachments/assets/58ace97c-f3b3-44f3-b86d-c84a11553560)


`SLT R1, R2, R4`

![6](https://github.com/user-attachments/assets/1296dce0-1043-4489-ad2e-46ec68de73d7)


`ADDI R12, R4, 5`


![7](https://github.com/user-attachments/assets/f37bca18-fa93-4bdb-b082-46a65577422e)

`BEQ R0, R0, 15`
![8](https://github.com/user-attachments/assets/195784f8-a318-4170-bd81-af43b6a6f77f)



`SW R3, R1, 2`

![9](https://github.com/user-attachments/assets/0c257e75-eafd-4b64-91df-90cb9354c706)


`LW R13, R1, 2`


![Screenshot from 2024-08-13 14-35-17](https://github.com/user-attachments/assets/cc2d7115-4e90-453c-b60d-b2c1a048e1a9)


# Task 4

The screenshot shows the following:-

1) A C code implementing Insertion sort.
  
2) The output as generated by gcc compiler.

3) The output by RISC-V (OFast) compiler, which is seen to be same as the gcc compiler.

<img width="737" alt="Screenshot 2024-08-15 at 1 49 19 AM" src="https://github.com/user-attachments/assets/edb16809-50cd-4839-9793-7ca3f185e46d">

# Task 5

Baisc Risc-V processor core using TL-Verilog on Makerchip.

## Given below are the screenshots of the code.


<img width="1075" alt="Screenshot 2024-08-21 at 11 22 34 PM" src="https://github.com/user-attachments/assets/9be62c7a-0500-45f7-af59-dd927d79ec33">
<img width="1194" alt="Screenshot 2024-08-21 at 11 22 52 PM" src="https://github.com/user-attachments/assets/16c3ed7b-3c5c-4554-a107-4ca2d59e900b">
<img width="1323" alt="Screenshot 2024-08-21 at 11 23 05 PM" src="https://github.com/user-attachments/assets/6f16849e-99c6-462f-a594-f73626b4e14b">
<img width="1386" alt="Screenshot 2024-08-21 at 11 23 22 PM" src="https://github.com/user-attachments/assets/7b036a40-d970-4fd3-a6fb-64ee159cf863">
<img width="1317" alt="Screenshot 2024-08-21 at 11 23 32 PM" src="https://github.com/user-attachments/assets/22ff1c44-c215-4a9e-9483-cea3da36ecee">

## Generated diagram

<img width="734" alt="Screenshot 2024-08-21 at 11 14 38 PM" src="https://github.com/user-attachments/assets/a61f4f03-bfbe-4dc0-9b16-4b4c69c31f3e">

## Generated visual

<img width="717" alt="Screenshot 2024-08-21 at 11 20 16 PM" src="https://github.com/user-attachments/assets/dddc4d6a-f605-4bf5-91f9-ac2b7f1fc322">

## Generated log

<img width="1615" alt="Screenshot 2024-08-21 at 11 19 04 PM" src="https://github.com/user-attachments/assets/0395ec41-1450-468e-84ae-9edaf7e38ae4">

## Test bench

<img width="577" alt="Screenshot 2024-08-21 at 11 19 52 PM" src="https://github.com/user-attachments/assets/0bbdd007-73c6-492e-8189-a5bc68a20ea1">

## Waveform with clock named $clk_nit

<img width="766" alt="Screenshot 2024-08-21 at 11 21 21 PM" src="https://github.com/user-attachments/assets/27c3b258-9649-4a62-8e8b-175b451639ae">

## Screenshot of /xreg[14] during all iterations of summing

<img width="1619" alt="Screenshot 2024-08-21 at 11 27 19 PM" src="https://github.com/user-attachments/assets/dd7f1af1-b882-4412-a643-63cdb00baec9">
<img width="1609" alt="Screenshot 2024-08-21 at 11 27 49 PM" src="https://github.com/user-attachments/assets/b561ca88-c133-4b5f-84c2-78187da1b22c">
<img width="1084" alt="Screenshot 2024-08-21 at 11 28 20 PM" src="https://github.com/user-attachments/assets/ff9bc241-c7bd-4d69-b236-17b99a05de83">


# Task 6

Run the following commands to convert the .tlv file to .v file.

![WhatsApp Image 2024-08-27 at 8 05 41 AM](https://github.com/user-attachments/assets/be883d34-9761-4400-8e09-ae21fe30b23c)

The following screenshot shows the .v file generated. 
![WhatsApp Image 2024-08-27 at 8 04 57 AM](https://github.com/user-attachments/assets/e98affa3-4333-418b-ac9a-2a0b3048de12)

Now using GTKWave the waveform can be seen. Screenshot of the same is attached below with the clock name clk_nit.
![WhatsApp Image 2024-08-27 at 8 03 43 AM](https://github.com/user-attachments/assets/db9868a5-b5e5-4b36-8f46-eeb2247d9af5)

This can now be compared to the makerchip waveform given below.
<img width="1619" alt="Screenshot 2024-08-21 at 11 27 19 PM" src="https://github.com/user-attachments/assets/dd7f1af1-b882-4412-a643-63cdb00baec9">
<img width="1609" alt="Screenshot 2024-08-21 at 11 27 49 PM" src="https://github.com/user-attachments/assets/b561ca88-c133-4b5f-84c2-78187da1b22c">
<img width="1084" alt="Screenshot 2024-08-21 at 11 28 20 PM" src="https://github.com/user-attachments/assets/ff9bc241-c7bd-4d69-b236-17b99a05de83">

local simulation
<img width="1440" alt="Screenshot 2024-09-14 at 1 07 13 AM" src="https://github.com/user-attachments/assets/3c2f80a0-2ae9-4e89-a051-8a8fda52418b">

# Slides for Task of 3rd September 

[Nitheezkant_R.pdf](https://github.com/user-attachments/files/16999251/Your.title.here.pdf)


# Video (Private)

https://drive.google.com/file/d/1etW8sFwG9FU7RaxZOxfgOIVtonqyHWGz/view?usp=sharing

# Task 7

To Synthesize RISC-V and compare output with functional simulations.

Copy the src folder from your VSDBabySoC folder to sky130RTLDesignAndSynthesisWorkshop.

## Synthesis: 

Enter the following commands

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog clk_gate.v
read_verilog rvmyth.v
synth -top rvmyth
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr rvmyth_net.v
!gedit rvmyth_net.v
exit

```
<img width="1680" alt="Screenshot 2024-11-04 at 7 59 25 PM" src="https://github.com/user-attachments/assets/b8a4ca01-8a21-4caa-81b8-40d358570ca2">
<img width="1680" alt="Screenshot 2024-11-04 at 8 00 07 PM" src="https://github.com/user-attachments/assets/8076c654-3a03-4a8c-a057-ded49953a42e">

### Simulation

Enter the following commands

```
iverilog ../../my_lib/verilog_model/primitives.v ../../my_lib/verilog_model/sky130_fd_sc_hd.v rvmyth.v testbench.v vsdbabysoc.v avsddac.v avsdpll.v clk_gate.v
./a.out
gtkwave dump.vcd
```

<img width="1680" alt="Screenshot 2024-11-04 at 8 36 42 PM" src="https://github.com/user-attachments/assets/fdccaa89-649b-414b-99ee-817656c6bc0b">

## Functional Simulation:

Enter the following commands

 ```
cd ~
cd VSDBabySoC
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```

<img width="1680" alt="Screenshot 2024-11-04 at 8 38 16 PM" src="https://github.com/user-attachments/assets/dd591c7c-9f86-4dc6-bf52-b053e61b1780">


## Comparision of waveforms

Here is clear comparion of waveform, verfing that the waveform is the same.

<img width="1680" alt="Screenshot 2024-11-04 at 8 37 45 PM" src="https://github.com/user-attachments/assets/57d08924-bf21-415c-94ff-f3f848a6719c">

# Task 8 

Post Synthesis Static Timing Analysis using OpenSTA.

Change the of VSDBabySoc/src/sdc/vsdbabysoc_synthesis.sdc to:

```
set PERIOD 11.45
set_units -time ns
create_clock [get_pins {pll/CLK}] -name clk -period $PERIOD
set_clock_uncertainty -setup  [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_transition [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_uncertainty -hold [expr $PERIOD * 0.08] [get_clocks clk]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_CP]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_VCO]
set_input_transition [expr $PERIOD * 0.08] [get_ports REF]
set_input_transition [expr $PERIOD * 0.08] [get_ports VCO_IN]
set_input_transition [expr $PERIOD * 0.08] [get_ports VREFH]
```

<img width="1680" alt="Screenshot 2024-11-04 at 10 11 56 PM" src="https://github.com/user-attachments/assets/9021a8c2-da82-4121-9a52-494598c95d70">

Enter the following commands

```
cd VSDBabySoc/src
sta
read_liberty -min ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -min ./lib/avsdpll.lib
read_liberty -min ./lib/avsddac.lib
read_liberty -max ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max ./lib/avsdpll.lib
read_liberty -max ./lib/avsddac.lib
read_verilog ../output/synth/vsdbabysoc.synth.v
link_design vsdbabysoc
read_sdc ./sdc/vsdbabysoc_synthesis.sdc
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

Hold 

<img width="1479" alt="Screenshot 2024-11-04 at 10 04 50 PM" src="https://github.com/user-attachments/assets/d4119cec-8c27-4070-89aa-909e7a1deeee">

Setup

<img width="1081" alt="Screenshot 2024-11-04 at 10 05 06 PM" src="https://github.com/user-attachments/assets/713270ee-8568-4111-953d-1be8d729e3c3">

# Task 9

Post Synthesis Static Timing Analysis using OpenSTA for all the sky130 lib files

Create a sta_pvt.tcl file and copy the Following

```
set list_of_lib_files(1) "sky130_fd_sc_hd__ff_100C_1v65.lib"
set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v95.lib"
set list_of_lib_files(3) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v95.lib"
set list_of_lib_files(7) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part1"
set list_of_lib_files(8) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part2"
set list_of_lib_files(9) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part3"
set list_of_lib_files(10) "sky130_fd_sc_hd__ss_100C_1v40.lib"
set list_of_lib_files(11) "sky130_fd_sc_hd__ss_100C_1v60.lib"
set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
set list_of_lib_files(14) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
set list_of_lib_files(15) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
set list_of_lib_files(16) "sky130_fd_sc_hd__ss_n40C_1v60.lib"
set list_of_lib_files(17) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part1"
set list_of_lib_files(18) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part2"
set list_of_lib_files(19) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part3"
set list_of_lib_files(20) "sky130_fd_sc_hd__ss_n40C_1v76.lib"
set list_of_lib_files(21) "sky130_fd_sc_hd__tt_025C_1v80.lib"
set list_of_lib_files(22) "sky130_fd_sc_hd__tt_100C_1v80.lib"

for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
read_liberty ./timing_libs/$list_of_lib_files($i)
read_verilog ../output/synth/vsdbabysoc.synth.v
link_design vsdbabysoc
read_sdc ./sdc/vsdbabysoc_synthesis.sdc
check_setup -verbose
report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > ./sta_output/min_max_$list_of_lib_files($i).txt

}
```

<img width="1680" alt="Screenshot 2024-11-04 at 10 40 54 PM" src="https://github.com/user-attachments/assets/9756bc48-7012-4623-9cf1-86f3a04ff936">

Enter the following commands

```
cd VSDBabySoC/src
sta
source sta_pvt.tcl
```

<img width="1680" alt="Screenshot 2024-11-04 at 10 43 58 PM" src="https://github.com/user-attachments/assets/54dba85b-b041-40b0-bb60-0e7b01256d0f">

Generated Files:

<img width="1680" alt="Screenshot 2024-11-04 at 10 44 49 PM" src="https://github.com/user-attachments/assets/d9b5fb2d-b986-48ac-8b79-ba45b2896ac0">

One of them:

<img width="1680" alt="Screenshot 2024-11-04 at 10 47 36 PM" src="https://github.com/user-attachments/assets/eee80739-5991-4946-86d2-5646f47799e9">

All values transfered to excel:

<img width="977" alt="Screenshot 2024-11-04 at 11 25 48 PM" src="https://github.com/user-attachments/assets/871c2156-3cc5-49f2-bc34-97f4062bb4d6">

Graphs:

<img width="1211" alt="Screenshot 2024-11-04 at 11 40 51 PM" src="https://github.com/user-attachments/assets/70407b2d-f33f-476e-9f36-f773b1ae8eb9">

<img width="1207" alt="Screenshot 2024-11-04 at 11 45 31 PM" src="https://github.com/user-attachments/assets/d1a89d02-886a-4c53-8922-6b9872360e93">

# Task 10



# Day 1



**QFN-48 Package**: The QFN-48 is a small, leadless package featuring 48 connection pads around its edge, offering superior thermal and electrical performance, making it well-suited for high-density applications.



![image](https://github.com/user-attachments/assets/16181d9a-b323-4d03-b7ca-c8128211a197)

![image](https://github.com/user-attachments/assets/322fa2e2-b826-47b9-a309-96f7a855f8b4)


A **Chip**, also known as an integrated circuit (IC), is composed of various functional components—such as memory, processing units, and input/output (I/O) interfaces—integrated into a silicon base. Chips are designed for specific electronic functions, including processing, data storage, communication, and control.

**Pads**: Small metal contact points on a chip or its package, used to link the internal circuitry to external connections, allowing for signal transmission.

**Core**: The primary processing unit within a chip, housing the functional logic optimized for performance and power efficiency.

**Die**: The part of a silicon wafer that holds a single IC before it is packaged, containing all the active circuitry of the chip.

### From Software Applications to Hardware Execution

For an application to run on hardware, the software must be converted from a high-level programming language into binary code that the hardware can understand:


![image](https://github.com/user-attachments/assets/7aea1b28-4cc7-412a-8cb9-f239140808fb)


1. **System Software Translation**: The system software layer converts high-level code into machine language. The Operating System (OS), compiler, and assembler are integral to this conversion process.

2. **Execution Process**:
   - The **OS** interprets and organizes high-level application functions written in languages such as C, C++, or Java.
   - The **Compiler** translates the high-level code into low-level, architecture-specific instructions optimized for the hardware being used (e.g., x86, ARM, RISC-V).
   - The **Assembler** then transforms these instructions into binary (machine code) that the hardware can understand and execute.
   - The **Hardware** ultimately runs these instructions, carrying out the tasks as specified by the program.

![image](https://github.com/user-attachments/assets/4f593b79-d6b1-496c-8231-fa017b4bc7ce)

**Example**: Take a stopwatch application running on a RISC-V core as an example. The OS processes a function written in C, which is then compiled into RISC-V-specific assembly instructions. The assembler translates these into binary code, and the hardware executes it, delivering the stopwatch functionality.

![image](https://github.com/user-attachments/assets/3d7f7f44-a1ae-4605-9e2c-5b2fe3206022)

3. **Hardware Translation to Layout**: In hardware design, the RTL (Register Transfer Level) defines the functionality using an HDL (Hardware Description Language) like Verilog. This is then synthesized into a netlist of gates, which are subsequently mapped onto a physical layout, ultimately forming the chip.

---

### ASIC Design Flow Overview

The process of designing an ASIC (Application-Specific Integrated Circuit) involves multiple stages, progressing from a high-level description to a final physical layout ready for fabrication:

![image](https://github.com/user-attachments/assets/a7589d94-48cd-4e09-92fd-38594a79c7a9)

1. **RTL Design**: Specifies the intended logic and functionality of the circuit in Verilog or VHDL. This high-level code outlines data paths, logic operations, and the interactions between different chip components.

2. **RTL Synthesis**: Converts the RTL code into a gate-level netlist, which includes standard cells such as AND gates, multiplexers, and flip-flops. Optimization steps focus on area, power, and timing constraints to ensure efficient performance.

3. **Floor and Power Planning**: This phase involves arranging the major functional blocks of the chip on the silicon die and defining the power distribution network. Proper floorplanning minimizes signal delays and enhances power efficiency by positioning components optimally.

4. **Placement**: Determines the physical locations of all cells and modules, minimizing wiring length and ensuring compliance with design constraints. Optimal placement balances performance, area, and power.

5. **Clock Tree Synthesis (CTS)**: CTS designs a clock distribution network to uniformly deliver the clock signal to all registers and flip-flops, minimizing clock skew and ensuring accurate timing across the chip.

6. **Routing**: Connects all components using metal layers, focusing on signal integrity and minimizing congestion. Routing tools prioritize paths that reduce resistance and signal delay while adhering to design rules.

7. **Sign-off**: This phase verifies the design for functionality, performance, power consumption, and manufacturability. Checks include timing analysis (ensuring setup and hold times are met), power analysis, and physical verification to confirm compliance with manufacturing constraints.

8. **GDSII File Generation**: The final layout is exported in the GDSII format, which serves as the blueprint for chip manufacturing. The GDSII file contains all necessary information to create the photomasks for the chip fabrication process.

---

### OpenLane ASIC Flow

OpenLane is an open-source ASIC design flow that integrates various open-source tools for each stage of the ASIC development process:

![image](https://github.com/user-attachments/assets/914dcbf2-4303-42ed-bbc4-38f29b621be4)

1. **RTL Synthesis, Technology Mapping, and Formal Verification**: Yosys is used for RTL synthesis, ABC handles technology mapping and formal verification.
2. **Static Timing Analysis**: OpenSTA is used to perform timing verification.
3. **Floor Planning**: Tools include init_fp for initial floor planning, ioPlacer for I/O placement, pdn for power grid planning, and tapcell for inserting tap cells to manage well contacts.
4. **Placement**: This step includes global placement with RePLace, optional cell resizing with Resizer, and detailed placement using OpenDP.
5. **Clock Tree Synthesis**: TritonCTS is used to build a balanced clock tree.
6. **Fill Insertion**: OpenDP manages the insertion of filler cells to ensure uniform chip density.
7. **Routing**: FastRoute handles global routing, while TritonRoute performs detailed routing for the chip.
8. **SPEF Extraction**: OpenRCX extracts Standard Parasitic Exchange Format (SPEF) data used for timing analysis.
9. **GDSII Streaming Out**: Magic and KLayout are used to generate and visualize the final layout.
10. **Design Rule Checking (DRC)**: Magic and KLayout also perform design rule checks to verify the design adheres to manufacturing constraints.
11. **Layout vs. Schematic (LVS) Check**: Netgen ensures the layout matches the schematic for consistency.
12. **Antenna Checks**: Magic checks for antenna effects, ensuring the design is reliable.

---

### OpenLane Directory Structure

The OpenLane directory structure is designed to facilitate open-source ASIC design, supporting PDK (Process Design Kit) integration:

```
├── OpenLane             -> Main directory to invoke tools (run docker first)
│   ├── designs          -> Holds all design files for the flow
│   │   ├── picorv32a    -> Example design used in workshops or tutorials
│   │   ├── ...          -> Additional designs
├── pdks                 -> Stores PDK-related files, supporting open-source tools
│   ├── skywater-pdk     -> Contains the Skywater 130nm PDK
│   ├── open-pdks        -> Scripts to adapt commercial PDKs for open-source tools
│   ├── sky130A          -> Variant of PDK with open-source compatibility
│   │   ├── libs.ref     -> Node-specific files (e.g., timing libraries, cell LEF files)
│   │   ├── libs.tech    -> Tool-specific files for KLayout, Netgen, Magic, etc.
```


This directory structure ensures compatibility with open-source EDA tools by organizing files specific to each design, technology node, and tool.

### OpenLane Synthesis Process for `picorv32a` Design

### **1. Open the OpenLane Directory**
   - Navigate to the OpenLane working directory within the VSD Virtual Box:
     ```bash
     cd Desktop/work/tools/openlane_working_dir/openlane
     docker
     ./flow.tcl -interactive
     ```

### **2. Launch OpenLane in Interactive Mode**
   - Start the Docker container and enter OpenLane's interactive mode:
     ```bash
     package require openlane 0.9
     prep -design picorv32a
     run_synthesis
     ```
![Screenshot 2024-11-13 135630](https://github.com/user-attachments/assets/09577795-96cf-4dfb-ab95-eba7f7723a0b)

### Viewing the Netlist
   - After synthesis completes, go to the folder containing the netlist:
     ```bash
     cd designs/picorv32a/runs/13-11_15-43/results/synthesis/
     gedit picorv32a.synthesis.v
     ```
---
![Screenshot 2024-11-13 140133](https://github.com/user-attachments/assets/6e6e3b04-bcfd-43ab-bb71-6e2c9d0b67a7)

### Viewing the Yosys Report
```bash
cd ../..
cd reports/synthesis
gedit 1-yosys_4.stat.rpt
```

![Screenshot 2024-11-13 140451](https://github.com/user-attachments/assets/dd672aa4-5b7b-46ba-b504-7fa4c4c38458)

28. Printing statistics.


```

=== picorv32a ===

   Number of wires:              14596
   Number of wire bits:          14978
   Number of public wires:        1565
   Number of public wire bits:    1947
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:              14876
     sky130_fd_sc_hd__a2111o_2       1
     sky130_fd_sc_hd__a211o_2       35
     sky130_fd_sc_hd__a211oi_2      60
     sky130_fd_sc_hd__a21bo_2      149
     sky130_fd_sc_hd__a21boi_2       8
     sky130_fd_sc_hd__a21o_2        57
     sky130_fd_sc_hd__a21oi_2      244
     sky130_fd_sc_hd__a221o_2       86
     sky130_fd_sc_hd__a22o_2      1013
     sky130_fd_sc_hd__a2bb2o_2    1748
     sky130_fd_sc_hd__a2bb2oi_2     81
     sky130_fd_sc_hd__a311o_2        2
     sky130_fd_sc_hd__a31o_2        49
     sky130_fd_sc_hd__a31oi_2        7
     sky130_fd_sc_hd__a32o_2        46
     sky130_fd_sc_hd__a41o_2         1
     sky130_fd_sc_hd__and2_2       157
     sky130_fd_sc_hd__and3_2        58
     sky130_fd_sc_hd__and4_2       345
     sky130_fd_sc_hd__and4b_2        1
     sky130_fd_sc_hd__buf_1       1656
     sky130_fd_sc_hd__buf_2          8
     sky130_fd_sc_hd__conb_1        42
     sky130_fd_sc_hd__dfxtp_2     1613
     sky130_fd_sc_hd__inv_2       1615
     sky130_fd_sc_hd__mux2_1      1224
     sky130_fd_sc_hd__mux2_2         2
     sky130_fd_sc_hd__mux4_1       221
     sky130_fd_sc_hd__nand2_2       78
     sky130_fd_sc_hd__nor2_2       524
     sky130_fd_sc_hd__nor2b_2        1
     sky130_fd_sc_hd__nor3_2        42
     sky130_fd_sc_hd__nor4_2         1
     sky130_fd_sc_hd__o2111a_2       2
     sky130_fd_sc_hd__o211a_2       69
     sky130_fd_sc_hd__o211ai_2       6
     sky130_fd_sc_hd__o21a_2        54
     sky130_fd_sc_hd__o21ai_2      141
     sky130_fd_sc_hd__o21ba_2      209
     sky130_fd_sc_hd__o21bai_2       1
     sky130_fd_sc_hd__o221a_2      204
     sky130_fd_sc_hd__o221ai_2       7
     sky130_fd_sc_hd__o22a_2      1312
     sky130_fd_sc_hd__o22ai_2       59
     sky130_fd_sc_hd__o2bb2a_2     119
     sky130_fd_sc_hd__o2bb2ai_2     92
     sky130_fd_sc_hd__o311a_2        8
     sky130_fd_sc_hd__o31a_2        19
     sky130_fd_sc_hd__o31ai_2        1
     sky130_fd_sc_hd__o32a_2       109
     sky130_fd_sc_hd__o41a_2         2
     sky130_fd_sc_hd__or2_2       1088
     sky130_fd_sc_hd__or2b_2        25
     sky130_fd_sc_hd__or3_2         68
     sky130_fd_sc_hd__or3b_2         5
     sky130_fd_sc_hd__or4_2         93
     sky130_fd_sc_hd__or4b_2         6
     sky130_fd_sc_hd__or4bb_2        2

   Chip area for module '\picorv32a': 147712.918400


```

# Day 2 

## **Core Concepts in IC Floorplanning**

### 1. **Utilization Factor**
The utilization factor is a crucial metric that compares the area occupied by the circuit (netlist) to the total core area of the chip. A higher utilization means more of the chip's area is used effectively, but over-utilization can lead to issues with routing and insufficient space for other essential components.

Ideally, the utilization factor would be 1 (100%), but in practice, a range of **0.5 to 0.6** is preferred to allow for buffer zones, routing channels, and the flexibility needed for adjustments.

#### **Utilization Factor Formula**:
$$
\text{Utilization Factor} = \frac{\text{Area Occupied by Netlist}}{\text{Total Core Area}}
$$

### 2. **Aspect Ratio**
The aspect ratio defines the shape of the chip, calculated as the ratio of its height to width. An **aspect ratio of 1** results in a square shape, while any other value produces a rectangular layout. The ideal aspect ratio is influenced by factors like functionality, packaging, and manufacturing constraints.

#### **Aspect Ratio Formula**:
$$
\text{Aspect Ratio} = \frac{\text{Height}}{\text{Width}}
$$

### **Pre-Placed Cells**
Pre-placed cells are critical functional blocks, such as memory units, custom processors, and analog circuits, that are manually positioned in fixed locations during the floorplanning phase. These blocks are **vital to the chip's operation** and must remain in place during the placement and routing stages to ensure the chip functions correctly.

### **Decoupling Capacitors**
- **Purpose**: These capacitors are placed close to logic circuits to **smooth out power supply fluctuations** during high-speed switching events.
- **Benefits**:
  - Minimize **voltage fluctuations**
  - Reduce **electromagnetic interference (EMI)**
  - Ensure **reliable power delivery**, particularly to sensitive circuits

### **Power Planning**
Effective power planning in an IC ensures that **VDD and VSS** are evenly distributed across the chip through a **power mesh**. The goal is to maintain a stable power supply, minimize **voltage drops**, and optimize the chip’s overall **power efficiency**. Increasing the number of power and ground points reduces the risk of instability.

### **Pin Placement**
Proper placement of **I/O pins** is critical to the chip’s performance. Careful distribution of these pins helps to minimize signal integrity issues and reduces heat buildup, both of which contribute to the chip’s overall stability and manufacturability.

---

## **Floorplanning with OpenLANE**

### 1. **Set Up OpenLANE**
Begin by navigating to the OpenLANE directory and starting the interactive session:

```bash
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```
### 2. **Run OpenLANE Flow**
To prepare the design (`picorv32a`) and begin the floorplanning process, execute the following commands:
```bash
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
```
![Screenshot 2024-11-13 141151](https://github.com/user-attachments/assets/762ce589-7b2f-4614-beca-846ddc2b6ec3)
![Screenshot 2024-11-13 141232](https://github.com/user-attachments/assets/cee062c8-36fe-45d1-8c60-f26d825ac8dd)

#### **Floorplan Results**:
After running the commands, the floorplan results will be generated and saved in the OpenLANE output directory. You can visualize and analyze the results from there.

### 3. **Floorplan Definition**
Once the floorplan has been generated, you can inspect the `.def` file, which contains the detailed floorplan information:
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_15-48/results/floorplan/
gedit picorv32a.floorplan.def
```

![Screenshot 2024-11-13 143148](https://github.com/user-attachments/assets/311d2b28-f008-4a64-83e1-ad2021f21123)

#### **Floorplan Calculation**:
- **Unit Distance**: 1 micron = 1000 unit distance
- **Die Dimensions**:
  - **Width**: 660,685 unit distance → 660.685 microns
  - **Height**: 671,405 unit distance → 671.405 microns
- **Area of the Die**: 660.685 × 671.405 = 443,587.212 µm²

### 4. **View Floorplan in Magic**
To visualize the floorplan, use Magic:
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_15-48/results/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
#### **Floorplan Visualizations**:
Once the command runs, you’ll see a graphical representation of the chip layout in Magic, which shows how cells and components are placed.

![Screenshot 2024-11-13 143259](https://github.com/user-attachments/assets/fb1a5892-0a8d-48ea-ae08-f9e174b31532)

---

## **Decap and Tap Cells**

- **Decap Cells**: These cells are placed near logic cells to handle transient power supply fluctuations and stabilize the power delivery network. They help maintain consistent voltage levels during switching events.

- **Tap Cells**: These are used to **connect to the power grid** and reduce **substrate noise** that can interfere with the chip's performance. Tap cells improve power distribution and minimize noise coupling within the substrate.
- 
![Screenshot 2024-11-13 144328](https://github.com/user-attachments/assets/98c243eb-3e75-4bde-84f5-a3cfc8cdcf7e)

---

## **Placement Process**

### 1. **Unplaced Standard Cells**
At the beginning of the placement process, cells are unplaced and located at the origin. These cells are not yet assigned specific positions and will be moved to their designated locations during the placement phase.

![Screenshot 2024-11-13 144647](https://github.com/user-attachments/assets/c6ae7df7-5dd4-416d-b0d3-88cc13a5b514)

### 2. **Run Placement**
Once floorplanning is complete, execute the placement step to arrange the cells:
```bash
run_placement
```
### 3. **View Placement in Magic**
Once placement is complete, you can view the result using Magic:

```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/13-11_15-48/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![Screenshot 2024-11-13 145351](https://github.com/user-attachments/assets/9d13bc37-afe1-49bf-9b71-16636f4b1b50)


#### **Placement Visualizations**:
After executing the command, you will be able to see the visual representation of how the standard cells are arranged on the chip layout in Magic. This provides a clear view of the cell placement and their relative positions within the chip design.
![Screenshot 2024-11-13 145447](https://github.com/user-attachments/assets/3b1701be-9cb8-47bf-8af3-eab5977904a8)

---

## **Cell Design and Characterization Flow**

### 1. **Library Cells**
A library consists of cells that define various functionalities, sizes, and electrical thresholds. These cells serve as the fundamental building blocks for creating an integrated circuit (IC).

### 2. **Design Flow**:
- **Inputs**: The design flow begins with inputs such as PDKs (Process Design Kits), SPICE models, DRC (Design Rule Check) and LVS (Layout vs. Schematic) checks, along with user-defined specifications.
- **Steps**:
  - **Circuit Design**: Define the logic and functionality of the circuit.
  - **Layout Design**: Create the physical layout of the circuit based on the circuit design.
  - **Parasitic Extraction**: Extract parasitic elements (e.g., capacitance, resistance) from the layout to model their impact on circuit performance.
  - **Characterization**: Analyze the circuit’s timing, noise, and power characteristics to ensure it meets performance and reliability requirements.
- **Outputs**:
  - **CDL (Circuit Description Language)**, **LEF (Library Exchange Format)**, **GDSII** (a file format for chip layout), **SPICE Netlist**, and various characterization files like `.lib` for timing, noise, and power.

---

## **Standard Cell Characterization Flow**

### 1. **Steps in Characterization**:
- **Load Models and Tech Files**: These files provide process-specific details, including the behavior of devices and design rules.
- **Extract Spice Netlist**: The circuit netlist is extracted from the design to enable detailed electrical analysis.
- **Characterization with GUNA**: Using characterization tools like GUNA, the following models are generated:
  - **Timing Models**: These describe the delays and propagation times for signals through the circuit.
  - **Power Models**: These models estimate the power consumption of the circuit during operation.
  - **Noise Models**: These models assess the noise characteristics and their impact on signal integrity.

---

## **Timing Parameters**

| **Timing Parameter**         | **Value**          |
|------------------------------|--------------------|
| **Slew Low Rise Threshold**   | 20%                |
| **Slew High Rise Threshold**  | 80%                |
| **Slew Low Fall Threshold**   | 20%                |
| **Slew High Fall Threshold**  | 80%                |
| **Input Rise Threshold**      | 50%                |
| **Input Fall Threshold**      | 50%                |
| **Output Rise Threshold**     | 50%                |
| **Output Fall Threshold**     | 50%                |

### **Propagation Delay**:
Propagation delay refers to the time it takes for an input signal to propagate through a logic gate or circuit and impact the output signal.

$$
\text{Rise Delay} = \text{time(out-fall-thr)} - \text{time(in-rise-thr)}
$$

### **Transition Time**:
Transition time is the time required for a signal to transition between logic levels. It is typically measured between **10% and 90%** or **20% and 80%** of the signal’s full swing.

$$
\text{Fall Transition Time} = \text{time(slew-high-fall-thr)} - \text{time(slew-low-fall-thr)}
$$

$$
\text{Rise Transition Time} = \text{time(slew-high-rise-thr)} - \text{time(slew-low-rise-thr)}
$$

# Day 3 

A CMOS inverter, consisting of a PMOS and NMOS transistor, is one of the fundamental components in digital circuits. The circuit switches between high and low output states based on the input voltage level. This guide includes details on how to model and simulate this behavior in SPICE.

---

## SPICE Deck Structure

### 1. **Netlist Creation**

The netlist defines the interconnections between the components (PMOS and NMOS transistors) in the inverter circuit. Below is a sample netlist structure for a CMOS inverter with labeled nodes for easy identification:

- **Input Node:** Input signal (IN)
- **Output Node:** Output of the inverter (OUT)
- **Power Supply Node:** Connected to VDD
- **Ground Node:** Connected to GND

Example of transistor description syntax:
```spice
[component name] [drain] [gate] [source] [substrate] [transistor type] W=[width] L=[length]
```

### 2. **Device Sizing**

The width-to-length (W/L) ratio of the PMOS and NMOS transistors is a critical factor in determining the drive strength and performance of a CMOS inverter. To ensure proper switching behavior, it's important to size the transistors appropriately. Typically, the PMOS transistor is sized with a **W/L ratio 2x to 3x** greater than the NMOS transistor to account for the different mobility of electrons and holes in the materials.

Example transistor sizing:

```spice
M1 OUT IN VDD VDD PMOS W=2u L=0.25u
M2 OUT IN GND GND NMOS W=1u L=0.25u
```
### 3. **Voltage Levels**

Define the gate input voltage and supply voltage (VDD). Modify the levels to match the design specifications; here, we use 2.5V as the supply voltage reference.

Example:
```spice
Vin IN 0 DC 0V
VDD VDD 0 DC 2.5V
```

### 4. **Node Naming**

Assign descriptive names to nodes in the netlist, such as `VDD`, `GND`, `IN`, and `OUT`, to help SPICE reference and simulate each component clearly.

![image](https://github.com/user-attachments/assets/bb9e2ba0-5180-436b-8749-24a7a49b1cdd)

---

## Model File

Include the MOSFET model file specific to the fabrication technology. For instance, `tsmc_025um_model.mod` contains parameters for 0.25µm technology.

Example:
```spice
.include tsmc_025um_model.mod
```

---

## Simulation Commands

### 1. **DC Analysis: Switching Threshold**

The switching threshold (Vm) is a key voltage level where the inverter transitions between logic high and low states. Vm is identified when both transistors enter the saturation region, causing high leakage current due to concurrent conduction.

#### Simulation Steps
- **Load the Circuit**: Load the SPICE deck with the `.cir` extension.
- **Run DC Analysis**: Perform a voltage sweep from 0V to 2.5V.
- **Plot Results**: Plot `OUT` vs `IN` to observe the switching threshold.

```spice
source filename.cir
run
setplot dc1
plot OUT vs IN
```
![image](https://github.com/user-attachments/assets/19001cda-6a74-40c8-8146-402c18956c79)

Example DC sweep to find the switching threshold:
```spice
Vin IN 0 DC 0V
.dc Vin 0 2.5 0.05
```

![image](https://github.com/user-attachments/assets/9178b978-af9e-46e3-830a-8e620a9f6174)

### 2. **Transient Analysis: Propagation Delay**

Transient analysis is used to calculate the propagation delay of the inverter by applying a pulse input signal.

Example pulse signal for transient analysis:
```spice
Vin IN 0 pulse 0 2.5 0 10p 10p 1n 2n
.tran 10p 4n
```

![image](https://github.com/user-attachments/assets/74c3f643-e113-4e54-9eb6-af97b28d834a)

#### Simulation Steps
- **Setup Input Pulse**: Define the pulse with specific rise and fall times and pulse width.
- **Run Transient Analysis**: Perform the transient simulation to observe the inverter’s response.
- **Plot Output**: Analyze `OUT` vs `time` to measure delay characteristics.

---

## Sample SPICE Deck

Here is a complete SPICE deck for simulating a CMOS inverter, combining all the components discussed above:

```spice
*** CMOS Inverter SPICE Simulation ***

* Device Netlist
M1 OUT IN VDD VDD PMOS W=2u L=0.25u
M2 OUT IN GND GND NMOS W=1u L=0.25u

* Voltage Sources
VDD VDD 0 DC 2.5V
Vin IN 0 DC 0V

* Model File
.include tsmc_025um_model.mod

* DC Analysis
.dc Vin 0 2.5 0.05

* Transient Analysis
Vin IN 0 pulse 0 2.5 0 10p 10p 1n 2n
.tran 10p 4n

.end
```

### Interpreting Results
- **Switching Threshold**: Observed at the Vm point, where leakage current peaks.
- **Propagation Delay**: Determined from the transient plot, indicating the time required for output transitions.

---

## CMOS Custom Inverter Simulation

### 1. Cloning and Setting Up Custom Inverter

Clone the custom inverter library to use with the OpenLane toolchain:

```bash
cd Desktop/work/tools/openlane_working_dir/openlane
git clone https://github.com/nickson-jose/vsdstdcelldesign
cd vsdstdcelldesign
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .
magic -T sky130A.tech sky130_inv.mag &
```


![Screenshot 2024-11-13 170156](https://github.com/user-attachments/assets/f673e7f7-dc36-44eb-88f8-906b9d0fbcca)

![Screenshot 2024-11-13 170230](https://github.com/user-attachments/assets/e7923460-288f-4ee8-86fc-469ccabb6d16)


**Layout in Magic**:
- Launch Magic with the custom `sky130_inv.mag` layout file.
- Identify the components: `NMOS`, `PMOS`, output `Y`, and connections to `VDD` and `GND`.

### 2. Inverter Layout and CMOS Fabrication Process

#### CMOS Fabrication Process (16-Mask Method)

The CMOS fabrication process involves a sequence of precise photolithographic and chemical procedures to form integrated circuits on a silicon wafer. This process consists of multiple layers and requires 16 photomasks to define and protect specific regions of the wafer at various stages. Each step is carefully managed to ensure that the final chips are both reliable and functionally accurate.

1. **Substrate Preparation**: Begin with a cleaned, polished silicon wafer as the base material.
2. **N-Well Formation**: Form N-well regions in the p-type substrate via ion implantation with phosphorus.
3. **P-Well Formation**: Create P-well regions in n-type areas by implanting boron.
4. **Gate Oxide Deposition**: Deposit a thin silicon dioxide layer to insulate between the gate and channel.
5. **Polysilicon Deposition**: Apply a polysilicon layer that serves as the gate electrode.
6. **Polysilicon Masking and Etching**: Mask and etch the polysilicon to shape the gate structures.
7. **N-Well Masking and Implantation**: Define and implant N-well regions with phosphorus.
8. **P-Well Masking and Implantation**: Define and implant P-well regions with boron.
9. **Source/Drain Implantation**: Form source/drain regions by implanting dopants (e.g., arsenic for NMOS, boron for PMOS).
10. **Gate Formation**: Use a mask to define and etch the gate structure.
11. **Source/Drain Masking and Etching**: Etch to expose source/drain areas for subsequent processing.
12. **Contact/Via Formation**: Etch holes to access source, drain, and gate areas for electrical connections.
13. **Metal Deposition**: Deposit metal (e.g., aluminum or copper) to establish interconnections.
14. **Metal Masking and Etching**: Mask and etch the metal layer to create the desired interconnect patterns.
15. **Passivation Layer Deposition**: Apply a protective silicon dioxide or nitride layer over the wafer surface.
16. **Final Testing and Packaging**: Test the wafer, separate functioning chips, and package them for use.

![image](https://github.com/user-attachments/assets/057b8888-8fc6-4f72-93fe-831ebdff8cd7)

#### Identification of Transistors in the Inverter

In the Magic layout viewer, hover over the desired transistor and press `S` to select it. In the Magic terminal, type `what` to display information about the component type.

**NMOS Transistor:**

![Screenshot 2024-11-13 171951](https://github.com/user-attachments/assets/f58604d2-61fd-4ecc-8239-220d4fe8b266)

**PMOS Transistor:**

![Screenshot 2024-11-13 171919](https://github.com/user-attachments/assets/f035f8e5-e3be-451a-944d-6d1ec063d304)

**Output Node - Y:**

![Screenshot 2024-11-13 172044](https://github.com/user-attachments/assets/4ba7ee55-ca28-44b8-ace0-62fe11cc6b43)

### 3. SPICE Extraction in Magic

1. **Run SPICE Extraction Commands**:
    In Magic’s tkcon window:
   ```tcl
    extract all
    ext2spice cthresh 0 rthresh 0
    ext2spice
    ```
   ![Screenshot 2024-11-13 171415](https://github.com/user-attachments/assets/df65aa13-d898-40ec-a888-61c6dbd3a3a3)

2. **View SPICE File**:
    The extracted SPICE file (`sky130_inv.spice`) includes transistor models and capacitances.
    ```spice
	* SPICE3 file created from sky130_inv.ext - technology: sky130A
	
	.option scale=10m
	
	.subckt sky130_inv A Y VPWR VGND
	X0 Y A VGND VGND sky130_fd_pr__nfet_01v8 ad=1.44n pd=0.152m as=1.37n ps=0.148m w=35 l=23
	X1 Y A VPWR VPWR sky130_fd_pr__pfet_01v8 ad=1.44n pd=0.152m as=1.52n ps=0.156m w=37 l=23
	C0 VPWR Y 0.117f
	C1 A Y 0.0754f
	C2 A VPWR 0.0774f
	C3 Y VGND 0.279f
	C4 A VGND 0.45f
	C5 VPWR VGND 0.781f
	.ends
    ```
   ![Screenshot 2024-11-13 173112](https://github.com/user-attachments/assets/a994cda7-2130-4e66-9675-2e7b9c4e3378)

### 4. Transient Response Analysis

Modify the SPICE file to perform transient response analysis and determine propagation delay.

Check the dimensions of the box.

It is 0.01 microns. 
update the spice file.

```spice
* SPICE3 file created from sky130_inv.ext - technology: sky130A

.option scale=0.01u

.include ./libs/pshort.lib
.include ./libs/nshort.lib

// .subckt sky130_inv A Y VPWR VGND

M1000 Y A VGND VGND nshort_model.0 w=35 l=23
+  ad=1.44n pd=0.152m as=1.37n ps=0.148m
M1001 Y A VPWR VPWR pshort_model.0 w=37 l=23
+  ad=1.44n pd=0.152m as=1.52n ps=0.156m

VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns)

C0 VPWR Y 0.117f
C1 A Y 0.0754f
C2 A VPWR 0.0774f
C3 Y VGND 2f
C4 A VGND 0.45f
C5 VPWR VGND 0.781f
// .ends


.tran 1n 20n
.control
run
.endc
.end
```
![Screenshot 2024-11-13 173829](https://github.com/user-attachments/assets/48b846a4-4838-4304-8b94-229a8063891e)

Run the modified file in ngspice:

```bash
ngspice sky130_inv.spice
```
![Screenshot 2024-11-13 174115](https://github.com/user-attachments/assets/0e4fdcbc-51b4-4454-a59c-d5918e0b332d)

**Plot the Waveform**:
```spice
plot y vs time a
```
![Screenshot 2024-11-13 175427](https://github.com/user-attachments/assets/9c0ec37a-c2fc-4f58-b547-3aca1a5906cf)


 **Rise Time**     
 
 ![image](https://github.com/user-attachments/assets/2742ceaa-332d-4c80-9882-305e03cb4cb3)

 2.2403 ns - 2.17871 ns = 0.06159 ns  
 
**Fall Time**       

![image](https://github.com/user-attachments/assets/babb3168-40ff-4e09-8220-667a49913ca3)

4.096 ns - 4.05075 ns = 0.04525 ns     

**Cell Rise Delay** 

![Screenshot 2024-11-13 180725](https://github.com/user-attachments/assets/80c3d6e3-3078-461f-bea3-9feb61f3e77f)

2.20556 ns - 2.15 ns = 0.05556 ns          

**Cell Fall Delay** 

![Screenshot 2024-11-13 180833](https://github.com/user-attachments/assets/b4d6db04-6d16-48c3-a9cc-0091dd0ce6b1)

4.07761 ns - 4.04776 ns = 0.02985 ns                 

### 5. DRC Rules in Magic

Perform DRC checks on the layout using the following commands

1. **Download DRC Tests**:
    ```bash
    cd ~
    wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
    tar xfz drc_tests.tgz
    cd drc_tests
    gvim .magicrc
    ```
![Screenshot 2024-11-13 181752](https://github.com/user-attachments/assets/1d9251b6-f19d-4519-9d5b-5bbaa5312570)
![Screenshot 2024-11-13 182013](https://github.com/user-attachments/assets/b39aca59-6996-43c4-95b6-00912ead5882)

Here we can observe that there is a DRC error. To resolve this, add the following commands to the `sky130A.tech` file:

```
spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching_illegal \
	"xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
spacing npres allpolynonres 480 touching_illegal \
	"poly.resistor spacing to N-tap < %d (poly.9)"
```
![Screenshot 2024-11-13 182629](https://github.com/user-attachments/assets/356524d8-8645-4509-9b9d-f6e7af6098df)

2. **Load and Check**:
    ```tcl
    tech load sky130A.tech
    drc check
    drc why
    ```
![Screenshot 2024-11-13 182916](https://github.com/user-attachments/assets/c8c5fb4d-7deb-4dfa-a87c-a32d9436db23)

# Day 4

### 1. **Extracting the `tracks.info` File**

Navigate to the desired directory and use `less` to view the `tracks.info` file.

```bash
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
cd ../../pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd/
gedit tracks.info
```
![Screenshot 2024-11-13 190822](https://github.com/user-attachments/assets/67c69335-c62e-410f-bf41-0c85791ab031)

### 2. **Setting Grid in tkcon for Local-Interconnect Layer**

In the `tkcon` window, set the grid for the routing tracks on the local-interconnect layer:

```tcl
grid 0.46um 0.34um 0.23um 0.17um
```
![Screenshot 2024-11-13 191658](https://github.com/user-attachments/assets/94da1fd2-f7f0-4fa9-a281-3621aab478c7)


This sets the pitch for the wires, aligning them with the required guidelines for the local-interconnect layer.

### 3. **Saving and Opening Custom Layout Files**

Save your design with a custom name, then open it with `magic`.

```tcl 
save sky130_achinv.mag
magic -T sky130A.tech sky130_nitinv.mag &
```

now do

```tcl
lef write
```

![Screenshot 2024-11-13 192607](https://github.com/user-attachments/assets/d1ef6e67-51ff-441f-9958-5c5ad64c3b3f)
![Screenshot 2024-11-13 192341](https://github.com/user-attachments/assets/bb3d06df-9c62-4b1d-a395-9290b6b94884)

### 4. **Modifying `config.tcl` for the OpenLANE Flow**

Modify the `config.tcl` file

```tcl
# Design
set ::env(DESIGN_NAME) "picorv32a"

set ::env(VERILOG_FILES) "./designs/picorv32a/src/picorv32a.v"
set ::env(SDC_FILE) "./designs/picorv32a/src/picorv32a.sdc"

set ::env(CLOCK_PERIOD) "5.000"
set ::env(CLOCK_PORT) "clk"

set ::env(CLOCK_NET) $::env(CLOCK_PORT)

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

set filename $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1 } {
  source $filename
}
```
![Screenshot 2024-11-13 193126](https://github.com/user-attachments/assets/5c689904-eb49-42d4-8221-bc2266a70aae)

### 5. **Running the OpenLANE Flow**

run the following

```bash
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
```

Add the LEF files

```tcl
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```
![Screenshot 2024-11-13 195709](https://github.com/user-attachments/assets/486eb8c4-2161-4b09-8cf4-f7103aecf9b4)


### 6. **Fixing Slack**

Configure the synthesis strategy and other synthesis parameters, then rerun to fix slack.

```tcl
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1
run_synthesis
```

![Screenshot 2024-11-13 200652](https://github.com/user-attachments/assets/edc535c8-71a4-43f8-bdee-1c40c97438f0)

### 7. **Floorplanning**

start the floorplan process

```tcl
run_floorplan
```

![Screenshot 2024-11-13 200803](https://github.com/user-attachments/assets/5a1831a1-1331-47fb-b102-101dd758a146)

If you encounter issues, try:

```tcl
init_floorplan
place_io
tap_decap_or
```

### 8. **Placement**

for placement:

```tcl
run_placement
```
### Viewing Placement in Magic

in a new terminal and navigate to the following directory to view the placement in **Magic**:

```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-11_19-30/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

**Magic Output Example:**

1. **Magic Placement Output**
   ![Screenshot 2024-11-13 205711](https://github.com/user-attachments/assets/b7a990ca-0d99-4347-a949-8331c6d9b123)

2. **Custom Inverter Cell Displayed in Magic**
   ![Screenshot 2024-11-14 123151](https://github.com/user-attachments/assets/2a3d46a9-0a40-4dd0-9c4a-f862d3ce20dc)


To view the specific inverter cell in Magic:
- Select the cell by clicking on it.
- In the console, type `expand`.

**Expanded Inverter Cell:**
	![Screenshot 2024-11-14 123352](https://github.com/user-attachments/assets/61f6d9ec-ca62-413a-8d84-40cbcd76d1d1)

### 9. **Timing Analysis with Ideal Clocks Using OpenSTA**

In pre-layout STA, clock buffer effects and net delays are considered, with wire delays estimated using the PDK library wire model. The initial synthesis run may exhibit notable timing violations, whereas an optimized timing run aims to achieve zero WNS (Worst Negative Slack). In this phase, we conduct timing analysis on the initial synthesis to identify potential optimization areas.

![image](https://github.com/user-attachments/assets/1d3b411f-39ad-4da4-b4d5-202ceea01e5f)


