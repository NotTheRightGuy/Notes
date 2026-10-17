---
study_order: 4
tags:
  - GATE/CS
  - GATE/Computer Organization
  - Instruction Addressing
aliases:
  - Addressing Modes
  - Operand Addressing
  - Effective Address
date_created: 2026-07-11
difficulty: ⭐⭐⭐⭐
last_revised: 2026-07-11
pyq_frequency: High
---

## Syllabus Position

Subject: [[Computer Organization & Architecture]]
Parent Topic: [[Instruction Set Architecture]]
Sibling Topics: [[Instruction Format]], [[Opcode Technique]]
Leads To: [[Pipelining]], [[Memory Hierarchy]]

GATE Syllabus Line: Instruction set architecture, instruction formats, addressing modes, and machine language.

Exam Weight Note: Often appears as 1-mark MCQ on effective address calculation and as 2-mark questions on indexed, base, and indirect addressing.

## The Problem This Solves

A processor must tell not just what operation to perform, but where the operand lives. Hard-coding every memory location would make instructions long and inflexible, while using only registers would limit access to large data. Addressing modes solve this by letting the same opcode reach data in registers, memory, constants, or computed locations. They are the CPU’s way of saying, “Use this operand, but interpret this field in the right way.”

Analogy: addressing mode is like choosing how to read a map coordinate. Sometimes the coordinate points directly to the destination, sometimes it points to a place that contains another clue, and sometimes it means “start here and walk this far.”

Core Idea (one sentence): An addressing mode defines how to interpret instruction fields to compute the **[[effective address]]** or retrieve the operand value.

## Formal Theory

### Formal definition
An **[[Addressing Mode]]** is the rule that maps an instruction’s address-related fields to an operand location or value. The computed target is often called the **effective address** $EA$.

### Common addressing modes

#### Immediate addressing
The operand value is inside the instruction itself.

$$Operand = A$$

Use: constants, loop bounds, small literals.

#### Register addressing
The operand is in a register named by the instruction.

$$Operand = R_i$$

Use: fastest access, no memory lookup.

#### Direct addressing
The instruction field gives the memory address directly.

$$EA = A$$

Then operand is fetched from memory at $EA$.

#### Indirect addressing
The instruction field points to a memory location that contains the actual address.

$$EA = M[A]$$

This adds one more memory access and supports pointer-like behavior.

#### Register indirect addressing
The register contains the memory address.

$$EA = (R_i)$$

#### Indexed addressing
The effective address is base plus an index.

$$EA = A + (R_i)$$

Useful for arrays because the index register changes while the base stays fixed.

#### Base-plus-offset addressing

$$EA = (R_b) + d$$

where $d$ is a displacement encoded in the instruction.

#### Relative addressing

$$EA = PC + d$$

Used heavily in branches because the target stays near the current instruction.

### Variants and special forms
- **Auto-increment**: use register-indirect, then increment the register.
- **Auto-decrement**: decrement first, then use the register.
- **Scaled indexed**: $EA = (R_b) + (R_i \times s) + d$ for array elements with stride $s$.

### Pseudocode: effective address calculation

```
Algorithm COMPUTE_EA(mode, A, R, PC):
    if mode = immediate:
        return A
    if mode = register:
        return R[A]
    if mode = direct:
        return A
    if mode = indirect:
        return Memory[A]
    if mode = indexed:
        return A + R[index]
    if mode = base_plus_offset:
        return R[base] + A
    if mode = relative:
        return PC + A
```

What GATE actually tests here: identify the mode from a description, compute effective address, distinguish direct vs indirect, and compare register-relative versus PC-relative usage.

## Diagrams and Visuals

1. Draw a table showing each addressing mode and its path to the operand.

ASCII approximation:

```
Instruction field A ---> [A] -----------------> operand
Register R ------------> [R] -----------------> operand
Memory[A] -------------> [A] -> [M[A]] ------> operand
PC + d ---------------------------------------> branch target
```

Labels: `A` = address field, `R` = register, `M[A]` = memory contents at address A.

2. Draw indexed array access:

```
Base B -----------+
                  +---- EA = B + i
Index i ----------+

Array:  [x0][x1][x2][x3]
          ^
         EA
```

