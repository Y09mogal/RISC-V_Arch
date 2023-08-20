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


<br />


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


<br />


<br />


<br />


<br />


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

Below is the custom file: 

<br />



<br />

Below is the objdump:

<br />


<br />

Below is using spike command: 

<br />



<br />



<br />

Below is another method command:

<br />


<br />

Below is the conclusion: 

<br />

![ABI-example](https://github.com/Y09mogal/RISC-V_Arch/assets/79003694/94900dff-bf8c-4ff2-b3b5-77ace399385a)

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

## Day-5


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
