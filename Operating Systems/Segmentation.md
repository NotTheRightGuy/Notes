---
study_order: 42
tags:
  - GATE/CS
  - GATE/OperatingSystems
  - MemoryManagement
aliases:
  - Memory Segmentation
  - Segmented Memory
date_created: 2026-06-09
difficulty: ⭐⭐⭐
last_revised: 2026-06-09
pyq_frequency: Medium
---

## Syllabus Position

**Subject:** [[Operating Systems Index]]
**Parent Topic:** [[Memory Management]]
**Sibling Topics:** [[Paging]], [[Contiguous Memory Allocation]], [[Fragmentation]]
**Leads To:** [[Virtual Memory]], [[Segmentation with Paging]]

> 📍 **GATE Syllabus Mapping:** Memory management: paging and segmentation.

**Exam Weight Note:** Frequently tested as a 2-mark NAT or MCQ focusing on address translation calculations, limit checks, and comparison with [[Paging]].

---

## 💡 Motivation & Intuition

### The Problem
Imagine you are writing a large software project. You have a main program, several functions, a global data area, and a stack. In [[Contiguous Memory Allocation]], the OS sees your program as one giant, monolithic block of bytes. But as a programmer, your "view" of memory is different. You think of your program as a collection of logical units (segments). If the stack grows too large or a function is added, the monolithic block approach fails to adapt gracefully without wasting space.

### The Analogy
Segmentation is like a **Library organized by Genres**.
- **Contiguous Allocation** is like having one long shelf where every book must be placed in order of arrival. If a new "History" book arrives and there's no space at the end of the history section, you have to move everything.
- **Paging** is like a library where every book is exactly the same size, and you put them in fixed-size slots regardless of genre.
- **Segmentation** is like having separate shelves for "Fiction," "Science," and "History." Each shelf (segment) can be a different length. You can grow the "Science" shelf without moving the "Fiction" shelf, as long as there is empty space somewhere in the library.

**Core Idea (one sentence):** Segmentation is a memory management scheme that supports the user's view of memory as a collection of variable-sized logical units.

---

## 📖 Theory

### Formal Definition
**Segmentation** is a non-contiguous memory management scheme where the [[Logical Address Space]] is a collection of segments. Each segment has a name and a length. Addresses specify both the **segment name** and the **offset** within the segment.

### Logical Address Structure
In a segmented system, a [[Logical Address]] is a pair:
$$\langle \text{segment-number}, \text{offset} \rangle$$
Represented as: $(s, d)$
- $s$: Index into the **Segment Table**.
- $d$: Displacement (offset) within the segment.

### The Segment Table
To map these logical addresses to [[Physical Address Space]], the OS maintains a **Segment Table**. Each entry in the table (Segment Table Entry - STE) consists of:
1. **Base:** The starting physical address where the segment resides in memory.
2. **Limit:** The length of the segment.

### Address Translation Hardware
When a process generates a logical address $(s, d)$:
1. The segment number $s$ is used as an index into the segment table.
2. The hardware checks if the offset $d$ is valid: **Is $0 \le d < \text{Limit}$?**
3. If $d \ge \text{Limit}$, a **[[Segmentation Fault]]** (trap) is generated.
4. If valid, the physical address is calculated as:
   $$\text{Physical Address} = \text{Base} + d$$

### Protection and Sharing
Segments represent logical units (like a code block or a shared library), making it easy to attach protection bits:
- **Read/Write/Execute bits:** A "Code" segment can be marked Read-Only and Execute-Only.
- **Sharing:** Two processes can share a segment by having their segment table entries point to the same physical [[Base Address]]. This is more "natural" than sharing pages because segments align with logical boundaries.

---

## 🖼️ Diagrams & Visuals

### Address Translation Flow (Mermaid)

```mermaid
graph TD
    CPU[CPU generates Logical Address: s, d] --> Index[Index s into Segment Table]
    Index --> Check{Is d < Limit?}
    Check -- No --> Trap[Segmentation Fault / Trap]
    Check -- Yes --> Add[Physical Address = Base + d]
    Add --> RAM[Access Physical Memory]
    
    subgraph Segment Table
    STE[Limit | Base]
    end
```

### Segment Table Lookup (ASCII)

