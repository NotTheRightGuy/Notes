---
study_order: 30
tags:
  - GATE/CS
  - GATE/OS
  - Synchronization
aliases:
  - Binary Semaphore
  - Counting Semaphore
date_created: 2026-05-22
difficulty: ⭐⭐⭐
last_revised: 2026-05-22
pyq_frequency: High
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[Critical Section Problem]]
Sibling Topics: [[Peterson's Solution]], [[Hardware Synchronization Instructions]]
Leads To: [[Classical Synchronization Problems]] (Producer-Consumer, Dining Philosophers)

## The Problem This Solves

[[Peterson's Solution]] and [[Hardware Synchronization Instructions]] use **Busy Waiting**, which wastes CPU time. Semaphores provide a way to synchronize processes by putting them to **Sleep** (blocking them) when they can't enter the CS.

## Formal Theory

A **Semaphore** is an integer variable accessed only through two atomic operations: `wait()` and `signal()` (also known as $P$ and $V$).

### Types of Semaphores
1. **Binary Semaphore:** Value can only be 0 or 1. Used for Mutual Exclusion.
2. **Counting Semaphore:** Value can be any integer. Used for resource management (e.g., $N$ printers).

### Operations
```
wait(S):
    while (S <= 0); // Busy wait (in simple version) or Sleep
    S--;

signal(S):
    S++;
```

## Intuition Anchors

**The Analogy:**
A key rack in a hotel.
- `wait()`: Take a key. If no keys are left, wait in the lobby.
- `signal()`: Put the key back. If someone is waiting in the lobby, they can now take it.

## Connections Web
- [[Critical Section Problem]]
- [[Deadlock]] (Semaphores can cause deadlock if used incorrectly)
- [[Producer-Consumer Problem]]

## Quick Revision Sheet
- **Semaphore:** Integer tool for sync.
- **Wait (P):** Decrements. Blocks if $\le 0$.
- **Signal (V):** Increments. Wakes up blocked processes.
- **Key Note:** Solves the busy-waiting problem by using process queues (in OS implementation).
