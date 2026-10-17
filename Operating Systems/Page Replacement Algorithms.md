---
study_order: 48
tags:
  - GATE/CS
  - GATE/OS
  - VirtualMemory
aliases:
  - Page Replacement
  - FIFO vs LRU vs OPT
date_created: 2026-06-07
difficulty: ⭐⭐⭐
last_revised: 2026-06-07
pyq_frequency: High
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Virtual Memory and Demand Paging]]
Sibling Topics: [[Thrashing]], [[Working Set Model]]
Leads To: [[Clock Algorithm]], [[Second Chance Algorithm]]

GATE Syllabus Line: "Memory management: ... page replacement algorithms."

Exam Weight Note: Very common 2-mark NAT questions. Usually requires tracing a reference string through 3 or 4 frames.

## The Problem This Solves

When using [[Demand Paging]], we might try to bring a page into memory but find that all physical **Frames** are full. We must choose an existing page to "evict" to make room. The goal is to minimize the total number of **Page Faults**.

Analogy: Imagine a small desk (RAM) that fits only 3 books. You need to read 10 different books (Reference String). When you need a new book and the desk is full, which book do you put back on the shelf? 
- FIFO: Put back the one you brought in first.
- LRU: Put back the one you haven't touched in the longest time.
- OPT: Put back the one you won't need for the longest time in the future.

Core Idea (one sentence): Strategically select a victim page for eviction to minimize the frequency of future page faults.

## Formal Theory