```text
Logical Address: [ s |  d ]
                   |    |
           ________|    |
          |             |
    Segment Table       |
   +-------+-------+    |
 s | Limit |  Base |    |
   +-------+-------+    |
   |  ...  |  ...  |    |     (d < Limit?)
   +-------+-------+    |________ YES _______
          |                                  |
          |            (Addition)            v
          +----------------(+)-------------> Physical Address
                            ^
                            |
```

---

## ⏱️ Complexity Analysis

### Time Complexity
- **Address Translation:** $O(1)$
  - Hardware lookup in the Segment Table is a constant time operation.
  - However, it requires an extra memory access to fetch the table entry (mitigated by a [[TLB]] - Translation Lookaside Buffer).

### Space Complexity
- **Internal Fragmentation:** $0$
  - Since segments are sized exactly to the logical unit's needs, no space is wasted *inside* a segment.
- **External Fragmentation:** **High**
  - Because segments are variable-sized and must be loaded contiguously into physical memory, "holes" develop between segments over time.
- **Table Overhead:** $O(S)$ where $S$ is the number of segments. Typically $S$ is much smaller than the number of pages in [[Paging]], so the table itself is smaller.

---

## 🔢 Worked Example

**Scenario:** Consider a system with the following Segment Table:

| Segment | Limit | Base |
|---------|-------|------|
| 0       | 500   | 1000 |
| 1       | 200   | 2500 |
| 2       | 350   | 4000 |

**Translate the following logical addresses $(s, d)$:**

1. **Address $(0, 420)$:**
   - Step 1: $s=0, d=420$.
   - Step 2: Check $d < \text{Limit} \implies 420 < 500$? Yes.
   - Step 3: Physical Address $= \text{Base} + d = 1000 + 420 = 1420$.

2. **Address $(1, 250)$:**
   - Step 1: $s=1, d=250$.
   - Step 2: Check $d < \text{Limit} \implies 250 < 200$? **No**.
   - Result: **Segmentation Fault**. (Offset exceeds segment size).

3. **Address $(2, 100)$:**
   - Step 1: $s=2, d=100$.
   - Step 2: Check $d < \text{Limit} \implies 100 < 350$? Yes.
   - Step 3: Physical Address $= 4000 + 100 = 4100$.

---

## 🧠 Intuition Anchors

**The Mental Model:**
Picture an accordion. Each segment is an accordion fold that can expand or contract to its specific size. When you lay several accordions on a floor, you might have gaps between them where no accordion fits (External Fragmentation), but every bit of the accordion's own paper is used (No Internal Fragmentation).

**The One-Line Recall:**
Segmentation = User's view + Variable-sized blocks + Base/Limit Table + **External Fragmentation**.

**The #1 Trap:**
**Confusing Offset checks with Page checks.** In [[Paging]], the offset $d$ *cannot* exceed the page size because the hardware defines it by bit-length (e.g., 12 bits for 4KB). In **Segmentation**, the offset $d$ is checked against a *software-defined* **Limit** register. GATE loves to give an offset larger than the limit to see if you trigger a fault.

---

## 🎯 GATE Questions

**Question 1 — (GATE-style) — 2-mark NAT**
A system uses segmentation. A process has a segment with Base $= 2000$ and Limit $= 800$. What is the physical address corresponding to logical address offset $550$? If the offset is $850$, what happens?

<details>
<summary>💡 Solution (click to reveal)</summary>

**Part A (Offset 550):**
- Check: $550 < 800$? Yes.
- Physical Address $= 2000 + 550 = 2550$.

**Part B (Offset 850):**
- Check: $850 < 800$? No.
- Result: **Trap/Segmentation Fault**.

**What this tests:** Basic understanding of the Limit register check.
</details>

---

**Question 2 — (Conceptual) — 1-mark MCQ**
Which of the following is TRUE regarding Segmentation?
- (A) It suffers from Internal Fragmentation.
- (B) It requires fixed-size memory blocks.
- (C) It allows for easier sharing of procedures/data than Paging.
- (D) The logical address space is contiguous.

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (C)**

**Reasoning:**
- (A) False. Segmentation suffers from External, not Internal fragmentation.
- (B) False. Segments are variable-sized.
- (C) **True**. Because segments correspond to logical units (functions, libraries), sharing a single segment table entry is simpler and more logical.
- (D) False. The user sees it as a collection of non-contiguous segments.

