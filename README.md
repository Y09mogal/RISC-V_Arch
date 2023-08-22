# RISC-V_Arch

## Day-0
<details> 
<summary>Installation of RISC-V toolchain</summary>

<br />

**Follow below given steps to install RISC-V toolchain :**

<br />

```bash
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd riscv_workshop_collaterals
chmod +x run.sh
./run.sh

```

<br />

 Upon running it, if you get make error, ignore that and type the following commands :

<br />

 ```bash

cd ~/riscv_toolchain/iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull 
chmod 777 autoconf.sh 
./autoconf.sh 
./configure 
make
sudo make install

```

<br />

- To set the PATH variable in .bashrc

<br />

```bash
source .bashrc
gedit .bashrc
#Instead of **nsaisampath** put your **username**
export PATH="/home/nsaisampath/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH" #Type at last line # save and close the bashrc and type
source .bashrc

```

<br />

![Screenshot from 2023-08-20 12-13-48](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/a733c2e0-84c2-4bb9-9ba1-da228885ac68)

<br />

</details>

## Day-1
<details>
<summary> Introduction to RISC-V ISA </summary>

<br />

RISC-V (or Reduced Instruction Set Architecture Computer) is an open-source instruction set architecture (ISA) that is used to design custom processors for a wide range of end applications. The flow of this architecture is as follows: There is a system software block that consists of an operating system, a compiler, and an assembler, and the flow is as follows: Operating systems that handle IO activities, memory allocation, and low-level synthesis functions. The compiler transforms C, C++, and Java into instructions, which are subsequently assembled into binary data that hardware can understand. A diagram to understand the same is given below:

<br />

![intro-vsd-iat-riscv](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/63fe5715-3fa3-46c9-8f36-cbe91c5061f3)

<br />

</details>

<details>
<summary> Integer number representation </summary>
<br />
 
**64-bit unsigned number system**

<br />


A significant concept used in most computer science and digital systems is the 64-bit number system for unsigned numbers. It is an essential component of current computing architectures and is critical in representing and processing numerical data. This number system is based on the binary (base-2) numeral system, which employs only two symbols to represent all numbers, commonly 0 and 1. Each number in a 64-bit number system is made up of 64 binary digits, which are frequently referred to as "bits." The range of values that can be represented is determined by the number of bits. The range of potential values for an unsigned number on a 64-bit machine (RISC-V doubleword) is 0 to 2^64 - 1.

<br />

![64-bit-unsigned](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/f018541d-b55a-4081-8138-80da16435a29)

<br />

![Screenshot from 2023-08-21 02-07-00](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/b145dc60-e1a4-40e1-9be5-0dc914f5b613)

<br />

![img](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/43dc44b5-a1d4-44d4-81a5-fcafafd978e3)

<br />

**64-bit signed number system**

<br />

Another significant component that makes up computer science and digital systems is the 64-bit signed number system. It is a 64-bit unsigned number system extension that enables the representation of both positive and negative integers using binary digits. The leftmost bit (most significant bit) is utilized as the sign bit in this system, defining whether the integer is positive or negative. The remaining 63 bits represent the number's magnitude.

<br />

![64-bit-signed](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/760102cd-9a70-4110-a252-b4d8b48049d5)

<br />

</details>

<details>
<summary> RISCV gcc compilation and assembly code </summary>

<br />

Use the following command to compile the c code through riscv compiler:

<br />

```bash
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o 1ton.o 1ton.c
```


<br />

![Screenshot from 2023-08-20 13-11-21](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/2d1d1300-d055-4bd7-b5f5-414a5cdc94cf)

<br />

![Screenshot from 2023-08-21 01-54-09](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/43e2ecd5-4496-4748-8cf3-6c8a66a4c33d)

<br />

![Screenshot from 2023-08-20 18-52-52](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/340a47d5-4a72-41ba-ab17-4779ce1c012e)

<br />

![Screenshot from 2023-08-20 19-06-26](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/b36a1cde-6d28-4c29-b12b-de864dce2182)

<br />

![Screenshot from 2023-08-20 19-08-21](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/9877d586-574e-4daa-8902-63f70a479e5c)

<br />


The given below command is used to observe the result:

<br />

```bash
riscv64-unknown-elf-objdump -d 1ton.o
```

<br />

Get the output file using the spike.  
The command to get the object output is given below:

<br />

```bash
spike pk 1ton.o
```

<br />


<br />

To debug the output, use the following command: 

<br />

```bash
spike -d pk 1ton.o
```

<>br /

Then, use the following command to observe file and memory locations :  

<br />

```bash
until pc 0 100b0
reg 0 a1
```

<br />

![Screenshot from 2023-08-21 01-50-52](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/28ea2f69-33f9-4294-b374-313e6e2360a5)

<br />

Below is the architecture

<br />

![arch-riscv](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/1b0427e6-cdb1-4d47-a757-db3d9075f136)

<br />

</details>

## Day-2
<details>
<summary> Application Binary Interface </summary>

<br />

**Introduction**

<br />

