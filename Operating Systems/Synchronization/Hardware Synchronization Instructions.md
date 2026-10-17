---
study_order: 29
tags:
  - GATE/CS
  - GATE/OS
  - Synchronization
aliases:
  - TSL
  - TestAndSet
  - Atomic Instructions
date_created: 2026-05-22
difficulty: ⭐⭐⭐
last_revised: 2026-05-22
pyq_frequency: Medium
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Critical Section Problem]]
Sibling Topics: [[Peterson's Solution]], [[Semaphores]]

## The Problem This Solves

Software solutions like the [[Lock Variable Approach]] fail because "Read-and-Modify" is not atomic. Hardware solutions solve this by providing special instructions that perform these steps as a single, uninterruptible operation.

## Formal Theory

### 1. TestAndSet (TSL)
The `TestAndSet` instruction does the following **atomically**:
1. Reads the value of a memory location.
2. Sets the value of that location to `true`.
3. Returns the original (old) value.

**Code:**
```
boolean TestAndSet(boolean *target) {
    boolean rv = *target;
    *target = true;
    return rv;
}

// Usage:
while (TestAndSet(&lock)); // Busy Wait
/* Critical Section */
lock = false;
```

### 2. Swap (XCHG)
The `Swap` instruction atomically exchanges the values of two memory locations.

**Code:**
```
void Swap(boolean *a, boolean *b) {
    boolean temp = *a;
    *a = *b;
    *b = temp;
}

// Usage:
key = true;
while (key == true) Swap(&lock, &key);
/* Critical Section */
lock = false;
```

## Correctness
- **Mutual Exclusion:** Guaranteed by atomicity.
- **Progress:** Guaranteed.
- **Bounded Waiting:** **NOT Guaranteed** in the simple version. A process could keep losing the race to grab the lock. (Special complex versions of TSL can provide Bounded Waiting).

## Intuition Anchors

**The One-Line Recall:**
Hardware instructions like TSL fix the [[Lock Variable Approach]] by making **Check-and-Set** atomic.

## Quick Revision Sheet
- **TSL:** Returns old value, sets new to true.
- **Swap:** Exchanges two values.
- **Pros:** Simple, works for any number of processes.
- **Cons:** Busy waiting, potential starvation (no bounded waiting).