</details>

---

**Question 3 — (Advanced) — 2-mark MCQ**
In a combined **[[Segmentation with Paging]]** scheme, the CPU generates a logical address. What is the correct order of translation?
- (A) Paging Table $\to$ Segment Table $\to$ Physical Address
- (B) Segment Table $\to$ Page Table $\to$ Physical Address
- (C) Both are checked in parallel.
- (D) None of the above.

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (B)**

**Reasoning:**
In modern systems (like x86), the logical address is first mapped to a **linear address** using the Segment Table. This linear address is then treated as a virtual address and translated to a physical address using the Page Table.
**Sequence:** Logical $(s, d) \xrightarrow{\text{Seg Table}}$ Linear Address $\xrightarrow{\text{Page Table}}$ Physical Address.

</details>

---

## ⚠️ Edge Cases & Traps

- [ ] **Offset == Limit:** The check is strictly $d < \text{Limit}$. If $d = \text{Limit}$, it is a **Segmentation Fault** (just like array index `arr[size]` is out of bounds).
- [ ] **Base + Offset Overflow:** Ensure the calculated physical address doesn't exceed the total physical memory size.
- [ ] **Sharing and Permissions:** If two processes share a segment, they might have different permissions (one Read-Only, one Read-Write) in their respective segment table entries.
- [ ] **External Fragmentation Fix:** Requires **Compaction**, which is expensive as it involves moving segments in memory.

---

## ⚖️ Comparisons

| Feature           | [[Contiguous Allocation]] | [[Paging]]            | [[Segmentation]]       |
| ----------------- | ------------------------- | --------------------- | ---------------------- |
| **Unit Size**     | Whole Process             | Fixed-size Pages      | Variable-sized Segments |
| **Fragmentation** | External                  | Internal              | External               |
| **User's View**   | Monolithic                | Not visible           | Logical Units          |
| **Hardware**      | Relocation Register       | Page Table            | Segment Table          |
| **Sharing**       | Difficult                 | Possible (Page level) | Easy (Logical level)   |

---

## 🧠 Memory Hooks

1. **Mnemonic:** **S-L-B** (Segment - Limit - Base). Always check **Limit** before adding **Base**.
2. **Visual Metaphor:** Segments are like "Files" on a disk. Files are variable-sized and can be shared, but if you store them contiguously, the disk gets fragmented.
3. **Quick Formula:** 
   $$ \text{Valid If: } d < \text{Limit} \implies \text{Phys} = \text{Base} + d $$

---

## 🕸️ Connections Web

**Prerequisite Knowledge:**
- [[Memory Management]] — general concepts.
- [[Logical Address Space]] vs [[Physical Address Space]] — the core mapping problem.

**Builds Upon This Topic:**
- [[Segmentation with Paging]] — how modern OSs combine both.
- [[Virtual Memory]] — implementing segmentation with swapping.

**GATE Subject Links:**
- [[Operating Systems Index]] — [[Memory Management]]

**Standard References:**
- [[Galvin Chapter 8]] — Main reference for Memory Management.
- [[Stallings Section 7.4]] — Detailed look at Segmentation.

---

## ✅ Quick Revision Sheet

- **Definition:** Mapping user-defined logical units (segments) to physical memory.
- **Address:** $(s, d)$. $s = $ index, $d = $ offset.
- **Translation:** If $d < \text{Limit}$, then Physical $= \text{Base} + d$. Else, Fault.
- **Pros:** No internal fragmentation, logical sharing/protection.
- **Cons:** **External fragmentation** (requires compaction).
- **Table Entry:** Contains **Base Address** and **Limit (Size)**.
- **Mnemonic:** "Segments size varies, Pages size stays."

---

## ✅ Revision Checklist

- [ ] I can explain why segmentation has no internal fragmentation.
- [ ] I can derive a physical address from a segment table and detect a fault.
- [ ] I understand the difference between $d < \text{Limit}$ and paging's power-of-2 offset.
- [ ] I can compare Paging and Segmentation across 3+ criteria.
- [ ] I have linked this to [[Segmentation with Paging]].

---
