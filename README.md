

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

