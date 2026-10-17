---
study_order: 16
tags:
  - GATE/CS
  - GATE/OS
  - scheduling/SJF
aliases:
  - Shortest Job First
  - SPN
date_created: 2026-05-18
difficulty: ⭐⭐⭐
last_revised: 2026-05-18
pyq_frequency: High
---

## Syllabus Position
Subject: [[Operating Systems]]
Parent Topic: [[CPU Scheduling Algorithms MOC]]
Leads To: [[SRTF]], [[HRRN]]

GATE Syllabus Line: CPU Scheduling Algorithms.

## The Problem This Solves
In [[FCFS]], a long process can block many short ones. If we always pick the shortest task first, we minimize the average waiting time for the whole group.

Analogy: In a supermarket, if you have 50 items and the person behind you has 1, letting them go first drastically reduces their wait without adding much to yours.

Core Idea: CPU is assigned to the process with the smallest [[Burst Time]].

## Formal Theory
**SJF** is **non-preemptive**. Once a process starts, it won't stop until finished, even if a shorter process arrives later.

### Characteristics
- **Criteria**: [[Burst Time]] ($BT$).
- **Mode**: Non-preemptive.
- **Optimality**: It is **optimal**—it gives the minimum average waiting time for a fixed set of processes.

## Complexity Analysis
- **Finding Shortest**: $O(\log n)$ if using a min-heap, $O(n)$ if searching an array.
- **Starvation**: Possible. Long processes may never get CPU if short ones keep arriving.

## Worked Example
Processes:
- P1: AT=0, BT=7
- P2: AT=2, BT=4
- P3: AT=4, BT=1
- P4: AT=5, BT=4

**Gantt Chart Trace:**
1. At $t=0$: Only P1 is there. Run P1.
2. At $t=7$: P1 finishes. P2, P3, P4 are in ready queue.
3. $BT(P2)=4, BT(P3)=1, BT(P4)=4$. Shortest is P3. Run P3.
4. At $t=8$: P3 finishes. P2, P4 available. Both have $BT=4$. Pick P2 (lower AT).
5. At $t=12$: P2 finishes. Run P4.
6. At $t=16$: P4 finishes.

| P1 (0-7) | P3 (7-8) | P2 (8-12) | P4 (12-16) |

## Intuition Anchors
- **The Optimal One**: Remember SJF = Min Avg WT.
- **The #1 Trap**: Forgetting it's non-preemptive. If a shorter job arrives at $t=1$ while a long one started at $t=0$, SJF *will not* switch. [[SRTF]] will.

## GATE Questions
**Question 1 (GATE-style)**:
SJF is optimal because:
- (A) It maximizes throughput.
- (B) It minimizes average waiting time.
- (C) It avoids starvation.
- (D) It is easy to implement.

<details>
<summary>Solution</summary>
Answer: (B). Proved by the fact that moving shorter jobs before longer ones reduces total wait time more than it increases the wait of the long job.
</details>

## Edge Cases and Failure Modes
- [ ] **Starvation**: If a stream of short jobs keeps coming, $P_{long}$ waits forever.
- [ ] **Unknown BT**: In real life, we don't know $BT$ in advance. It must be predicted using [[Exponential Smoothing]].

## Quick Revision Sheet
- **Criteria**: [[Burst Time]]
- **Mode**: Non-preemptive
- **Optimal**: Yes (for Avg WT)
- **Starvation**: Yes
- **Real-world issue**: Hard to know $BT$ beforehand.
