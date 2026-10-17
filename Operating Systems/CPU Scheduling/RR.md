---
study_order: 18
tags:
  - GATE/CS
  - GATE/OS
  - scheduling/RR
aliases:
  - Round Robin
date_created: 2026-05-18
difficulty: ⭐⭐⭐⭐
last_revised: 2026-05-18
pyq_frequency: Very High
---

## Syllabus Position
Subject: [[Operating Systems]]
Parent Topic: [[CPU Scheduling Algorithms MOC]]

GATE Syllabus Line: CPU Scheduling Algorithms.

## The Problem This Solves
In systems where multiple users are active (Time-sharing), we can't let one process hog the CPU. Everyone needs a "fair slice" of time regularly.

Analogy: A teacher answering questions in a class. Instead of finishing one student's 10 questions, the teacher answers 1 question from each student in a circle.

Core Idea: Each process gets a small unit of CPU time ([[Time Quantum]]), then is moved to the back of the queue.

## Formal Theory
**Round Robin (RR)** is strictly **preemptive**.

### Characteristics
- **Criteria**: [[Arrival Time]] + [[Time Quantum]].
- **Ready Queue**: Treated as a **Circular Queue**.
- **Performance**: Heavily dependent on the size of the [[Time Quantum]] ($q$):
    - If $q$ is very large $\rightarrow$ RR becomes [[FCFS]].
    - If $q$ is very small $\rightarrow$ RR becomes **Processor Sharing** (too many context switches).

## Worked Example
Processes: P1(BT=5), P2(BT=3), P3(BT=1). AT=0 for all. $q=2$.

**Queue Trace:**
1. Initial Queue: [P1, P2, P3]
2. $t=0..2$: P1 runs. Queue becomes [P2, P3, P1] (P1 moved to back).
3. $t=2..4$: P2 runs. Queue becomes [P3, P1, P2].
4. $t=4..5$: P3 runs. P3 finishes! Queue: [P1, P2].
5. $t=5..7$: P1 runs. P1 finishes! Queue: [P2].
6. $t=7..8$: P2 runs. P2 finishes!

**Gantt Chart:**
| P1(2) | P2(2) | P3(1) | P1(3) | P2(1) |

## Intuition Anchors
- **The Fairness King**: Best for [[Response Time]].
- **The #1 Trap**: When a process is preempted at the **same time** a new process arrives, the **new process** is usually added to the queue **before** the preempted one (standard GATE convention, but check question wording).

## GATE Questions
**Question 1 (GATE-style)**:
If [[Time Quantum]] is increased, what happens to [[Response Time]]?
- (A) Decreases
- (B) Increases
- (C) Stays same
- (D) Becomes zero

<details>
<summary>Solution</summary>
Answer: (B). Larger quantum means processes wait longer before getting their turn again.
</details>

## Quick Revision Sheet
- **Criteria**: Time Slice / Quantum.
- **Mode**: Preemptive.
- **Starvation**: No.
- **Good for**: Interactive systems, Time-sharing.
- **Rule of Thumb**: $q$ should be such that 80% of CPU bursts are shorter than $q$.