An Application Binary Interface (ABI) connects two binary program modules. Often, one of these modules is a library or an operating system facility, and the other is a user-run program. An ABI specifies how to access data structures or computational procedures in machine code, which is a low-level, hardware-dependent format. An API (Application Programming Interface), on the other hand, defines this access in source code, which is a relatively high-level, hardware-independent, and typically human-readable format. The calling convention, which governs how data is delivered as input to or read as output from computational procedures, is a frequent element of an ABI.

<br />

![ABI](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/711643c8-7dec-4e01-a0da-0dd33866812d)

<br />

<br />

![ABI-1](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/e4bdddf8-7619-4e6e-9877-4a6d9c3ea4d1)

<br />

Memory allocation for double words often entails reserving contiguous blocks of memory in a computer's RAM (Random Access Memory) to store data that is twice the size of a regular word, which on many computer architectures is often 32 bits or 4 bytes. Double words are usually 64 bits or 8 bytes long. This method is essential in computer programming because it enables the efficient storing and handling of larger data structures and numeric values, such as long integers or floating-point numbers with better precision. When allocating memory for double words, appropriate alignment is critical to guarantee that the memory addresses are consistent with the system's architecture, as misaligned memory access might result in performance penalties or even program crashes.

<br />

![ABI-2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/df567f6a-7cd6-4b28-a9b7-cdb38e1daf23)

<br />

Single register load and store instructions can move a 32-bit word, a 16-bit halfword, or an 8-bit byte between memory and a register. Loads of bytes and halfwords can be zero or sign extended as they are loaded.

<br />

There are three basic addressing modes for load and store instructions:
- Offset
- Pre-indexed
- Post-indexed

<br />

An instantaneous offset or offset depending on a register is added or subtracted from a base register to create the address. Shift operations can also be used to scale register-based offsets. The result of the offset computation is updated in the base register in pre-indexed and post-indexed addressing modes.

<br />

![ABI-3](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/f74f0ba3-7e34-4a65-ae2f-8df350815896)

<br />

<br />

![ABI-4](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/0b21601d-2496-4602-994c-2ad745d58efe)

<br />

<br />

![ABI-5](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/d6cf8d94-186a-4a86-9670-dd6bacf2f97c)

<br />

</details>

<details>
<summary> ABI function cells </summary>

<br />

![Screenshot from 2023-08-21 02-46-42](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/559ab795-e535-4bd9-9c83-07d13843b8e5)

<br />

![Screenshot from 2023-08-21 02-46-13](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/d9eae506-a822-4982-b7b2-fb71a6d0d890)


<br />

Below is the custom file: 

<br />

![Screenshot from 2023-08-21 02-48-36](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/2c7239d0-839c-4caf-87df-033dd44cdc88)


<br />

Below is the objdump:

<br />

![Screenshot from 2023-08-21 02-51-35](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/ae3376ff-6b5d-4314-9b8e-68962c0b1e08)

<br />

Below is using spike command: 

<br />

![Screenshot from 2023-08-21 02-54-06](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/8a3cdfe7-2535-4dd2-81fa-622445bd77ba)


<br />


<br />

Below is the conclusion: 

<br />

![ABI-example](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/94900dff-bf8c-4ff2-b3b5-77ace399385a)

<br />

</details>

<details>
<summary>Lab to sun C-program on RISC-V CPU</summary>

<br />

![lab2-d2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/fde75ef3-484b-4d26-87cf-ff5a600e0fdd)

<br />

We have RISCV CPU program code here, via which we send the HEX format file of a C program to see the output of the given code.


<br />

```bash
chmod 777 rv32im.sh
./rv32im.sh 
```

<br />

![Screenshot from 2023-08-22 19-11-39](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/4b5dca80-c9cb-4e6d-a6d6-f3ba346ba0d7)

<br />

![Screenshot from 2023-08-22 18-57-00](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/ee7a53fe-b4ed-4e2c-8afb-4cacb53d7703)

<br />

Input hex file to sent through verilog code:

<br />

**firmware.hex:**

<br />

![Screenshot from 2023-08-22 19-15-33](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/7e1b6007-1b61-48f1-b09a-b6e42f882387)

<br />

**firmware32.hex:**

<br />

![Screenshot from 2023-08-22 19-15-59](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/8d0073d5-3638-44c9-8f8b-aaad5f233baf)

<br />


 
</details>

## Day-3

<details>

<summary> Combinational Logic using Makerchip in TL-verilog </summary>

<br />

Makerchip platform is a cloud based web application that takes design input in form of TL-verilog code and provides logical diagram & waveform as output without any testbench provided externally.
This section describes about TL-verilog and Makerchip platform & its examples.

<br />

**Logic gates representation and their truth tables**

<br />

![lgr_tt](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/2530d328-b160-46b8-b1f3-bfd9d9cf410a)

<br />

**Example of Full Adder Circuit**

<br />

![fa_ckt](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/09770c88-e25d-4925-9593-e7d27d729799)

<br />

**Boolean Operators Representation**


<br />

![Bool_opr_Representation](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/b300789a-6286-4650-a6f3-575fc1fa3f60)

<br />


**Combinational Logic Examples in Makerchip IDE**

<br />

