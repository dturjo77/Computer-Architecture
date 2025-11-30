### General Purpose Registers (GPR) – Exam-Focused Explanation  
(Computer Organization & Architecture / Microprocessor)

#### What is a Register?
- A register is the **fastest memory** inside the CPU.
- It is used to hold data **temporarily** during processing.
- Size: usually 8-bit, 16-bit, 32-bit or 64-bit depending on the processor (e.g., 8086 → 16-bit, 80386 onward → 32-bit, modern x86-64 → 64-bit).

#### Types of Registers (as per your diagram)
There are two broad categories:

| Type                     | Meaning                                 | Usage Example                                      | Can be used by programmer? |
|--------------------------|-----------------------------------------|----------------------------------------------------|----------------------------|
| **General Purpose Register (GPR)** | Multi-purpose, flexible registers       | Storing variables, intermediate results, addresses, counters, arithmetic/logic operations | YES (freely)              |
| **Dedicated / Special Purpose Register** | Fixed job decided by CPU designer       | Program Counter (PC), Stack Pointer (SP), Flags, Instruction Register (IR), Accumulator (in some architectures) | Usually NO or restricted  |

Your first image highlights **General Purpose Register (GPR)**.

#### General Purpose Registers (GPR) – Key Points for Exam

1. **Purpose**
   - Used for **arithmetic & logical operations**
   - Temporary **storage of data**
   - Holding **memory addresses** (pointers)
   - Passing **parameters** and returning values in functions

2. **Why “General Purpose”?**
   - The programmer can use them for **almost any task** (unlike dedicated registers which have fixed roles).

3. **Examples in Popular Processors (most asked in university exams)**

| Processor   | General Purpose Registers (GPRs)                         | Total GPRs | Size     |
|-------------|----------------------------------------------------------|------------|----------|
| 8085        | B, C, D, E, H, L (A is accumulator → sometimes treated separately) | 6 or 7     | 8-bit    |
| 8086/8088   | AX, BX, CX, DX                                           | 4          | 16-bit   |
|             | (Each can be used as AH+AL, BH+BL, etc. → 8-bit halves)  |            |          |
| 80386+ (32-bit) | EAX, EBX, ECX, EDX, ESI, EDI, EBP, ESP                   | 8          | 32-bit   |
| x86-64 (64-bit) | RAX, RBX, RCX, RDX, RSI, RDI, RBP, RSP, R8–R15           | 16         | 64-bit   |
| ARM (32-bit)| R0 – R12                                                 | 13         | 32-bit   |
| RISC-V (RV64) | x0 (zero) – x31                                          | 32         | 64-bit   |

4. **Common Conventional Uses** (very important for exams – examiners love asking “conventional use of BX” etc.)

| Register | Conventional / Most Common Use in 8086/8088                |
|----------|------------------------------------------------------------|
| AX       | Accumulator – primary register for arithmetic, I/O, function return |
| BX       | Base register – often holds memory address (offset)        |
| CX       | Counter – used in loops (LOOP, REP instructions)           |
| DX       | Data – used with AX for 32-bit operations, I/O ports       |
| SI       | Source Index – source pointer in string operations         |
| DI       | Destination Index – destination pointer in string ops     |
| BP       | Base Pointer – for stack frame in functions                |
| SP       | Stack Pointer – points to top of stack (dedicated)         |

Note: SP, IP/PC, Flag register are **not** GPRs because they have fixed jobs.

#### Key Exam Questions & Answers

1. **What is the difference between General Purpose and Dedicated registers?**  
   → GPRs can be used for any purpose by the programmer.  
   → Dedicated registers have a specific fixed function (e.g., PC, SP, Flags).

2. **How many general purpose registers are there in 8086?**  
   → 4 (AX, BX, CX, DX). Sometimes people count SI, DI, BP also → total 7 usable as GPR.

3. **Why are GPRs faster than RAM?**  
   → They are inside the CPU, made of flip-flops, no bus delay.

4. **Name any four general purpose registers of 8086.**  
   → AX, BX, CX, DX

5. **Which register is used as default counter in loop instructions?**  
   → CX (Count register)

#### Summary Table for Quick Revision (copy into notes)

| Feature                   | General Purpose Register (GPR)      | Dedicated Register             |
|---------------------------|-------------------------------------|--------------------------------|
| Flexibility               | High (any task)                     | Low (fixed job)                |
| Programmer control        | Full                                | Restricted                     |
| Examples (8086)           | AX, BX, CX, DX, SI, DI, BP          | SP, IP, Flags, IR              |
| Speed                     | Fastest                             | Fastest (same level)           |
| Total in modern x86-64    | 16 (RAX–R15)                        | ~10–15 special ones            |

This is exactly how the topic is taught and asked in university semester exams (VTU, Anna University, Mumbai University, JNTU, etc.). Memorize the table and conventional uses – you’ll score full marks in 4–8 mark questions. Good luck!

---
### Shift Operations – Exam-Oriented Explanation  
(Computer Organization & Architecture / Microprocessor – 4–8 marks guaranteed question)

