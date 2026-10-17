---
study_order: 7
tags:
  - GATE/CS
  - GATE/OS
  - Processes
aliases:
  - PCB
  - Task Control Block
  - Process Descriptor
date_created: 2026-05-12
difficulty: ⭐⭐
last_revised: 2026-05-12
pyq_frequency: Medium
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Process]]
Sibling Topics: [[Process States]], [[Context Switching]]
Leads To: [[CPU Scheduling]], [[Memory Management]]

GATE Syllabus Line: "Processes, Threads... Process Management."

Exam Weight Note: Often appears as a "Which of the following is NOT in a PCB?" question.

## The Problem This Solves

If the OS pauses a process to run another one, it needs a "Save Game" file. When it comes back to the first process, it must know exactly where it left off, what the variable values were, and what files were open.

Analogy: A PCB is like a **Passport** for a process. It contains its ID, its current status, where it's been (accounting), and what it's allowed to do (permissions).

Core Idea: The PCB is a data structure used by the OS to store all the information about a process.

## Formal Theory

The OS maintains a **Process Table**, which is an array of PCBs (one for each process).

### Attributes in a PCB
1. **Process ID (PID)**: A unique integer identifier for the process.
2. **Process State**: Current state ([[Process States]]) — New, Ready, etc.
3. **Program Counter (PC)**: The address of the next instruction to be executed.
4. **CPU Registers**: Includes accumulators, index registers, stack pointers, etc. (Saved during [[Context Switching]]).
5. **CPU Scheduling Information**: Priority, pointers to scheduling queues.
6. **Memory Management Information**: Page tables, segment tables, or base/limit registers.
7. **Accounting Information**: CPU time used, time limits, execution ID.
8. **I/O Status Information**: List of open files, I/O devices allocated.

What GATE actually tests here: The fact that the **Program Counter** and **Registers** are part of the PCB is crucial for understanding how processes resume.

## Diagrams and Visuals

### PCB Structure in Memory
```text
+---------------------------+
|        Process ID         |
+---------------------------+
|       Process State       |
+---------------------------+
|      Program Counter      |
+---------------------------+
|       CPU Registers       |
+---------------------------+
|   Scheduling Information  |
+---------------------------+
|     Memory Management     |
+---------------------------+
|    I/O & Open Files       |
+---------------------------+
|           ...             |
+---------------------------+
```

## Complexity Analysis
- **Access Time**: $O(1)$ if the PID is used as an index into the Process Table.
- **Space Complexity**: Fixed size per process (e.g., a few KBs), total space is $O(Max\_Processes)$.

## Intuition Anchors

**The Mental Model:**
The PCB is the **"Soul"** of the process. If you move the PCB to another machine (conceptually), you move the process. The "Body" is the memory image (Code/Data).

**The One-Line Recall:**
PCB = ID + State + PC + Registers + Memory Info + I/O Info.

**The #1 Trap:**
Thinking that the **Code (Text)** or **Data** itself is inside the PCB. **Correction**: The PCB only contains *pointers* to memory (page tables), not the actual user data or code.

## GATE Questions

**Question 1 — [GATE-style] — [1-mark]**
> Which of the following is NOT typically stored in a Process Control Block (PCB)?
- (A) Process ID
- (B) Program Counter
- (C) User Data
- (D) List of open files

<details>
<summary>Solution</summary>

**Answer: (C)**

**Reasoning:**
User data is stored in the **Data** or **Stack** sections of the process's address space, not in the kernel-level PCB structure. The PCB tracks the process, it doesn't hold its application-level variables.

</details>

## Edge Cases and Failure Modes
- [ ] **Kernel Memory Exhaustion**: If too many processes are created, the kernel might run out of space for PCBs even if there is plenty of user RAM.
- [ ] **Zombie Process**: A process that has finished execution but still has an entry in the Process Table (PCB exists) because its parent hasn't read its exit status.

## Comparisons

| Item | In PCB? | In User Memory? |
|------|---------|-----------------|
| PID | Yes | No |
| PC | Yes | No |
| Global Variables | No | Yes (Data) |
| Heap Pointers | No | Yes (Stack/Data) |
| Page Tables | Yes | No |

## Connections Web
**Must know before:**
- [[Process]]

**Topics that build on this:**
- [[Context Switching]] — specifically uses the PCB.
- [[CPU Scheduling]] — uses priority info in PCB.
- [[Memory Management]] — uses page table pointers in PCB.
- [[Zombie and Orphan Processes]]

**Standard references:**
- [[Silberschatz Chapter 3.1.3]]

## Quick Revision Sheet
- **Purpose**: Store process metadata for management and context switching.
- **Key Fields**: PID, State, PC, Registers, Memory Limits, Open Files.
- **Location**: Kernel Memory.
- **Mnemonic**: **S**ome **P**eople **R**ead **M**any **I**nteresting **A**ccounts (**S**tate, **P**C, **R**egisters, **M**emory, **I**/O, **A**ccounting).

## Revision Checklist
- [ ] I can list at least 6 items found in a PCB.
- [ ] I understand why the PC is stored in the PCB.
- [ ] I know that the PCB is stored in Kernel memory.
- [ ] I can explain the difference between a PCB and a process's address space.
助けが必要ですか？