### 1. FIFO (First-In-First-Out)
- The page that has been in memory the longest is replaced.
- Implementation: A simple Queue.
- **Trap**: Suffers from **[[Belady's Anomaly]]** (Page faults can increase even if we increase the number of frames).

### 2. Optimal (OPT / MIN)
- Replace the page that will not be used for the longest period of time in the future.
- **Crucial**: This is an "Offline" algorithm (requires knowledge of the future). Used as a benchmark.
- Guarantees the minimum possible page faults.

### 3. LRU (Least Recently Used)
- Replace the page that has not been used for the longest period of time in the *past*.
- Uses the "Principle of Locality".
- Implementation: Counter or Stack.
- **Property**: Does NOT suffer from Belady's Anomaly (it is a "Stack Algorithm").

### 4. LRU Approximations
- **Clock / Second Chance**: Uses a "Reference Bit". If bit is 1, give it a second chance and clear bit. If 0, replace.
- **NRU (Not Recently Used)**: Categorizes pages based on Reference and Modified bits.

## Diagrams and Visuals

**Algorithm Tracing Table (Example with 3 frames):**

| Ref | 7 | 0 | 1 | 2 | 0 | 3 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| F1 | 7 | 7 | 7 | 2 | 2 | 2 |
| F2 | | 0 | 0 | 0 | 0 | 3 |
| F3 | | | 1 | 1 | 1 | 1 |
| Fault? | F | F | F | F | H | F |

## Complexity Analysis

| Algorithm | Replacement Logic | Implementation Complexity |
| :--- | :--- | :--- |
| FIFO | Head of Queue | $O(1)$ |
| OPT | Future Scan | $O(N)$ (Impossible in real-time) |
| LRU | Min Timestamp | $O(1)$ with special Hardware / $O(N)$ software |
| Clock | Circular Scan | $O(N)$ worst case (Average $O(1)$) |

## Worked Example

**Reference String:** 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5
**Frames:** 3

**LRU Trace:**
1. [1] (F)
2. [1, 2] (F)
3. [1, 2, 3] (F)
4. [4, 2, 3] (F) - 1 was least recent.
5. [4, 1, 3] (F) - 2 was least recent.
6. [4, 1, 2] (F) - 3 was least recent.
7. [5, 1, 2] (F) - 4 was least recent.
8. [5, 1, 2] (Hit) - 1 is now most recent.
9. [5, 1, 2] (Hit) - 2 is now most recent.
10. [3, 1, 2] (F) - 5 was least recent.
11. [3, 4, 2] (F) - 1 was least recent.
12. [3, 4, 5] (F) - 2 was least recent.

Total Faults (LRU): 10.

**Wait!** Compare this with FIFO for the same string (often tested together).

## Intuition Anchors

**The Mental Model:**
- **FIFO** is like a waiting line. The person who stood in line first leaves first.
- **LRU** is like a pile of clothes. You wear a shirt, then put it on top. The shirt at the very bottom is the one you haven't worn in the longest time — throw that one away.
- **OPT** is a psychic librarian.

**The #1 Trap:**
Assuming FIFO always performs better with more frames. **[[Belady's Anomaly]]** is the counter-example. LRU and OPT are immune because they are "Stack Algorithms" (the set of pages in $n$ frames is always a subset of pages in $n+1$ frames).

**The One-Line Recall:**
OPT (Future), LRU (Past), FIFO (Arrival).

## GATE Questions

**Question 1 — [GATE 2004] — [2-mark]**
Which of the following page replacement algorithms suffers from Belady's Anomaly?
- (A) FIFO
- (B) LRU
- (C) Optimal
- (D) Both (A) and (B)

<details>
<summary>Solution</summary>
**Answer: (A) FIFO**
**Reasoning:** Only FIFO (and some non-stack algorithms) show this behavior. LRU and OPT are stack algorithms and are immune.
</details>

---

**Question 2 — [GATE 2017] — [2-mark]**
Consider a system with 4 frames. Initially empty. Reference string: 1, 2, 3, 4, 2, 1, 5, 3, 2, 4, 6. How many page faults for LRU?

<details>
<summary>Solution</summary>
1. [1] (F)
2. [1, 2] (F)
3. [1, 2, 3] (F)
4. [1, 2, 3, 4] (F)
5. [1, 2, 3, 4] (Hit) - 2 used
6. [1, 2, 3, 4] (Hit) - 1 used
7. [1, 2, 5, 4] (F) - 3 was least recent (Order of use: 3, 4, 2, 1)
8. [1, 2, 5, 3] (F) - 4 was least recent (Order of use: 4, 2, 1, 5)
9. [1, 2, 5, 3] (Hit) - 2 used
10. [4, 2, 5, 3] (F) - 1 was least recent (Order of use: 1, 5, 3, 2)
11. [4, 2, 6, 3] (F) - 5 was least recent (Order of use: 5, 3, 2, 4)
**Total: 8 Faults.**
</details>

## Edge Cases and Failure Modes

- [ ] **Belady's Anomaly**: Only happens in specific strings for FIFO.
- [ ] **Initial State**: All algorithms start with $N$ faults for $N$ frames (Cold Start).
- [ ] **Cyclic References**: If memory fits $N$ pages and we cycle through $N+1$ pages, LRU and FIFO will fault on *every* access.

## Comparisons

| Feature | FIFO | LRU | OPT |
| :--- | :--- | :--- | :--- |
| Metric | Arrival Time | Usage Time | Future Need |
| Belady's? | Yes | No | No |
| Hardware Req | Low | High | Impossible |
| Practical? | Yes | Yes (Approx) | No |

## Connections Web

**Must know before:**
- [[Paging]]
- [[Virtual Memory and Demand Paging]]

**Topics that build on this:**
- [[Thrashing]] — occurs when page fault rate is too high.
- [[Belady's Anomaly]] — the weirdness of FIFO.
- [[Clock Algorithm]] — the practical version of LRU.

## Quick Revision Sheet

1. **FIFO**: Queue based. Oldest out.
2. **LRU**: Stack/Counter based. Least recently used out.
3. **OPT**: Benchmarking only. Longest future wait out.
4. **Stack Algorithms**: (LRU, OPT) No Belady's Anomaly.
5. **Belady's Anomaly**: More frames $\neq$ fewer faults (FIFO).

## Revision Checklist
- [ ] I can trace any string for FIFO/LRU/OPT without errors.
- [ ] I understand why LRU is better than FIFO.
- [ ] I can define Belady's Anomaly and name the algorithms that suffer from it.