Adder:


<br />

![adder](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/ff03d332-b7bc-4c4a-af8d-1582fcbb3d68)

<br />


Multiplexer:


<br />

![mux](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/322f9d06-002a-4439-be53-9604063ac775)

<br />

Ripple Carry:

<br />

![ripple_carry_adder](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/d70fe5d4-de05-4a4e-bdeb-aec0c072609d)

<br />

 
</details>

<details>

<summary>Sequential circuits in Maker chip platform</summary>

<br />

**Free Counter**

<br />

![maker_chip_counter](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/6ad26aba-dcd4-4fc4-a658-d58600a58b20)

<br />


Here's a sequential calculator that remembers previous calculations for the next one.

<br />

![maker_chip_calc2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/4fade9ce-57ec-4854-bfbf-08095fc8510a)

<br />


 
</details>

<details>

<summary>Pipelined Logic</summary>

<br />

We take pythagorean example from platform and execute it to understand its flow. We compile and observe the output on different windows as shown below.

<br />

![maker_chip_counter](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/e0c1659e-24a2-4ebd-812d-a8e274ecabd0)

<br />

Pipeline refers to executing in stages. We can divide entire calculation into several stages to have clock frequency unchanged. This is done in TL-verilog by putting @1, @2 before that stage instruction. 

<br />

![maker_chip_calc2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/46ed35a3-29fa-4ab9-a694-7c0a226b6946)

<br />

Below is Counter and Calculator in pipeline:  

<br />

![Counter_Calc](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/cfbd9bc5-4c96-4992-a7b0-74bcc1373a77)

<br />

Below shown cyclic calculator diagram:  

<br />

![Cyclic_cCalc](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/2b251a13-457d-4d69-a2db-583d469c3af3)

<br />

Below is makerchip implementation of counter calculator:  

<br />

![CC](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/06d8fe68-44d8-4825-b6d7-cbe835a15ad6)

<br />

Below is makerchip implementation of two cycle calculator: 

<br />

![2cycle_calc](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/9f464797-ca46-44cf-8d18-dddec9e79231)

<br />
 
</details>

<details>

<summary>Validity</summary>

<br />

**Validity**

<br />

Validity is a feature unique to TL-verilog that is not found in other RTL languages. In TL-verilog, debugging is easier, error checking is better, and clock gatig is automated. If there are numerous stages of calculation, we use validity to signal which valid output is available for the next series of computations.

<br />

**Clock gating**

<br />

Clock consumes more power in most circuits since it is created continually by the clock generator circuit. Clock gating prevents clock signals from being toggled. To perform clock gating, we apply the condition of validity.

<br />

**Distance Calculator**

<br />

Here we use pythagoras theorem to calculate distance between two points through a given path as shown.

<br />

![maker_chip_distance_calc](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/a16a2ae9-5c9e-4fbc-90eb-d716d035721a)

<br />

**Calculator with single value memory Lab**

<br />

Here we modify and design previous calculator to have single value memory and recall use for successive computations.

<br />

![maker_chip_single_mem_calc](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/b0949560-76a4-41a2-ac74-ff1d411e0c2b)

<br />

 
</details>

## Day-4

<details>

<summary>Introduction</summary>

<br />

The functional specification of a processor is referred to  the term architecture. It represents the capabilities that the programme can rely on from the hardware. Architecture does not describe how a processor is constructed. It describes what a processor is capable of. Micro-architecture, on the other hand, describes the construction and design of a processor. The number and size of caches, instruction cycle counts, pipeline length, and other parameters are defined by microarchitecture.

<br />

**Micro-Architecture**

<br />

![ma1](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/5d41b32f-5b90-4377-907d-294da360a6e6)

<br />

![ma11](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/e8c4d266-597f-4f51-b112-e55920a24199)

<br />

Makerchip implementation of the same is shown as below:

<br />

![makerchip_ma](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/3d44d74b-df01-47f4-90a6-557b33e079e1)

<br />


 
</details>

<details>
 
<summary>RISCV Micro-Architecture</summary>

<br />

### Simple RISCV Micro-architecture

Here,we implement the following basic blocks:

-Program Counter (PC)
-Imem-Rd ( Instruction Memory)
-Instruction Decoder
-Register File Read
-Arithmatic Logic Unit (ALU)
-Register File Write
-Branch


<br />

![maker_chip_micro_arch](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/0b78e14f-f773-426d-ac10-34c3e5a83b77)

<br />

### Next PC lab

Program counter stores address of next instruction.
```
$pc[31:0] = $reset ? 32'b0 : >>1$pc + 32'd4;
```

<br />

![maker_chip_next_pc](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/9e04c6ab-9c0a-4122-b584-1e19c3178ae4)

<br />


### Fetch lab
This reads instruction according to address stored in PC.

```
cpu
      @0
         $reset = *reset;
         $pc[31:0] = $reset ? 32'b0 : >>1$pc + 32'd4;
      @1 
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $instr[31:0] = $imem_rd_data[31:0];
         
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr; 



      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4)
```


<br />

![maker_chip_fetch](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/51f3dd9f-e110-40ee-a544-28c696abd0db)