3. Mermaid flow for selection:

```mermaid
graph TD
    I[Instruction] --> M{Mode?}
    M -- Immediate --> V[Use value in instruction]
    M -- Direct --> D[EA = A]
    M -- Indirect --> N[EA = M[A]]
    M -- Base/Index --> B[EA = base + offset]
    M -- Relative --> P[EA = PC + d]
```

## Complexity Analysis

Addressing modes are not asymptotic algorithms, but they do affect instruction latency and memory traffic.

- **Immediate / register addressing**: $O(1)$ operand access, because no extra memory reference is needed.
- **Direct / indexed / base-plus-offset**: $O(1)$ to compute EA, plus one memory access for the operand.
- **Indirect addressing**: one extra memory read for the pointer, so it has higher constant cost.

Complexity Summary Table:

| Case | Time Complexity | Space Complexity | Trigger Condition |
|------|-----------------|------------------|-------------------|
| Best Case | $O(1)$ | $O(1)$ | Immediate or register mode |
| Average Case | $O(1)$ | $O(1)$ | Typical EA computation |
| Worst Case | $O(1)$ with larger constant | $O(1)$ | Indirect mode with extra memory reference |

Justification: the instruction format already contains the mode bits, so the decoder chooses one finite hardware path. The cost changes by constant factors, not by input size.

## Worked Example

Suppose memory starts with the following values:
- $R_1 = 1000$
- $R_2 = 8$
- $PC = 200$
- Memory[1008] = 45
- Memory[1000] = 700

Instruction: `LOAD R0, 8(R1)`

This is base-plus-offset addressing.

Step 1: Identify base register $R_1 = 1000$.
Step 2: Offset $d = 8$.
Step 3: Compute effective address.
$$EA = (R_1) + d = 1000 + 8 = 1008$$
Step 4: Fetch operand from memory.
$$Operand = M[1008] = 45$$
Step 5: Load $R_0 \leftarrow 45$.

State trace:
- Before: $R_0 = ?$, $R_1 = 1000$, Memory[1008] = 45
- After EA: $EA = 1008$
- After load: $R_0 = 45$

Now compare with indirect addressing: `LOAD R0, (R1)` would give $EA = M[1000] = 700$, then operand would come from Memory[700], not Memory[1000]. That is the key difference GATE likes to test.

What changes if the instruction is PC-relative? Then the base is $PC$ instead of a general-purpose register, which makes branch targets position-independent.

## GATE Questions

**Question 1 — GATE-style — 1-mark**

In indirect addressing, which of the following is true?

- (A) The instruction field itself is the operand
- (B) The field gives an address of the actual address
- (C) The field always stores a register number
- (D) The operand is computed using only the PC

<details>
<summary>Solution</summary>

**Answer: (B)**

**Reasoning:** Indirect addressing uses the instruction field to point to memory that contains the actual address. Option (A) is immediate, (C) is register addressing, and (D) is relative addressing.

**What this question is really testing:** distinction among immediate, register, indirect, and PC-relative modes.

**Trap to avoid:** confusing direct and indirect addressing.

</details>

**Question 2 — Conceptual / Numerical — 2-mark**

Given $R_3 = 500$ and an instruction `ADD R1, 20(R3)`, what is the effective address?

- (A) 20
- (B) 500
- (C) 520
- (D) 480

<details>
<summary>Solution</summary>

**Answer: (C)**

**Reasoning:** Base-plus-offset means $EA = (R_3) + 20 = 500 + 20 = 520$. The operand is fetched from Memory[520].

</details>

**Question 3 — Hard / Multi-concept — 2-mark**

Why is PC-relative addressing preferred for branches in position-independent code?

<details>
<summary>Solution</summary>

**Reasoning:** PC-relative branches encode the target as an offset from the current instruction. That means the same code can run correctly even if loaded at a different memory address, because the branch target shifts along with the code. It also keeps branch fields small when targets are usually nearby.

**What this question is really testing:** relation between instruction encoding, relocation, and address computation.

</details>

