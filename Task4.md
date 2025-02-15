GTKWave is a waveform visualization tool that presents simulation outcomes in a user-friendly graphical format, assisting users in examining signal variations over time, focusing on particular events, and troubleshooting their designs. Combined, these tools create a comprehensive simulation and verification framework, with Iverilog carrying out the simulation and GTKWave facilitating the interpretation of the results.

for simulation, we use a verilog netlist and testbench. a .vcd file is generated, and the output waveforms are simulated using gtkwave.


![image](https://github.com/user-attachments/assets/0613b508-1962-47d5-80e1-96f2018c788b)


INSTALLATION STEPS
-----------------------

(1) Installing:
sudo apt-get update
sudo apt-get install iverilog gtkwave
-------------------------------


(2) Generating files:
MAKE TWO FILES IN .v FORMAT AS SAID EARLIER FOR VERILOG NETLIST AND FOR THE TESTBENCH

(my files were sv.v and stb.v)

-----------------------------------

(3) Compiling the iverilog:
iverilog -o my_simulation.vvp sv.v sbt.v
--------------------------------



(4) To run the simulation:
vvp my_simulation.vvp
------------------------------------
Waveform Using GTKWave:
gtkwave iiitb_rv32i.vcd
[it will give the simulation]
[ if the vcd file is not found to be in directory then give commant : "ls -1" and see the .vcd file in the directory and run the command for GTKwave]









![image](https://github.com/user-attachments/assets/51ed6a2c-f11d-4d2d-afb0-b7d75c446537)

![image](https://github.com/user-attachments/assets/472870db-fc98-4531-87a9-cd52dbc91fb4)





---------------------------------------------------------
---------------------------------------------------------
### 5-Stage RISC Pipeline Detailed Breakdown

The 5-stage RISC pipeline is an essential structure that allows processors to handle multiple instructions simultaneously in different stages, improving overall throughput and execution efficiency. Below is a more detailed look at each stage, including additional signals and processes:

---

### **1. Instruction Fetch (IF) Stage:**
**Signals:**
- **IF_ID_IR (Instruction Register):** Holds the instruction fetched from memory. This is a temporary register used to store the instruction for decoding in the next cycle.
- **IF_ID_NPC (Next Program Counter):** Holds the address of the next instruction to be fetched. This is calculated as `PC + 4` in most RISC architectures, where instructions are 4 bytes long.

**Process:**
- The **Program Counter (PC)** holds the address of the current instruction. In the IF stage, the instruction at the current PC address is fetched from memory.
- The **PC** is incremented by 4 (since each instruction is typically 4 bytes in length) to point to the next instruction.
- The **Instruction Register (IR)** holds the fetched instruction temporarily for the next stage.
- The **Next Program Counter (NPC)** is updated to hold the address of the next instruction to be fetched. The value of NPC is calculated as the PC + 4, preparing for the next instruction fetch.

**Key Points:**
- Fetching occurs sequentially, but the pipeline ensures that the processor is always fetching new instructions in parallel with decoding and executing others.

---

### **2. Instruction Decode (ID) Stage:**
**Signals:**
- **ID_EX_A:** The first operand (register value) read from the register file, as specified by the instruction.
- **ID_EX_B:** The second operand (register value) read from the register file, if applicable to the instruction.
- **ID_EX_IMMEDIATE:** This is the immediate value extracted from the instruction, if the instruction is of a type that uses immediates (e.g., I-type, S-type).
- **ID_EX_IR:** Holds the instruction that was fetched in the IF stage, which is now being decoded.

**Process:**
- The instruction fetched in the IF stage is now **decoded** to determine what operation needs to be performed and which operands are involved.
- The instruction specifies registers, and the **register file** is accessed to retrieve the operand values for the operation.
- For **I-type** and **S-type** instructions (like `ADDI` or `SW`), the immediate value is extracted from the instruction itself and passed along to the next stages.
- The **Control Unit** decodes the instruction to generate control signals that dictate the operation type (e.g., ALU operation, memory access, etc.).
- The **instruction** is passed along with the read operands and immediate values to the next stage (Execution).

**Key Points:**
- Decoding identifies whether the instruction involves arithmetic, logic, memory access, or branch operations.
- The instruction's fields (opcode, registers, immediate) are used to configure the execution stage and determine the necessary actions.

---

### **3. Execution (EX) Stage:**
**Purpose:**  
This stage performs the actual operation, whether it’s arithmetic, logical, or memory address calculation.

**Operations:**
- **Arithmetic and Logical Operations:**  
   For **R-type instructions** (e.g., `ADD`, `SUB`, `AND`), the **Arithmetic Logic Unit (ALU)** performs the specified operation on the operands passed from the ID stage. The ALU is configured by control signals generated during the decode phase to determine which operation to execute (e.g., addition, subtraction).
   
- **Address Calculation for Memory Operations:**  
   For **I-type** and **S-type** instructions (e.g., `LW`, `SW`), the EX stage computes the effective memory address. This is done by adding the base register value (from the register file) to the **immediate value** extracted from the instruction. For example:
   - In **`LW`**, the address for the memory operation is calculated as `Base + Immediate`.
   - In **`SW`**, a similar address computation happens, but it uses the register values and stores the data at that address.
   
- **Branch Decision:**  
   For branch instructions (like **BEQ**, **BNE**), the **ALU** computes the target address based on the immediate value and the current PC. The branch condition is also evaluated in this stage to determine if the instruction should be taken or not.

**Key Points:**
- This stage is crucial for performing all calculations (arithmetic, logical, memory addressing) and determining where memory accesses (loads/stores) will occur.

---

### **4. Memory (MEM) Stage:**
**Purpose:**  
This stage is responsible for reading from or writing to memory, depending on the type of instruction.

**Operations:**
- **Load Operations (e.g., `LW`):**  
   The **calculated address** from the EX stage is used to access the **data memory**. The data located at this address is then read and passed to the next stage (Write-back).
   
- **Store Operations (e.g., `SW`):**  
   In the case of **store** instructions, data from the **register file** (passed from the ID stage) is written to the memory address calculated during the EX stage.
   
- **Memory Access Control:**  
   The **Memory Unit** handles the read or write operation. In a typical RISC processor, the memory is byte-addressable, so the address and data sizes must align with the instruction set requirements (e.g., 32-bit words).

**Key Points:**
- Memory operations are handled in this stage, allowing for direct data transfer between registers and memory.
- If the instruction does not require memory access (e.g., an arithmetic operation), this stage is skipped.

---

### **5. Write-back (WB) Stage:**
**Purpose:**  
The final stage where the result of the operation is written back into the **register file**, making it available for future instructions.

**Operations:**
- **Load Instructions (`LW`):**  
   The result obtained from memory (data read from memory in the MEM stage) is written back into the **destination register**. This allows future instructions to use the loaded data.
   
- **Arithmetic Operations (e.g., `ADD`, `SUB`):**  
   For instructions that perform arithmetic or logical operations, the result computed in the **EX stage** is written back into the **destination register** specified by the instruction.

**Key Points:**
- This stage completes the instruction execution by ensuring the result (either data from memory or the result of an arithmetic operation) is written to the correct register.
- The write-back to the register file ensures that subsequent instructions can use the result of the current instruction.

---

### **Pipeline Summary and Key Considerations:**
- **Parallelism:**  
   The 5-stage pipeline allows for instruction-level parallelism, where different stages of multiple instructions can execute concurrently. While one instruction is being executed, another can be decoded, and yet another can be fetched.
   
- **Data Hazards:**  
   Data hazards can occur when one instruction depends on the result of a previous instruction. These hazards are typically managed with techniques such as forwarding (passing data directly between stages) or stalling (pausing the pipeline until the required data is available).
   
- **Control Hazards:**  
   Control hazards occur when branching instructions change the flow of execution. These can be managed by techniques like branch prediction and branch delay slots.

- **Pipelining Efficiency:**  
   In an ideal scenario, the pipeline operates with maximum efficiency, but in practice, stalls and hazards can reduce throughput. Techniques like instruction reordering, out-of-order execution, and other optimizations are used to maintain high throughput in modern processors.

In summary, the 5-stage RISC pipeline ensures that instructions are processed efficiently by dividing the process into smaller, manageable stages. Each stage performs a specific task, enabling multiple instructions to be processed simultaneously in different stages, significantly enhancing the processor's throughput.