<br />

### Decode
We decode instruction fetched from memory.
```
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = $reset ? 32'b0 : >>1$pc + 32'd4;
      @1 
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $instr[31:0] = $imem_rd_data[31:0];
         
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr; 
            
      @1
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b10100;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         
         
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                    32'b0;
         
         
         $rs2[4:0] = $instr[24:20];
         $rs1[4:0] = $instr[19:15];
         $rd[4:0]  = $instr[11:7];
         $opcode[6:0] = $instr[6:0];
         $func7[6:0] = $instr[31:25];
         $func3[2:0] = $instr[14:12];


      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4) 
```


<br />

![maker_chip_decode](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/83c82594-b817-488a-af13-35ed218d94cb)

<br />

 
</details>

<details>

<summary>Fetch and Decode</summary>

<br />

The design of a processor is built on three fundamental steps: fetch, decode, and execute and  we will construct a RISC-V CPU core, the block diagram for which is shown below:

<br />

![d4-p1](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/33a28291-4709-4ff3-8dad-defb34ea83ed)

<br />

**Template for running Viz**

<br />

```bash
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;



      // YOUR CODE HERE
      // ...

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      //m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   //m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```

<br />

 
</details>

<details>

<summary>PC Logic Lab</summary>

<br />

A crucial part of a computer's central processing unit (CPU) is the programme counter (PC), which maintains track of the address of the subsequent instruction to be retrieved and executed. As instructions are fetched and executed in a programme, the PC logic oversees the updating of the programme counter.

<br />

**Incrementing the PC**

<br />

The PC must be modified to point to the address of the subsequent instruction after the previous instruction has been fetched. The most frequent method is to multiply the instruction size by the PC. Because instructions in many architectures have a limited size, such as 32 bits, the PC is incremented by 4 after each instruction fetch.

<br />

![d4l1](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/9e993855-bebc-4db5-90fe-f64f0528cc6d)

<br />

```bash
|cpu
      @0
         $reset = *reset;
         
         $pc[31:0] = >>1$reset ? '0 : >>1$pc + 32'd4;
```

<br />

![d4l11](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/0dbbb1c0-39a6-4671-8477-b86f039a6b57)

<br />

 
</details>

<details>

<summary>Instruction Fetch Logic Lab</summary>

<br />

![d4l2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/5e99accb-4f3d-4218-bcd6-cccf9a80def3)

<br />

```bash
|cpu
      @0
         $reset = *reset;
         
         $pc[31:0] = >>1$reset ? '0 : >>1$pc + 32'd4; 

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```

<br />

![d4l21](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/14eeb93b-c4e1-442b-9347-2abf5e974595)

<br />

The following warning will be found in the log:

<br />

```bash
WARNING(1) (UNUSED-SIG): File 'top.tlv' Line 61 (char 16)
			-> instantiated: '/raw.githubusercontent.com/BalaDhinesh/RISCVMYTHWorkshop/master/tlvlib/riscvshelllib.tlv':32, which
	resulted in 'top.m4':74(ch16):
	+---------------vvvvvvvvvvvvvvvvvvv-------
	>               $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
	+---------------^^^^^^^^^^^^^^^^^^^-------
	Signal |cpu$imem_rd_data is assigned but never used.
```

<br />

![d4l22](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/282e652b-c54f-4c07-8353-ef3c68b5deb9)

<br />

```bash
|cpu
      @0
         $reset = *reset;
         //pc
         $pc[31:0] = >>1$reset ? 32'b0 : >>1$pc + 32'd4;
      @1   
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;   
         $instr[31:0] = $imem_rd_data[31:0];
         
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;   

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
  endmodule
```

<br />

![d4l23](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/d0d5da0f-22de-45e6-9cda-0fa584415ff6)

<br />

![d4l24](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/99fe1e98-e965-4d41-9db0-992b43b3f7e6)

<br />

 
</details>


<details>

<summary>RISC-V Instruction Types IRSBJU Decode Logic
 Lab</summary>

<br />

Instruction decoding is the process of deciphering the bits of an instruction read from memory to discover the operation that the instruction is expected to perform in computer architecture. Different sorts of instructions have different formats and meanings, so the decoding method varies appropriately. I'll give a general overview of typical instruction types and their decoding below:

<br />

1. **R-Type (Register-Type) Instructions:**
   R-Type instructions operate on data stored in registers. They usually involve arithmetic, logical, or shift operations.
   
   Format: 
   ```
   opcode | rd | funct3 | rs1 | rs2 | funct7
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `funct3`: Function code specifying the operation.
   - `rs1`: Source register 1.
   - `rs2`: Source register 2.
   - `funct7`: Additional function code (used for certain instructions).

2. **I-Type (Immediate-Type) Instructions:**
   I-Type instructions perform operations with an immediate value (constant) and a register.
   
   Format:
   ```
   opcode | rd | funct3 | rs1 | imm[11:0]
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `funct3`: Function code specifying the operation.
   - `rs1`: Source register.
   - `imm[11:0]`: 12-bit immediate value.

