

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



### Differences Between RISC-V ISA and Hardcoded ISA

There are notable differences between the RISC-V ISA and the Hardcoded ISA. Below is a comparison for the instructions provided:

| **Operation**       | **RISC-V ISA (Hex)** | **RISC-V ISA (Binary)**               | **Hardcoded ISA (Hex)** | **Hardcoded ISA (Binary)**              |
|---------------------|---------------------|---------------------------------------|-------------------------|-----------------------------------------|
| **ADD R6, R2, R1**  | `32'h00110333`       | `000000000001 00010 000 00110 0110011` | `32'h02208300`           | `000000100010 00000 100 00000 01100000` |
| **SUB R7, R1, R2**  | `32'h402083b3`       | `010000000010 00000 000 00111 0110011` | `32'h02209380`           | `000000100010 01000 100 10000 01100000` |
| **AND R8, R1, R3**  | `32'h0030f433`       | `000000000011 00000 111 01000 0110011` | `32'h0230a400`           | `000000100011 01000 101 00100 01100000` |
| **OR R9, R2, R5**   | `32'h005164b3`       | `000000000101 00010 110 01001 0110011` | `32'h02513480`           | `000000100101 00010 110 10100 01100000` |
| **XOR R10, R1, R4** | `32'h0040c533`       | `000000000100 00000 100 01010 0110011` | `32'h0240c500`           | `000000100100 00000 100 11000 01100000` |
| **SLT R1, R2, R4**  | `32'h0045a0b3`       | `000000000100 00010 010 00001 0110011` | `32'h02415580`           | `000000100100 00010 101 01010 01100000` |
| **ADDI R12, R4, 5** | `32'h004120b3`       | `000000000101 00010 010 01100 0010011` | `32'h00520600`           | `000000100100 00010 010 00010 01100000` |
| **BEQ R0, R0, 15**  | `32'h00000f63`       | `000000000000 00000 000 00000 1100011` | `32'h00f00002`           | `000000000000 00000 000 00000 11000000` |
| **SW R3, R1, 2**    | `32'h0030a123`       | `000000000011 00000 010 00001 0100011` | `32'h00209181`           | `000000100010 00000 010 00001 01100000` |
| **LW R13, R1, 2**   | `32'h0020a683`       | `000000000010 00000 010 01101 0000011` | `32'h00208681`           | `000000100010 00000 010 01100 01100000` |
| **SRL R16, R14, R2**| `32'h0030a123`       | `000000000011 00000 010 00001 0100011` | `32'h00271803`           | `000000100010 00000 011 00110 01100000` |
| **SLL R15, R1, R2** | `32'h002097b3`       | `000000000010 00000 111 01111 0110011` | `32'h00208783`           | `000000100010 00000 111 01111 01100000` |

### Visual Representation of Instructions:

#### Instruction 1: ADD R6, R2, R1
<img width="688" alt="Screenshot 2024-08-13 at 12 02 06 PM" src="https://github.com/user-attachments/assets/3c646c0c-418e-477c-9eb3-492b19edcede">



#### Instruction 2: SUB R7, R1, R2

<img width="631" alt="Screenshot 2024-08-13 at 12 02 20 PM" src="https://github.com/user-attachments/assets/a9064af4-626c-4a06-8894-be8b9cd4259a">


#### Instruction 3: AND R8, R1, R3

<img width="629" alt="Screenshot 2024-08-13 at 12 02 32 PM" src="https://github.com/user-attachments/assets/d15f8729-77e8-402c-b652-68d1b772e9bc">


#### Instruction 4: OR R9, R2, R5


<img width="664" alt="Screenshot 2024-08-13 at 12 03 38 PM" src="https://github.com/user-attachments/assets/e2ebbe72-6651-4fb9-a59e-8950ab03036e">




#### Instruction 5: XOR R10, R1, R4
<img width="689" alt="Screenshot 2024-08-13 at 12 03 48 PM" src="https://github.com/user-attachments/assets/b1ae1c27-89a2-47b6-8728-3fbecd97574d">


#### Instruction 6: SLT R1, R2, R4

<img width="717" alt="Screenshot 2024-08-13 at 12 04 03 PM" src="https://github.com/user-attachments/assets/a281af28-27f4-42c6-865e-d77e28bdb13c">


#### Instruction 7: ADDI R12, R4, 5

<img width="780" alt="Screenshot 2024-08-13 at 12 04 14 PM" src="https://github.com/user-attachments/assets/8e5dc591-7eea-45e3-aff4-fc70c3cb5b7d">

#### Instruction 8: BEQ R0, R0, 15

<img width="746" alt="Screenshot 2024-08-13 at 12 04 24 PM" src="https://github.com/user-attachments/assets/d29af610-aa45-4e9c-ad96-a065ee4e3b80">



