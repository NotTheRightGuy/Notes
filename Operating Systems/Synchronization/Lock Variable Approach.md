---
study_order: 25
tags:
  - GATE/CS
  - GATE/OS
  - Synchronization
aliases:
  - Single Lock Solution
date_created: 2026-05-22
difficulty: ⭐
last_revised: 2026-05-22
pyq_frequency: Low
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Critical Section Problem]]
Sibling Topics: [[Strict Alternation]], [[Interest Variable Approach]]
Leads To: [[TestAndSet]] (The hardware fix for this software failure)

GATE Syllabus Line: "Software solutions to the critical section problem."

## The Problem This Solves

This is the simplest, most intuitive "naive" attempt to solve the [[Critical Section Problem]]. It mimics how we use a key for a room.

**Core Idea:** Use a single shared variable `lock`. If `lock == 0`, the CS is free. If `lock == 1`, the CS is busy.

## Formal Theory

### The Algorithm
```
Shared variable: int lock = 0;

Process Pi:
    while (lock == 1);  // Entry Section (Busy Waiting)
    lock = 1;           // Acquire Lock
    /* Critical Section */
    lock = 0;           // Exit Section (Release Lock)
    /* Remainder Section */
```

### The Fatal Flaw
The entry section involves two steps: **Reading** the lock and **Writing** the lock. These are not atomic.

1. $P_0$ reads `lock == 0`.
2. **Context Switch** occurs before $P_0$ sets `lock = 1`.
3. $P_1$ reads `lock == 0`.
4. Both processes enter the Critical Section.

**Result:** [[Mutual Exclusion]] is violated.

## Diagrams and Visuals

**Trace Table:**
| Step | Process | Action | Lock Value | State |
| :--- | :--- | :--- | :--- | :--- |
| 1 | $P_0$ | `while(lock==1)` | 0 | Exits loop |
| 2 | - | **Switch to $P_1$** | 0 | - |
| 3 | $P_1$ | `while(lock==1)` | 0 | Exits loop |
| 4 | $P_1$ | `lock = 1` | 1 | **In CS** |
| 5 | $P_0$ | `lock = 1` | 1 | **In CS (Violated!)** |

## Complexity Analysis

- **Time:** $O(1)$ for entry/exit (ignoring busy waiting).
- **Space:** $O(1)$ (one shared integer).
- **Constraint:** Fails on Mutex.

## Intuition Anchors

**The #1 Trap:**
Believing that setting `lock = 1` immediately after the loop is "fast enough" to prevent others. In OS, "fast" doesn't exist—only "atomic" exists.

**The One-Line Recall:**
Lock variable fails because **Checking** and **Setting** the lock is not one atomic operation.

## GATE Questions

**Question 1 — [GATE-style]**
The lock variable approach to the critical section problem:
- (A) Satisfies Mutual Exclusion but fails Progress.
- (B) Satisfies Progress but fails Mutual Exclusion.
- (C) Satisfies both.
- (D) Fails both.

<details>
<summary>Solution</summary>
**Answer: (B)**
It fails **Mutual Exclusion** because two processes can enter simultaneously. It satisfies **Progress** because if the CS is free, a process can enter without being blocked by others (unless they are also trying to enter, which leads back to the Mutex failure).
</details>

## Connections Web

**Must know before this topic:**
- [[Critical Section Problem]]
- [[Atomic Operations]]

**Topics that build on this:**
- [[TestAndSet]] — The hardware instruction that makes this approach work by combining "Read and Set" into one atomic step.

## Quick Revision Sheet
- **Lock Variable:** Naive software approach.
- **Fail:** Violates [[Mutual Exclusion]].
- **Why:** Preemption between "Check" and "Set".
- **Hardware Fix:** [[TestAndSet]].