3. **S-Type (Store-Type) Instructions:**
   S-Type instructions store data from a register into memory.
   
   Format:
   ```
   opcode | imm[11:5] | rs2 | rs1 | funct3 | imm[4:0]
   ```
   
   - `opcode`: Operation code.
   - `imm[11:5]`: Upper immediate bits.
   - `rs2`: Source register 2.
   - `rs1`: Source register 1.
   - `funct3`: Function code specifying the operation.
   - `imm[4:0]`: Lower immediate bits.

4. **B-Type (Branch-Type) Instructions:**
   B-Type instructions perform conditional branches based on comparisons.
   
   Format:
   ```
   opcode | imm[12] | imm[10:5] | rs2 | rs1 | funct3 | imm[4:1] | imm[11] | imm[0]
   ```
   
   - `opcode`: Operation code.
   - `imm[12]`: Upper immediate bit.
   - `imm[10:5]`: Immediate bits for offset calculation.
   - `rs2`: Source register 2.
   - `rs1`: Source register 1.
   - `funct3`: Function code specifying the operation.
   - `imm[4:1]`: Immediate bits for offset calculation.
   - `imm[11]`: Immediate bit.
   - `imm[0]`: Immediate bit.

5. **U-Type (Upper Immediate-Type) Instructions:**
   U-Type instructions load a constant into a register.
   
   Format:
   ```
   opcode | rd | imm[31:12]
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `imm[31:12]`: 20-bit immediate value.

6. **J-Type (Jump-Type) Instructions:**
   J-Type instructions perform unconditional jumps.
   
   Format:
   ```
   opcode | rd | imm[20] | imm[10:1] | imm[11] | imm[19:12]
   ```
   
   - `opcode`: Operation code.
   - `rd`: Destination register.
   - `imm[20]`: Immediate bit.
   - `imm[10:1]`: Immediate bits for offset calculation.
   - `imm[11]`: Immediate bit.
   - `imm[19:12]`: Immediate bits for offset calculation.

<br />

Many RISC architectures, notably RISC-V, use these as the primary instruction types. When an instruction is read from memory, the instruction decoder uses the opcode and other data to determine the instruction type and operands. The CPU can then use the decoded values to perform the relevant operation based on the instruction type. Remember that this is a high-level overview, and specifics may differ depending on the architecture and implementation details.

<br />

![d4l3](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/b2a044cc-799a-4ee8-8312-13e531174203)

<br />

![d4l31](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/9fb94d44-f867-43dc-ac28-62eb80eb193f)

<br />

```bash
|cpu
      @0
         $reset = *reset;
      @1
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001 ;
                       
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b10100 ; 
                       
         $is_s_instr = $instr[6:2] ==? 5'b0100x ;
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101 ;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000 ;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011 ;
                                     
      // YOUR CODE HERE
      // ...

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      //m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
      //m4+myth_fpga(@0)  // Uncomment to run on fpga

   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic. @4 would work for all labs.
\SV
   endmodule
```

<br />

![d4l32](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/b9abe6ba-0c0c-4622-863d-12a7bae8d986)

<br />

![d4l33](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/d34c051b-01cd-4baa-9789-f2045c007cfa)

<br />

 
</details>

<details>

<summary>Lab - Instruction Immediate Decode Logic For RV-ISBUJ</summary>

<br />

![d4l4](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/2a2ed0d4-dd8d-4a83-af4f-2fdfad98637e)

<br />

```bash
//immediate instr
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}}, $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}}, $instr[30:25], $instr[11:8], $instr[7] } :
                      $is_b_instr ? { {19{$instr[31]}}, {2{$instr[7]}}, $instr[30:25], $instr[11:8], 0 } :
                      $is_u_instr ? { $instr[31], $instr[30:20], $instr[19:12], 0 } :
                         $is_j_instr ? { {21{$instr[31]}}, $instr[19:12], {2{$instr[20]}}, $instr[30:25], $instr[24:21], 0 } :
                         32'b0;
```

<br />

![d4l41](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/aabbc03c-a530-4f8c-8506-ab40921e2e50)

<br />

![d4l42](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/d789d656-d4ca-4cae-b360-0f9d21f33a03)

<br />

 

 
</details>

<details>

<summary>Lab - Decode other Fields of Instructions For RV-ISBUJ</summary>

<br />

![d4l5](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/cb633929-5f83-4009-9ac7-a1176e9a0612)

<br />

```bash
//extracting other instruction fields
         $rs2 = $instr[24:20];
         $rs1 = $instr[19:15];
         $rd = $instr[11:7];
         $opcode = $instr[6:0];
         $funct3 = $instr[12:14];
         $funct7 = $instr[25:30];

```

<br />

![d4l51](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/8dea0217-6ade-40f4-8796-8a401a6cbe24)

<br />

![d4l52](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/4ccb58b8-b120-4ebb-813a-b940d06ba5e0)

<br />

 
</details>

<details>

<summary>Lab - Decode Instruction Field Based on Instr Type RV-ISBUJ</summary>

<br />

![d4l6](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/f3fe136d-74f6-4a8c-8ae0-1c62a6a2858b)

<br />

```bash

