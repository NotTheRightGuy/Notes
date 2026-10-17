---
study_order: 17
tags:
  - GATE/CS
  - GATE/OS
  - scheduling/SRTF
aliases:
  - Shortest Remaining Time First
  - Preemptive SJF
date_created: 2026-05-18
difficulty: ⭐⭐⭐⭐
last_revised: 2026-05-18
pyq_frequency: Very High
---

## Syllabus Position
Subject: [[Operating Systems]]
Parent Topic: [[CPU Scheduling Algorithms MOC]]
Sibling Topic: [[SJF]]

GATE Syllabus Line: CPU Scheduling Algorithms.

## The Problem This Solves
Even if a job is running, if a new job arrives that can finish faster than the current one, it's better to switch to the new job to keep average wait times low.

Core Idea: Always run the process with the smallest **Remaining** Burst Time.

## Formal Theory
**SRTF** is the **preemptive** version of [[SJF]]. 

### Characteristics
- **Criteria**: Remaining [[Burst Time]].
- **Preemption**: Occurs whenever a new process arrives with a shorter $BT$ than the remaining time of the current process.
- **Optimality**: Even more optimal than SJF in environments where processes arrive dynamically.

## Worked Example (Tricky Trace)
Processes:
- P1: AT=0, BT=8
- P2: AT=1, BT=4
- P3: AT=2, BT=9
- P4: AT=3, BT=5

**Step-by-step Trace:**
1. $t=0$: P1 starts. Remaining $BT=8$.
2. $t=1$: P2 arrives ($BT=4$). P1 has 7 left. $4 < 7$, so **Preempt P1**, Start P2.
3. $t=2$: P3 arrives ($BT=9$). P2 has 3 left. $3 < 9$, continue P2.
4. $t=3$: P4 arrives ($BT=5$). P2 has 2 left. $2 < 5$, continue P2.
5. $t=5$: P2 finishes. Queue: P1(7), P3(9), P4(5). Smallest is P4. Run P4.
6. $t=10$: P4 finishes. Queue: P1(7), P3(9). Run P1.
7. $t=17$: P1 finishes. Run P3.
8. $t=26$: P3 finishes.

**Gantt Chart:**
| P1 (0-1) | P2 (1-5) | P4 (5-10) | P1 (10-17) | P3 (17-26) |

**Avg WT Calculation:**
- P2: $CT=5, TAT=5-1=4, WT=4-4=0$
- P4: $CT=10, TAT=10-3=7, WT=7-5=2$
- P1: $CT=17, TAT=17-0=17, WT=17-8=9$
- P3: $CT=26, TAT=26-2=24, WT=24-9=15$
- **Avg WT** = $(0+2+9+15)/4 = 6.5$

## Intuition Anchors
- **The Context Switch King**: SRTF can have many context switches.
- **The #1 Trap**: Forgetting to update the *remaining* time of the current process when comparing.

## GATE Questions
**Question 1 (GATE 2011)**:
Consider 4 processes with ATs (0, 1, 2, 3) and BTs (8, 4, 9, 5). Find avg WT using SRTF.
- (A) 6.5
- (B) 7.5
- (C) 5.5
- (D) 4.5
<details>
<summary>Solution</summary>
Answer: (A). (Trace provided in Worked Example above).
</details>

## Quick Revision Sheet
- **Criteria**: Min Remaining Time.
- **Mode**: Preemptive.
- **Starvation**: Yes.
- **Overhead**: High due to frequent context switching.
- **Best Case**: Optimal Avg WT.