Pattern Recognition:
- If the question shows parentheses, think register-indirect or base-plus-offset.
- If it mentions a branch, suspect PC-relative mode.
- If it asks about performance, remember indirect has an extra memory reference.
- If it asks for the address itself, distinguish EA from operand value.

## Edge Cases and Failure Modes

- [ ] Input of size 0 or 1
  - Wrong assumption: every operand requires memory access.
  - What happens: immediate mode may need no memory fetch at all.
  - Fix: identify whether the operand is embedded in the instruction.
- [ ] All elements identical / repeated state
  - Wrong assumption: direct and indirect address the same location.
  - What happens: direct gives the address; indirect gives the contents at that address.
  - Fix: track one extra dereference.
- [ ] Overflow / address wraparound
  - Wrong assumption: $EA = base + offset$ always fits.
  - What happens: address arithmetic can overflow machine word size.
  - Fix: check address width and sign extension rules.
- [ ] Off-by-one in displacement
  - Wrong assumption: branch offsets count from the current PC without pipeline adjustments.
  - What happens: some ISAs define branch displacement relative to the next instruction.
  - Fix: read the ISA rule carefully.
- [ ] Infinite loop / non-termination
  - Wrong assumption: indirect chains always terminate.
  - What happens: pointer loops can create repeated dereferences in software emulation.
  - Fix: limit dereference depth where relevant.
- [ ] Topic-specific failure: confusing EA with operand value
  - Wrong assumption: computed address is the data.
  - What happens: you answer Memory[EA] incorrectly when the question only asks for EA.
  - Fix: always separate address computation from memory access.

## Comparisons

| Feature | [[Addressing Mode]] | [[Opcode Technique]] | [[Instruction Format]] |
|----------------------|-----------------------|-----------------------|-----------------------|
| Time Complexity | $O(1)$ per access | $O(1)$ decode path | $O(1)$ decode path |
| Space Complexity | fixed instruction bits | fixed instruction bits | fixed instruction bits |
| Key Property | how operand is found | what operation is done | how fields are laid out |
| When to Prefer | when computing operand location | when choosing operation encoding | when designing instruction words |
| GATE Trap | EA vs operand confusion | opcode bits vs total bits | field boundaries and bit positions |

The most common GATE question comparing these is a small instruction format or assembly snippet asking which part determines the operation and which part determines the operand location. The answer hinges on separating opcode meaning from addressing interpretation.

## Memory Hooks

- Mnemonic: `I D R B P` = Immediate, Direct, Register, Base-plus-offset, PC-relative.
- Visual metaphor: opcode picks the verb; addressing mode picks the path to the object.
- Common trap warning: if you see parentheses, do not jump straight to the data. First ask whether the parentheses mean address, pointer, or offset.
- Quick recall formula: `EA = base + offset`, `EA = PC + d`, `EA = M[A]`.

## Connections Web

**Prerequisite Knowledge:**
- [[Binary Arithmetic]] — for adding base and offset
- [[Registers]] — for register-based operand locations
- [[Memory Addressing]] — for interpreting physical/logical addresses
- [[Instruction Set Architecture]] — because modes are part of ISA design

**Builds Upon This Topic:**
- [[Opcode Technique]]
- [[Instruction Format]]
- [[Pipelining]]
- [[Memory Hierarchy]]

**GATE Subject Links:**
- [[Computer Organization & Architecture]]
- [[Assembly Language]]
- [[Machine Code]]

**Cross-Subject Connections:**
- [[Operating Systems]] — relocation and virtual memory affect address interpretation
- [[Compilers]] — code generation chooses addressing modes for arrays and branches

**Standard References:**
- [[Patterson & Hennessy]]
- [[Computer Organization and Design]]
- [[Hamming Code]] — not directly related, but both depend on bit-field discipline

## Revision Checklist

- [ ] I can define addressing mode and effective address.
- [ ] I can compute EA for direct, indirect, indexed, base-plus-offset, and PC-relative modes.
- [ ] I can explain why indirect mode costs more than immediate mode.
- [ ] I can distinguish EA from operand value in one glance.
- [ ] I can solve the worked example without looking.

How would GATE test this? Usually as a one-line assembly fragment or a bit-pattern question where one wrong dereference or wrong PC base changes the answer.