#### What is Shift Operation?
Shift means moving all bits of a register/memory left or right by one or more positions.  
It is the fastest way to multiply or divide by powers of 2.

| Operation          | Effect on Value                  | Example (8-bit)                  |
|--------------------|----------------------------------|----------------------------------|
| Logical Shift Left | × 2 for each shift               | 00000101 × 2 → 00001010          |
| Logical Shift Right| ÷ 2 (unsigned division)          | 00001010 ÷ 2 → 00000101          |
| Arithmetic Shift Right| ÷ 2 (preserves sign for signed numbers) | 10001010 (-118) → 11000101 (-59) |

#### Types of Shift Operations (MOST IMPORTANT FOR EXAM)

| Type                  | Direction | What enters from left/right? | What happens to lost bit? | Sign bit preserved? | Used for |
|-----------------------|-----------|------------------------------|---------------------------|---------------------|----------|
| **Logical Shift Left (SHL / SAL)** | ← Left    | 0 enters from right (LSB)    | MSB is lost → goes to Carry Flag (CF) | No              | Multiply by 2, clear register |
| **Logical Shift Right (SHR)** | → Right   | 0 enters from left (MSB)     | LSB is lost → goes to CF | No (sign can change) | Unsigned division by 2 |
| **Arithmetic Shift Right (SAR)** | → Right   | MSB (sign bit) is copied back| LSB lost → CF            | Yes                 | Signed division by 2 |
| **Rotate Left (ROL)**        | ← Cyclic  | MSB goes to LSB & also to CF  | Nothing lost             | —                   | Bit testing, encryption |
| **Rotate Right (ROR)**       | → Cyclic  | LSB goes to MSB & also to CF | Nothing lost             | —                   | Same as above |
| **Rotate thru Carry (RCL, RCR)** | Cyclic with Carry flag | Involves Carry flag          | Nothing lost             | —                   | Multi-word shifts |

#### Visual Summary (Exactly as in your image – memorize this)

| Direction | Logical Shift                  | Arithmetic Shift                | Rotate                          |
|-----------|--------------------------------|---------------------------------|---------------------------------|
| Right →   | 0 comes in from left<br>LSB lost to CF | Sign bit copied in<br>LSB lost to CF | LSB goes to MSB<br>No loss      |
| Left ←    | 0 comes in from right<br>MSB lost to CF | Same as logical left (SAL = SHL) | MSB goes to LSB<br>No loss      |

#### Exam-Favorite Numerical Examples (8-bit)

1. **SHL (Logical Shift Left)**  
   Before: 1011 0101  
   SHL 1 → 0110 1010  (MSB 1 lost → CF=1)

2. **SHR (Logical Shift Right)**  
   Before: 1011 0101  
   SHR 1 → 0101 1010  (0 filled, LSB 1 → CF=1)

3. **SAR (Arithmetic Shift Right)** – Signed number  
   Before: 1011 0101 (-75 in 2’s complement)  
   SAR 1 → 1101 1010 (-38)  ← sign bit 1 preserved

4. **ROL (Rotate Left)**  
   Before: 1011 0101  
   ROL 1 → 0110 1011  (1 from MSB moved to LSB)

#### Most Commonly Asked University Exam Questions & Answers

| Question                                                                 | Answer |
|--------------------------------------------------------------------------|--------|
| Difference between SHR and SAR?                                          | SHR fills 0 from left → changes sign of negative numbers.<br>SAR copies sign bit → preserves sign (correct signed division). |
| What is the fastest way to multiply a number by 4?                       | SHL twice (or SHL by 2 positions) → ×4 |
| What is the fastest way to divide a signed number by 8?                  | SAR 3 times |
| After SHR 1, where does the bit that goes out appear?                    | In Carry Flag (CF) |
| Difference between Shift and Rotate?                                     | Shift: bits that go out are lost.<br>Rotate: bits circle back, nothing is lost. |
| Which instruction is used for signed division by power of 2?             | SAR |
| SAL and SHL are same or different?                                       | Exactly same instruction (both opcodes do logical left shift) |
| How to check if a number is odd/even using shift?                        | SHR 1 → if CF=1 → odd, CF=0 → even |

#### Quick Revision Table (Copy into last page of answer sheet)

| Instruction | Full Name               | Fills with        | Preserves Sign? | Use Case                     |
|-------------|-------------------------|-------------------|-----------------|------------------------------|
| SHL/SAL     | Shift Logical Left      | 0 from right      | No              | ×2, ×4, ×8 …                |
| SHR         | Shift Logical Right     | 0 from left       | No              | Unsigned ÷2                  |
| SAR         | Shift Arithmetic Right  | Sign bit copied   | Yes             | Signed ÷2                    |
| ROL         | Rotate Left             | Cyclic            | —               | Bit manipulation             |
| ROR         | Rotate Right            | Cyclic            | —               | Encryption, serial data      |

Memorize the diagram and the table above → you will get full 8 marks in any “Explain shift and rotate operations with diagram” question.  
All the best for your exam!

---

