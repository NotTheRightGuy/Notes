---
study_order: 27
tags:
  - GATE/CS
  - GATE/OS
  - Synchronization
aliases:
  - Flag Variable Approach
date_created: 2026-05-22
difficulty: ⭐⭐
last_revised: 2026-05-22
pyq_frequency: Low
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Critical Section Problem]]
Sibling Topics: [[Lock Variable Approach]], [[Strict Alternation]]
Leads To: [[Peterson's Solution]] (The combination of Flag + Turn)

## The Problem This Solves

Instead of forcing turns, let processes announce their interest.

**Core Idea:** Use an array `flag[2]`. `flag[i] = true` means process $P_i$ wants to enter the CS.

## Formal Theory

### The Algorithm (Version 1: Deadlock Prone)
```
Shared variable: boolean flag[2] = {false, false};

Process Pi:
    flag[i] = true;      // I am interested
    while (flag[j]);     // Wait if other is interested (j = 1-i)
    /* Critical Section */
    flag[i] = false;     // Done
```

### The Failure: Deadlock
If both processes set their flags to `true` at the exact same time:
1. $P_0$ sets `flag[0] = true`.
2. **Context Switch**.
3. $P_1$ sets `flag[1] = true`.
4. Both processes reach the `while` loop.
5. $P_0$ waits for `flag[1]` to be false.
6. $P_1$ waits for `flag[0]` to be false.

**Result:** Both wait forever. **Progress Violated** (Deadlock).

### Alternative: Mutex Violation
If we swap the lines (check first, then set):
```
while (flag[j]);
flag[i] = true;
```
This is just a [[Lock Variable Approach]] with separate flags—it fails **Mutual Exclusion** because both can pass the `while` loop before either sets their flag.

## Intuition Anchors

**The #1 Trap:**
Assuming that because each process has its own flag, they won't interfere. In version 1, they interfere by being "too polite"—both step aside and wait for the other.

**The One-Line Recall:**
Interest Variable alone leads to **Deadlock** if both signal interest before checking.

## Connections Web
- [[Critical Section Problem]]
- [[Deadlock]]
- [[Peterson's Solution]] (Fixes this by adding a `turn` variable to break the tie).

## Quick Revision Sheet
- **Approach:** Process-specific flags.
- **Problem:** If both set flags simultaneously, they deadlock.
- **Requirement Violated:** Progress.
