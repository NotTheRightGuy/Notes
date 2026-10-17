---
study_order: 28
tags:
  - GATE/CS
  - GATE/OS
  - Synchronization
aliases:
  - Peterson's Algorithm
date_created: 2026-05-22
difficulty: ⭐⭐⭐⭐
last_revised: 2026-05-22
pyq_frequency: High
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Critical Section Problem]]
Sibling Topics: [[Strict Alternation]], [[Interest Variable Approach]]
Leads To: [[Hardware Synchronization Instructions]], [[Semaphores]]

GATE Syllabus Line: "Peterson's solution for two processes."

## The Problem This Solves

[[Strict Alternation]] violated Progress. [[Interest Variable Approach]] led to Deadlock. Peterson's Solution combines both to create a perfect software-based solution for **two processes**.

**Core Idea:** Use both **Interest** (to show intent) and **Turn** (to break ties/deadlocks). It's like two people at a narrow door: "I want to go (Flag), but after you (Turn)."

## Formal Theory

Peterson's solution is a classic software-based solution for the [[Critical Section Problem]] that works for two processes ($P_0$ and $P_1$).

### The Algorithm
```
Shared variables:
    boolean flag[2] = {false, false}; // Intent
    int turn;                         // Tie-breaker

Process Pi (i is 0 or 1, j is 1-i):
    flag[i] = true;                   // Step 1: Signal Interest
    turn = j;                         // Step 2: Give turn to other (Yield)
    while (flag[j] && turn == j);     // Step 3: Wait condition

    /* Critical Section */

    flag[i] = false;                  // Step 4: Release Interest
    
    /* Remainder Section */
```

### Proof of Correctness

#### 1. Mutual Exclusion
To enter CS, $P_i$ needs `flag[j] == false` OR `turn == i`. 
If both $P_0$ and $P_1$ try to enter:
- Both set `flag[0]=true` and `flag[1]=true`.
- The `turn` variable will eventually be either 0 or 1 (it's a single shared variable).
- If `turn == 0`, $P_1$ stays in the `while` loop, and $P_0$ enters.
- If `turn == 1`, $P_0$ stays in the `while` loop, and $P_1$ enters.
- **Result:** Only one can enter.

#### 2. Progress
If $P_j$ is in the Remainder Section, then `flag[j] == false`.
When $P_i$ wants to enter:
- It sets `flag[i]=true` and `turn=j`.
- The `while` condition `flag[j] && turn == j` becomes `false` because `flag[j]` is false.
- $P_i$ enters immediately.
- **Result:** $P_j$ does not block $P_i$ from outside.

#### 3. Bounded Waiting
Suppose $P_i$ is waiting in the `while` loop. $P_j$ is in CS.
- When $P_j$ exits, it sets `flag[j] = false`.
- If $P_j$ immediately tries to re-enter, it sets `flag[j] = true` but **it must set `turn = i`**.
- Now $P_i$'s `while` condition `flag[j] && turn == j` (where $j$ is $1-i$) becomes `flag[j] && turn == i`, which is false because `turn` is now $i$.
- $P_i$ enters.
- **Result:** $P_i$ waits at most one entry of $P_j$.

## Diagrams and Visuals

**Logic Flow:**
```mermaid
graph TD
    A[Start Pi] --> B[flag[i] = true]
    B --> C[turn = j]
    C --> D{Other interested AND turn is theirs?}
    D -- Yes --> D
    D -- No --> E[Critical Section]
    E --> F[flag[i] = false]
    F --> G[Remainder Section]
```

## Complexity Analysis

| Case | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Best Case** | $O(1)$ (No contention) | $O(1)$ |
| **Worst Case**| $O(\text{Busy Wait})$ | $O(1)$ |

- **Auxiliary Space:** 1 array of 2 booleans + 1 integer.
- **Hardware Assumption:** Peterson's assumes that **Load** and **Store** operations on `flag` and `turn` are [[Atomic Operations]]. On modern out-of-order processors, it may fail without "memory barriers."

## Worked Example

$P_0$ and $P_1$ both want to enter.
1. $P_0$ sets `flag[0] = true`, `turn = 1`.
2. $P_1$ sets `flag[1] = true`, `turn = 0`.
3. $P_0$ checks `while(flag[1] && turn == 1)`. Since `turn` is 0, condition is FALSE.
4. $P_0$ enters CS.
5. $P_1$ checks `while(flag[0] && turn == 0)`. Since `turn` is 0, condition is TRUE.
6. $P_1$ waits.
7. $P_0$ leaves, `flag[0] = false`.
8. $P_1$'s loop condition `flag[0] && turn == 0` becomes FALSE. $P_1$ enters.

## Intuition Anchors

**The Analogy:**
Two polite people at a door.
- "I want to go" (`flag = true`).
- "But you go first" (`turn = other`).
- If you both say "after you," the one who said it *last* is the one who actually waits, because they overwrote the `turn` variable.

**The Mental Model:**
The `flag` is the **Request**. The `turn` is the **Tie-breaker**. You wait only if you have requested AND it is the other person's turn to break the tie.

**The #1 Trap:**
Thinking Peterson's works for $N$ processes. It doesn't. For $N$ processes, we need [[Bakery Algorithm]]. Also, Peterson's uses **Busy Waiting**, which wastes CPU cycles.

## GATE Questions

**Question 1 — [PYQ: GATE 2007] — [2-mark]**
The wait condition for Peterson's solution for process $P_i$ is `while (flag[j] && turn == j)`. What happens if we change it to `while (flag[j] || turn == j)`?
- (A) Mutual Exclusion is violated.
- (B) Progress is violated (Deadlock).
- (C) Bounded Waiting is violated.
- (D) It still works correctly.

<details>
<summary>Solution</summary>
**Answer: (B)**
If $P_i$ sets `turn = j`, and the condition is `OR`, then $P_i$ will wait simply because `turn == j`, even if $P_j$ is not interested (`flag[j] == false`). If both processes are at the entry, they will both be stuck because one will see `turn == j` and the other will see `turn == i`.
</details>

## Edge Cases and Failure Modes

- [ ] **Modern CPUs:** Compilers or CPUs might reorder `flag[i] = true` and `turn = j`. If `turn = j` happens first, Mutex can be violated. (Fix: Memory Barriers).
- [ ] **Single Core:** On a single core, busy waiting is useless unless the OS preempts the waiting process to let the other one finish.

## Comparisons

| Feature | [[Strict Alternation]] | [[Interest Variable]] | [[Peterson's Solution]] |
| :--- | :--- | :--- | :--- |
| **Processes** | 2 | 2 | 2 |
| **Mutex** | Yes | No/Deadlock | **Yes** |
| **Progress** | No | No (Deadlock) | **Yes** |
| **Mechanism** | Turn only | Flag only | **Flag + Turn** |

## Connections Web
- [[Critical Section Problem]]
- [[Bakery Algorithm]] ($N$-process version)
- [[Busy Waiting]]
- [[Memory Barriers]]

## Quick Revision Sheet
- **Peterson's:** Software solution for 2 processes.
- **Variables:** `flag[2]` (Interest), `turn` (Tie-breaker).
- **Entry:** `flag[i]=true; turn=j; while(flag[j] && turn==j);`
- **Exit:** `flag[i]=false;`
- **Success:** Mutex, Progress, Bounded Waiting.
- **Downside:** Busy waiting, only 2 processes.

## Revision Checklist
- [ ] I can write the 4 lines of Peterson's from memory.
- [ ] I can explain why `turn = j` is necessary (tie-breaking).
- [ ] I can prove why it satisfies Progress.
- [ ] I know it's only for 2 processes.
