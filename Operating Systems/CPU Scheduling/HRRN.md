---
study_order: 20
tags:
  - GATE/CS
  - GATE/OS
  - scheduling/HRRN
aliases:
  - Highest Response Ratio Next
date_created: 2026-05-18
difficulty: ⭐⭐⭐
last_revised: 2026-05-18
pyq_frequency: Low
---

## Syllabus Position
Subject: [[Operating Systems]]
Parent Topic: [[CPU Scheduling Algorithms MOC]]

GATE Syllabus Line: CPU Scheduling Algorithms.

## The Problem This Solves
[[SJF]] is great for efficiency but causes [[Starvation]] for long jobs. We need a way to prioritize short jobs but also give long jobs a "bonus" for waiting.

Core Idea: Favor short jobs, but increase priority as waiting time increases.

## Formal Theory
**HRRN** is **non-preemptive**.

### [[Response Ratio]] ($RR$) Formula
$$RR = \frac{W + B}{B} = 1 + \frac{W}{B}$$
Where:
- $W$ = [[Waiting Time]] so far.
- $B$ = [[Burst Time]] (Expected CPU burst).

### Characteristics
- **Criteria**: Highest Response Ratio.
- **Starvation**: **No**. As $W$ increases, $RR$ increases, eventually making it the highest.

## Intuition Anchors
- **SJF with an Aging bonus**: It naturally favors shorter $B$ (denominator) but prevents starvation via $W$ (numerator).
- **The #1 Trap**: Calculating $RR$ once. In HRRN, you must recalculate $RR$ for all ready processes **every time** the CPU becomes free.

## Worked Example
Processes: P1(AT=0, BT=3), P2(AT=2, BT=6), P3(AT=4, BT=4), P4(AT=6, BT=5)

1. $t=0$: Only P1. Run P1 till $t=3$.
2. $t=3$: P2 is in queue ($W=3-2=1$).
   $RR(P2) = (1+6)/6 = 1.16$.
   Run P2 till $t=9$.
3. $t=9$: P3 ($W=9-4=5$) and P4 ($W=9-6=3$) are in queue.
   $RR(P3) = (5+4)/4 = 2.25$
   $RR(P4) = (3+5)/5 = 1.6$
   Run P3 till $t=13$.
4. At $t=13$: Run P4.

## Quick Revision Sheet
- **Criteria**: $1 + (W/B)$
- **Mode**: Non-preemptive
- **Starvation**: No
- **Relationship**: $B$ is small $\rightarrow$ RR is large; $W$ is large $\rightarrow$ RR is large.
