---
study_order: 26
tags:
  - GATE/CS
  - GATE/OS
  - Synchronization
aliases:
  - Turn Variable Approach
  - Strict Alternation
date_created: 2026-05-22
difficulty: ⭐⭐
last_revised: 2026-05-22
pyq_frequency: High
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Critical Section Problem]]
Sibling Topics: [[Lock Variable Approach]], [[Interest Variable Approach]]
Leads To: [[Peterson's Solution]]

GATE Syllabus Line: "Software solutions: Strict Alternation."

## The Problem This Solves

This approach ensures that processes take turns in a fixed sequence. It's like a game where you can only move after the other person has moved.

**Core Idea:** A shared variable `turn` indicates whose turn it is. $P_0$ can only enter if `turn == 0`, and $P_1$ only if `turn == 1`. After leaving, they switch the turn to the other.

## Formal Theory

### The Algorithm
```
Shared variable: int turn = 0;

Process P0:
    while (turn != 0);  // Entry
    /* Critical Section */
    turn = 1;           // Exit
    /* Remainder */

Process P1:
    while (turn != 1);  // Entry
    /* Critical Section */
    turn = 0;           // Exit
    /* Remainder */
```

### Correctness Analysis
1. **Mutual Exclusion:** Satisfied. `turn` cannot be both 0 and 1 simultaneously.
2. **Bounded Waiting:** Satisfied. Each process waits at most one turn of the other.
3. **Progress:** **FAILED.** 

### Why Progress Fails
If $P_0$ is much faster than $P_1$:
1. $P_0$ enters CS, sets `turn = 1`, and moves to its remainder section.
2. $P_1$ is not ready to enter CS (remains in remainder).
3. $P_0$ wants to enter CS *again*.
4. $P_0$ is stuck in `while (turn != 0)` because `turn` is 1.
5. `turn` will only become 0 when $P_1$ finishes its CS.
6. Thus, $P_1$ (which is in its remainder section) is blocking $P_0$ from entering. **Progress Violated.**

## Diagrams and Visuals

**State Diagram of Progress Violation:**
```mermaid
graph LR
    A[P0 in Remainder] -- turn=0 --> B[P0 in CS]
    B -- turn=1 --> C[P0 in Remainder]
    C -- Wants to enter --> D[P0 Stuck: turn=1]
    E[P1 in Remainder] -- Doing nothing --> D
```

## Intuition Anchors

**The Analogy:**
Two roommates sharing a car. Rule: "I use it Monday, you use it Tuesday, regardless of whether you actually need it." If you don't need the car on Tuesday, it just sits there, and I can't use it even if I have an emergency.

**The #1 Trap:**
GATE often asks: "Does this solution allow a process to enter the CS twice in a row?" 
Answer: No. This is the definition of strict alternation, and it's exactly why it violates Progress.

**The One-Line Recall:**
Strict Alternation satisfies Mutex but **violates Progress** because a process in its remainder section can block another.

## GATE Questions

**Question 1 — [PYQ: GATE 2016]**
Consider two processes $P_0$ and $P_1$ using a shared variable `turn`. 
If $P_0$ finishes its critical section and sets `turn = 1`, but $P_1$ never enters its critical section, then $P_0$:
- (A) Can enter the CS again immediately.
- (B) Will be blocked from entering the CS again.
- (C) Will cause a deadlock.
- (D) Will violate Mutual Exclusion.

<details>
<summary>Solution</summary>
**Answer: (B)**
As per the code, $P_0$ needs `turn == 0` to enter. Since `turn` is now 1 and $P_1$ isn't changing it, $P_0$ is blocked. This is a violation of Progress.
</details>

## Quick Revision Sheet
- **Approach:** Turn variable.
- **Mutex:** Yes.
- **Bounded Wait:** Yes.
- **Progress:** **No** (Strict dependency on other process).
- **Key Insight:** Remainder section interference.
