---
study_order: 49
tags:
  - GATE/CS
  - GATE/OS
  - VirtualMemory
aliases:
  - Thrashing and Working Set
date_created: 2026-06-07
difficulty: ⭐⭐⭐
last_revised: 2026-06-07
pyq_frequency: Medium
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Virtual Memory and Demand Paging]]
Sibling Topics: [[Page Replacement Algorithms]], [[Demand Paging]]
Leads To: [[Load Control]]

GATE Syllabus Line: "Virtual memory: thrashing."

Exam Weight Note: Usually appears as conceptual MCQ/MSQ about CPU utilization and the relationship between degree of multiprogramming and page faults.

## The Problem This Solves

If we increase the **Degree of Multiprogramming** (number of processes in RAM) too much, each process gets fewer frames. Eventually, processes don't have enough frames to hold their "active" pages. This leads to a constant cycle of page faults, where the CPU spends more time swapping pages than executing instructions.

Analogy: Imagine a student trying to study 10 subjects at once on a tiny desk. They spend all their time putting one book away and taking another one out. They never actually get to read a single page.

Core Idea (one sentence): A state where the system is so busy swapping pages that the CPU utilization drops to near zero.

## Formal Theory

### 1. The Thrashing Curve
As the **Degree of Multiprogramming** increases:
- Initially, CPU utilization increases.
- Beyond a certain point, processes start competing for frames.
- Utilization drops sharply as page faults skyrocket.

### 2. Working Set Model ($\Delta$)
- Based on the **Locality of Reference**.
- The **Working Set** is the set of pages used by a process in the last $\Delta$ time units.
- **Goal**: Allocate enough frames to each process to house its entire working set.
- If $Total\_Working\_Set\_Size > Total\_Available\_Frames$, Thrashing occurs.

### 3. Page Fault Frequency (PFF)
- A more direct way to control thrashing.
- If Page Fault Rate > Upper Bound: Give process more frames.
- If Page Fault Rate < Lower Bound: Take frames away from process.

## Diagrams and Visuals

**CPU Utilization vs. Degree of Multiprogramming:**
```mermaid
graph LR
    A[Start] --> B[Increasing Utilization]
    B --> C[Maximum Point]
    C --> D[Thrashing Zone - Sharp Drop]
```

## Intuition Anchors

**The Mental Model:**
Picture a revolving door. If one person goes through at a time, it's efficient. If 50 people try to jam in at once, the door gets stuck. No one moves, but everyone is working hard to push. That's **Thrashing**.

**The #1 Trap:**
Thinking that adding more processes always improves performance. There is an **Optimal Degree of Multiprogramming**.

**The One-Line Recall:**
Thrashing = CPU utilization $\downarrow$ while Swapping activity $\uparrow$.

## GATE Questions

**Question 1 — [GATE 2005] — [1-mark]**
A system is thrashing. What should the OS designer do to increase CPU utilization?
- (A) Increase the degree of multiprogramming
- (B) Decrease the degree of multiprogramming
- (C) Increase the page size
- (D) Use a faster CPU

<details>
<summary>Solution</summary>
**Answer: (B) Decrease the degree of multiprogramming**
**Reasoning:** Thrashing is caused by too many processes competing for too few frames. Removing some processes frees up frames for the remaining ones, allowing them to complete their working sets.
</details>

## Edge Cases and Failure Modes

- [ ] **Global vs Local Replacement**: Local replacement can limit thrashing to a single process, but it may not prevent the entire system from slowing down if the disk is the bottleneck.
- [ ] **Wrong $\Delta$**: If $\Delta$ (working set window) is too small, it won't encompass the locality. If too large, it wastes memory.

## Connections Web

**Must know before:**
- [[Paging]]
- [[Page Replacement Algorithms]]

**Topics that build on this:**
- [[Demand Paging]]
- [[Locality of Reference]]

## Quick Revision Sheet

1. **Thrashing**: Paging activity $\uparrow$, CPU utilization $\downarrow$.
2. **Cause**: Sum of working sets > Total physical memory.
3. **Fix**: Suspend some processes (Reduce Multiprogramming).
4. **Locality**: Programs tend to access a small set of pages repeatedly for a period of time.
5. **Working Set**: The "Minimum Frames" needed to prevent thrashing.

## Revision Checklist
- [ ] I can explain the thrashing curve.
- [ ] I understand how the Working Set model prevents thrashing.
- [ ] I know why the CPU utilization drops during thrashing.
