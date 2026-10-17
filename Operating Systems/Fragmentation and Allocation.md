---
study_order: 37
tags:
  - GATE/CS
  - GATE/OS
  - MemoryManagement
aliases:
  - Memory Fragmentation
  - First Fit vs Best Fit
date_created: 2026-06-07
difficulty: ⭐⭐
last_revised: 2026-06-07
pyq_frequency: Medium
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Memory Management Overview]]
Sibling Topics: [[Paging]], [[Segmentation]]
Leads To: [[Compaction]]

GATE Syllabus Line: "Memory management: ... contiguous allocation."

Exam Weight Note: Often tested via simple numericals on First Fit, Best Fit, and Worst Fit strategies.

## The Problem This Solves

When processes are loaded and removed from memory, the free space gets broken into pieces. If the pieces are too small or scattered, we might not be able to fit a new process even if we have enough total memory.

Analogy: Imagine a parking lot where people park haphazardly. Even if there is space for 10 more cars, the gaps between cars might be too small for any single car to fit.

Core Idea (one sentence): Fragmentation is the waste of memory caused by the mismatch between available holes and requested block sizes.

## Formal Theory

### 1. Internal Fragmentation
- Occurs in **Fixed Partitioning**.
- Memory is divided into fixed slots. If a process is smaller than the slot, the leftover space *inside* the slot is wasted.
- It cannot be used by any other process.

### 2. External Fragmentation
- Occurs in **Variable Partitioning** (Contiguous).
- Total free memory exists to satisfy a request, but it is not **Contiguous**.
- Solution: **Compaction** (shuffling memory to bring all holes together) or **[[Paging]]** (non-contiguous allocation).

### 3. Allocation Strategies
To minimize fragmentation and search time:
- **First Fit**: Allocate the *first* hole that is big enough. (Fastest)
- **Best Fit**: Allocate the *smallest* hole that is big enough. (Minimizes leftover space, but creates tiny "useless" holes).
- **Worst Fit**: Allocate the *largest* hole. (Leaves the largest possible leftover hole).

## Worked Example

**Holes:** 100K, 500K, 200K, 300K, 600K
**Requests:** 212K, 417K, 112K, 426K

**First Fit Trace:**
1. 212K $\to$ Fits in 500K (Remains 288K).
2. 417K $\to$ Fits in 600K (Remains 183K).
3. 112K $\to$ Fits in 100K (No, wait) $\to$ Fits in 288K (Remains 176K).
4. 426K $\to$ **Cannot fit!** (Even though 200K + 300K are free).

**Best Fit Trace:**
1. 212K $\to$ Fits in 300K (Remains 88K).
2. 417K $\to$ Fits in 500K (Remains 83K).
3. 112K $\to$ Fits in 200K (Remains 88K).
4. 426K $\to$ Fits in 600K (Remains 174K).
**Result:** Best Fit succeeded where First Fit failed.

## Intuition Anchors

**The Mental Model:**
- **First Fit**: "I'm in a hurry, give me the first spot I see."
- **Best Fit**: "I'm a perfectionist, find the spot that fits me exactly."
- **Worst Fit**: "I'm messy, give me the biggest room so the leftovers are still big."

**The #1 Trap:**
Assuming Best Fit is always "best". Best Fit can lead to many tiny holes (External Fragmentation) that are useless for any future process.

## GATE Questions

**Question 1 — [GATE 2007] — [2-mark]**
Which of the following strategies for dynamic storage allocation is generally the fastest?
- (A) First Fit
- (B) Best Fit
- (C) Worst Fit
- (D) Next Fit

<details>
<summary>Solution</summary>
**Answer: (A) First Fit**
**Reasoning:** First Fit stops as soon as it finds a hole, whereas Best Fit and Worst Fit usually require searching the entire list to find the optimal hole.
</details>

## Quick Revision Sheet

- **Internal**: Inside block. Fix: Variable partitions.
- **External**: Between blocks. Fix: Paging or Compaction.
- **First Fit**: Fast, simple.
- **Best Fit**: Smallest sufficient hole.
- **Worst Fit**: Largest sufficient hole.
- **Compaction**: Moving processes in memory. Very high overhead (CPU intensive).

## Revision Checklist
- [ ] I can trace the 3 allocation strategies on a list of holes.
- [ ] I understand the difference between internal and external fragmentation.
- [ ] I know how Paging solves external fragmentation.