//instruction field code
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         $funct7_valid = $is_r_instr; 
         ?$funct7_valid
            $funct7[5:0] = $instr[25:31];
         $opcode_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr || $is_s_instr || $is_b_instr;
         ?$opcode_valid
            $opcode[4:0] = $instr[11:7];


```

<br />

![d4l61](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/34b17513-ef43-4afe-aee8-8e4a987a0fa6)

<br />

![d4l62](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/2019036a-3508-4af1-99d8-4b7d24de8153)

<br />

 
 
</details>

<details>

<summary>Lab - Decode_2 Instruction Field Based on Instr Type RV-ISBUJ</summary>

<br />

**Pipeline structure:**

<br />

![d4l7](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/56e9e6cb-7e8d-4a39-97da-71c2fb2be374)

<br />

<br />

**Makerchip Implementation:**

<br />

![d4l71](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/9a2ca35b-2275-4453-af9f-6da1114a7882)

<br />
 
</details>


<details>

<summary>Lab-RISCV Control Logic: Register file read</summary>

<br />

**Pipeline structure:**

<br />

![d4ll1](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/38690ec8-6c50-4681-96ce-f69136012e0e)

<br />

<br />

**Makerchip Implementation:**

<br />

![d4ll12](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/78efebb1-52a5-4fef-a9ad-73981e461782)

<br />
 
</details>


<details>

<summary>Lab-RISCV Control Logic: ALU</summary>

<br />

**Pipeline structure:**

<br />

![d4ll2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/330046d1-e01b-4360-bd3f-03020f94a8c7)

<br />

<br />

**Makerchip Implementation:**

<br />

![d4ll21](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/e8cb073e-325e-4903-b681-cac7b5dc402a)

<br />
 
</details>



<details>

<summary>Lab-RISCV Control Logic: Register file write</summary>

<br />

**Pipeline structure:**

<br />

![d4ll3](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/2e401d6a-27af-459e-bc28-79139921c9d6)

<br />

<br />

**Makerchip Implementation:**

<br />

![d4ll31](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/62665453-0a37-4539-a5e5-20619fee4167)

<br />
 
</details>


## Day-5

<details>

<summary>CPU Pipelining</summary>

<br />

Given below waterfall diagram depicts the CPU pipelining:

<br />

![d5-p1](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/567267a5-5ee2-4f75-9f5b-e2c087a1519e)

<br />

Code for the same is given below:

<br />

```bash
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
 m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
      
      //Fetch
         // Next PC
         $pc[31:0] = (>>1$reset) ? '0 : 
                     (>>3$taken_br) ? >>3$br_tgt_pc : >>1$inc_pc;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
      @1         
         $instr[31:0] = $imem_rd_data[31:0];
         $inc_pc[31:0] = $pc + 32'd4;  
      // Decode   
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100 ||
                       $instr[6:2] ==? 5'b0110x;                       
         $is_b_instr = $instr[6:2] == 5'b11000;
         $is_u_instr = $instr[6:2] == 5'b0x101;
         $is_s_instr = $instr[6:2] == 5'b0100x;
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7] } :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31:12] , 12'b0} : 
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} : 32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         // Branch Instruction
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         
         // Arithmetic Instruction
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         
         // Load Instruction
         $is_load = $dec_bits ==? 11'bx_xxx_0000011;
         
         // Store Instruction
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         
         // Jump Instruction
         $lui = $dec_bits ==? 11'bx_xxx_0110111;
         $auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $jal = $dec_bits ==? 11'bx_xxx_1101111;
         $jalr = $dec_bits ==? 11'bx_000_1100111;
         
      @2   
      // Register File Read
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
            
      // Branch Target PC       
         $br_tgt_pc[31:0] = $pc + $imm;
      
      // Input signals to ALU
         $src1_value[31:0] = ((>>1$rd == $rs1) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data1[31:0];
         $src2_value[31:0] = ((>>1$rd == $rs2) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data2[31:0];
         
      @3   
         
      // ALU
         $sltu_result = $src1_value < $src2_value ;
         $sltiu_result = $src1_value < $imm ;
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value : 
                         $is_or ? $src1_value | $src2_value : 
                         $is_ori ? $src1_value | $imm :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_xori ? $src1_value ^ $imm :
                         $is_and ? $src1_value & $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_sub ? $src1_value - $src2_value :
                         $is_slti ? (($src1_value[31] == $imm[31]) ? $sltiu_result : {31'b0,$src1_value[31]}) :
                         $is_sltiu ? $sltiu_result :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_srai ? ({{32{$src1_value[31]}}, $src1_value} >> $imm[4:0]) :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_slt ? (($src1_value[31] == $src2_value[31]) ? $sltu_result : {31'b0,$src1_value[31]}) :
                         $is_sltu ? $sltu_result :
                         $is_srl ? $src1_value >> $src2_value[5:0] :
                         $is_sra ? ({{32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $lui ? ({$imm[31:12], 12'b0}) :
                         $auipc ? $pc + $imm :
                         $jal ? $pc + 4 :
                         $jalr ? $pc + 4 : 32'bx;
                         
      // Register File Write
         $rf_wr_en = $valid ? (($rd == 5'b0) ? 1'b0 : $rd_valid) : 1'b0;     
         ?$rf_wr_en
            $rf_wr_index[4:0] = $rd[4:0];
      
         $rf_wr_data[31:0] = $result[31:0];
      
      // Branch
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
                     
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         
         
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule
```

<br />

**Makerchip Implementation :**

<br />

![d5-p2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/7df17ad3-4173-4a0e-9c39-e3ad02f6ab1e)

<br />
 
</details>

<details>

<summary>Load and Store</summary>

<br />

**Load Store Unit :**

<br />

![d5-pp1](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/68a8bd1d-f492-4634-a55c-6054542e26d6)

<br />

**Waterfall Diagram depicting the same:**

<br />

![d5-pp2](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/50199ce5-10e6-46bd-82e2-9a72801c9dd3)

<br />

**Code for the same :**

<br />

```bash
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
 m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the value of r10 into address 17.
   m4_asm(LW, r17, r0, 10000)           // Load the value from 
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
      
      //Fetch
         // Next PC
         $pc[31:0] = (>>1$reset) ? '0 : 
                     (>>3$taken_br) ? >>3$br_tgt_pc : 
                     (>>3$is_load) ? >>3$inc_pc : >>1$inc_pc;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
      @1         
         $instr[31:0] = $imem_rd_data[31:0];
         $inc_pc[31:0] = $pc + 32'd4;  
      // Decode   
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100 ||
                       $instr[6:2] ==? 5'b0110x;                       
         $is_b_instr = $instr[6:2] == 5'b11000;
         $is_u_instr = $instr[6:2] == 5'b0x101;
         $is_s_instr = $instr[6:2] == 5'b0100x;
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7] } :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31:12] , 12'b0} : 
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} : 32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         // Branch Instruction
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         
         // Arithmetic Instruction
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         
         // Load Instruction
         $is_load = $dec_bits ==? 11'bx_xxx_0000011;
         
         // Store Instruction
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         
         // Jump Instruction
         $lui = $dec_bits ==? 11'bx_xxx_0110111;
         $auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $jal = $dec_bits ==? 11'bx_xxx_1101111;
         $jalr = $dec_bits ==? 11'bx_000_1100111;
         
      @2   
      // Register File Read
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
            
      // Branch Target PC       
         $br_tgt_pc[31:0] = $pc + $imm;
      
      // Input signals to ALU
         $src1_value[31:0] = ((>>1$rd == $rs1) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data1[31:0];
         $src2_value[31:0] = ((>>1$rd == $rs2) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data2[31:0];
         
      @3   
         
      // ALU
         $sltu_result = $src1_value < $src2_value ;
         $sltiu_result = $src1_value < $imm ;
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value : 
                         $is_or ? $src1_value | $src2_value : 
                         $is_ori ? $src1_value | $imm :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_xori ? $src1_value ^ $imm :
                         $is_and ? $src1_value & $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_sub ? $src1_value - $src2_value :
                         $is_slti ? (($src1_value[31] == $imm[31]) ? $sltiu_result : {31'b0,$src1_value[31]}) :
                         $is_sltiu ? $sltiu_result :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_srai ? ({{32{$src1_value[31]}}, $src1_value} >> $imm[4:0]) :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_slt ? (($src1_value[31] == $src2_value[31]) ? $sltu_result : {31'b0,$src1_value[31]}) :
                         $is_sltu ? $sltu_result :
                         $is_srl ? $src1_value >> $src2_value[5:0] :
                         $is_sra ? ({{32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $lui ? ({$imm[31:12], 12'b0}) :
                         $auipc ? $pc + $imm :
                         $jal ? $pc + 4 :
                         $jalr ? $pc + 4 : 
                         ($is_load || $is_s_instr) ? $src1_value + $imm : 32'bx;
                         
      // Register File Write
         $rf_wr_en = ($rd_valid && $valid && $rd != 5'b0) || >>2$valid_load;
         ?$rf_wr_en
            $rf_wr_index[4:0] = !$valid ? >>2$rd[4:0] : $rd[4:0];
      
         $rf_wr_data[31:0] = !$valid ? >>2$ld_data[31:0] : $result[31:0];
      
      // Branch
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
                     
         $valid_taken_br = $valid && $taken_br;
         
      // Load
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         
         
      @4
         $dmem_rd_en = $valid_load;
         $dmem_wr_en = $valid && $is_s_instr;
         $dmem_addr[3:0] = $result[5:2];
         $dmem_wr_data[31:0] = $src2_value[31:0];
         
      @5   
         $ld_data[31:0] = $dmem_rd_data[31:0];
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = |cpu/xreg[17]>>5$value == (1+2+3+4+5+6+7+8+9);
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule
```

<br />

**Makerchip Implementation:**

<br />

![d5-pp3](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/bcc7b323-a50e-473f-a815-3babb879c19e)

<br />
 
</details>

<details>

<summary>Final CPU</summary>

<br />

**Final RISC-V based CPU Code:**

<br />

```bash
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
 m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the value of r10 into address 17.
   m4_asm(LW, r17, r0, 10000)           // Load the value from 
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
      
      //Fetch
         // Next PC
         $pc[31:0] = (>>1$reset) ? '0 : 
                     (>>3$valid_taken_br) ? >>3$br_tgt_pc : 
                     (>>3$valid_load) ? >>3$inc_pc : 
                     (>>3$valid_jump && >>3$is_jal) ? >>3$br_tgt_pc :
                     (>>3$valid_jump && >>3$is_jalr) ? >>3$jalr_tgt_pc : >>1$inc_pc;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
      @1         
         $instr[31:0] = $imem_rd_data[31:0];
         $inc_pc[31:0] = $pc + 32'd4;  
      // Decode   
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100 ||
                       $instr[6:2] ==? 5'b0110x;                       
         $is_b_instr = $instr[6:2] == 5'b11000;
         $is_u_instr = $instr[6:2] == 5'b0x101;
         $is_s_instr = $instr[6:2] == 5'b0100x;
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7] } :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31:12] , 12'b0} : 
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} : 32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         // Branch Instruction
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         
         // Arithmetic Instruction
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         
         // Load Instruction
         $is_load = $dec_bits ==? 11'bx_xxx_0000011;
         
         // Store Instruction
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         
         // Jump Instruction
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         
         $is_jump = $is_jal || $is_jalr;
         
      @2   
      // Register File Read
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
            
      // Branch Target PC       
         $br_tgt_pc[31:0] = $pc + $imm;
      
      // Jump Target PC
         $jalr_tgt_pc[31:0] = $src1_value + $imm;
         
      // Input signals to ALU
         $src1_value[31:0] = ((>>1$rd == $rs1) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data1[31:0];
         $src2_value[31:0] = ((>>1$rd == $rs2) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data2[31:0];
         
      @3   
         
      // ALU
         $sltu_result = $src1_value < $src2_value ;
         $sltiu_result = $src1_value < $imm ;
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value : 
                         $is_or ? $src1_value | $src2_value : 
                         $is_ori ? $src1_value | $imm :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_xori ? $src1_value ^ $imm :
                         $is_and ? $src1_value & $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_sub ? $src1_value - $src2_value :
                         $is_slti ? (($src1_value[31] == $imm[31]) ? $sltiu_result : {31'b0,$src1_value[31]}) :
                         $is_sltiu ? $sltiu_result :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_srai ? ({{32{$src1_value[31]}}, $src1_value} >> $imm[4:0]) :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_slt ? (($src1_value[31] == $src2_value[31]) ? $sltu_result : {31'b0,$src1_value[31]}) :
                         $is_sltu ? $sltu_result :
                         $is_srl ? $src1_value >> $src2_value[5:0] :
                         $is_sra ? ({{32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $is_lui ? ({$imm[31:12], 12'b0}) :
                         $is_auipc ? $pc + $imm :
                         $is_jal ? $pc + $imm :
                         $is_jalr ? $pc + $imm : 
                         ($is_load || $is_s_instr) ? $src1_value + $imm : 32'bx;
                         
      // Register File Write
         $rf_wr_en = ($rd_valid && $valid && $rd != 5'b0) || >>2$valid_load;
         ?$rf_wr_en
            $rf_wr_index[4:0] = !$valid ? >>2$rd[4:0] : $rd[4:0];
      
         $rf_wr_data[31:0] = !$valid ? >>2$ld_data[31:0] : $result[31:0];
      
      // Branch
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
                     
         $valid_taken_br = $valid && $taken_br;
         
      // Load
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load || >>1$valid_jump || >>2$valid_jump);
      
      // Jump
         $valid_jump = $valid && $is_jump;
                  
      @4
         $dmem_rd_en = $valid_load;
         $dmem_wr_en = $valid && $is_s_instr;
         $dmem_addr[3:0] = $result[5:2];
         $dmem_wr_data[31:0] = $src2_value[31:0];
         
      @5   
         $ld_data[31:0] = $dmem_rd_data[31:0];
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = |cpu/xreg[17]>>5$value == (1+2+3+4+5+6+7+8+9);
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic       
\SV
   endmodule
```

<br />

**Makerchip Implementation:**

<br />

![final](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/0a70547f-ba6b-4c5d-ab7a-8f04784eb4f8)

<br />

![image-3](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/3c27ba9c-ac59-41ec-aa33-b9f3d05bf687)

<br />


 
</details>


### Acknowledgments
* Kunal Ghosh, CEO, and Co-founder, VSD Corp. Pvt. Ltd.

### Contact Information
* Yash Dharemsh Mogal, IMtech 2020, International Institute of Information Technology, Bangalore Yash.Mogal@iiitb.ac.in
* Kunal Ghosh, CEO, and Co-founder, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com

## References
* https://github.com/kunalg123/riscv_workshop_collaterals
* https://en.wikipedia.org/wiki/Toolchain
* https://en.wikipedia.org/wiki/GNU_toolchain
* https://www.vsdiat.com
* http://makerchip.com/
* https://github.com/stevehoover
* https://github.com/riscv-software-src/homebrew-riscv/tree/main
