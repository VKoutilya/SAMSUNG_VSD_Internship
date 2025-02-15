TASk 3 :


"1) List various RISC-V instruction type (R, I, S, B, U, J) after going through RISC-V software documentation

2) Identify 15 unique RISC-V instructions from riscv-objdmp of your application code 

3) Identify exact 32-bit instruction code in the instruction type format for 15 unique instructions

4) Upload the 32-bit pattern on Github"


(i) R- TYPE

The R-Type is an instruction format in the RISC-V architecture used for performing arithmetic and logical operations between registers. It is structured as follows:

opcode (6-0): This field identifies the operation to be performed, such as addition, subtraction, AND, OR, etc.

rd (11-7): This field specifies the destination register where the result of the operation will be stored after execution.

funct3 (14-12): This 3-bit field helps specify the exact operation within the given opcode category (e.g., distinguishing between ADD and SUB operations).

rs1 (19-15): The first source register that holds one of the operands for the operation.

rs2 (24-20): The second source register, which contains the other operand for the operation.

funct7 (31-25): This 7-bit field provides additional operation details, allowing for variations of instructions that share the same opcode and funct3 values.



(ii) I-TYPE

The I-Type instruction format in RISC-V is used for operations that involve a combination of immediate values and registers. The format is organized as follows:

*opcode (6-0): This field determines the specific operation to execute, such as loading data or adding an immediate value.

rd (11-7): This indicates the destination register where the result of the operation will be stored after execution.

funct3 (14-12): A 3-bit field that specifies the type of operation within the broader opcode category (for example, differentiating between ADDI and LW operations).

rs1 (19-15): The first source register that holds one of the operands used in the operation.

imm[11:0] (31:20): A 12-bit immediate value, which is a constant directly embedded within the instruction. This constant serves as one of the operands in the instruction.



(iii) S-TYPE

he S-Type instruction format in RISC-V is used for operations involving store instructions, where data is written to memory. The structure is as follows:

opcode (6-0): Specifies the operation to be performed, such as store word or store half-word.

funct3 (14-12): A 3-bit field that defines the specific store operation (e.g., distinguishing between SW and SH).

rs1 (19-15): The source register containing the base address for memory access.

rs2 (24-20): The source register containing the data to be stored in memory.

imm[11:5] (31:25) and imm[4:0] (11:7): The immediate value is split into two parts. The immediate represents the offset to the memory address and is used in combination with the base address from rs1.




(iv) U-TYPE

The U-Type instruction format in RISC-V is used for operations that involve large immediate values. The structure is as follows:

opcode (6-0): Specifies the operation to be performed, such as Load Upper Immediate (LUI) or Add Upper Immediate to PC (AUIPC).

rd (11-7): The destination register where the result of the operation will be stored.

imm[31:12] (31:12): A 20-bit immediate value used for loading large constants. This value is shifted left by 12 bits and placed in the upper portion of the register.






(v) B-TYPE The B-Type instruction format in RISC-V is used for branch operations that determine the control flow of a program. The structure is as follows:

opcode (6-0): Specifies the branch operation, such as branch if equal (BEQ) or branch if not equal (BNE).

funct3 (14-12): A 3-bit field that specifies the condition of the branch (e.g., comparing equality, inequality, etc.).

rs1 (19-15): The first source register, which is compared to the second source register for the branch condition.

rs2 (24-20): The second source register, which is compared to rs1 for the branch decision.

imm[12] (31:31), imm[10:5] (30:25), imm[4:1] (11:8), and imm[11] (7:7): The immediate value is used to calculate the offset for the branch. The instruction uses these fields to construct the target address for the branch.






(vi) J-TYPE

The J-Type instruction format in RISC-V is used for unconditional jump operations. The structure is as follows:

opcode (6-0): Specifies the jump operation, such as Jump and Link (JAL).

rd (11-7): The destination register, where the return address (the address of the next instruction) is stored.

imm[20] (31:31), imm[10:1] (30:21), imm[11] (20:20), and imm[19:12] (19:12): The immediate value used to calculate the target address for the jump. The instruction fields are combined to form the full 20-bit immediate value, which is then used to determine the jump target relative to the current instruction.






![image](https://github.com/user-attachments/assets/84df9c3a-2228-48e4-bc23-0c3d29993b94)




1.  lui a0, 0x21 (Address: 100b0) Instruction Type: U-Type Explanation: Loads the immediate value 0x21 into the upper 20 bits of the register a0.
2. addi sp, sp, -16  (Address: 100b4) Instruction Type: I-Type Explanation: Adds an immediate value -16 to the sp register, effectively reserving 16 bytes of space on the stack.

3.li a2, 15 (Address: 100b8) Instruction Type: I-Type Explanation: Loads the immediate value 15 into register a2. Internally, it is equivalent to addi a2, x0, 15.

4.addi a0, a0, 384(Address: 100c0) Instruction Type: I-Type Explanation: Adds the immediate value 384 to the value in register a0. 6.sd ra, 8(sp)(Address: 100c4) Instruction Type: S-Type Explanation: Stores the value in register ra at the memory address sp + 8. This is used for storing data to memory.

5.jal ra, 10408(Address: 100c8) Instruction Type: J-Type Explanation: The jal instruction jumps to the target address 10408 and stores the return address in register ra.



6.addi sp, sp, 16(Address: 100d4) Instruction Type: I-Type Explanation: Adds the immediate value 16 to the sp register, effectively restoring the stack pointer after reserving space.

7.li a1, 0 (Address: 100bc) Instruction Type: I-Type Explanation: Loads the immediate value 0 into register a1. Internally, it is equivalent to addi a1, x0, 0.


8.ret(Address: 100d8) Instruction Type: I-Type (mapped to jalr) Explanation: Returns from the function by jumping to the address stored in ra, equivalent to jalr x0, ra, 0.

9.li a2, 0 (Address: 100b8) Instruction Type: I-Type Explanation: Loads the immediate value 0 into register a2. Internally, it is equivalent to addi a3, x0, 0.

10.li a3, 0 (Address: 100b8) Instruction Type: I-Type Explanation: Loads the immediate value 0 into register a3. Internally, it is equivalent to addi a3, x0, 0.
