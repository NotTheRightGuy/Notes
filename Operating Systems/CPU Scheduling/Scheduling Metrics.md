---
study_order: 22
tags:
  - GATE/CS
  - GATE/OS
  - scheduling
aliases:
  - Scheduling Parameters
  - Process Metrics
date_created: 2026-05-18
difficulty: ⭐
last_revised: 2026-05-18
pyq_frequency: High
---

## Syllabus Position

Subject: [[Operating Systems]]
Parent Topic: [[CPU Scheduling Algorithms MOC]]
Leads To: [[FCFS]], [[SJF]], [[SRTF]], [[RR]], [[HRRN]]

GATE Syllabus Line: CPU Scheduling, Process scheduling metrics.

## The Problem This Solves

To evaluate how "good" a [[CPU Scheduling]] algorithm is, we need quantitative metrics. Without these, we can't compare if [[FCFS]] is better than [[Round Robin]] for a specific workload.

Analogy: Like measuring a restaurant's efficiency—you track when the customer arrived, how long they waited for a table, how long it took to cook the food, and when they finally left.

## Formal Theory

In [[Operating Systems]], several time-based metrics are used to evaluate scheduler performance:

### 1. [[Arrival Time]] ($AT$)
The time at which a process enters the **Ready Queue**.

### 2. [[Burst Time]] ($BT$)
The time required by a process for execution on the CPU (also called CPU Time).

### 3. [[Completion Time]] ($CT$)
The time at which a process finishes its execution.

### 4. [[Turnaround Time]] ($TAT$)
The total time spent by the process in the system.
$$TAT = CT - AT$$
Also, $TAT = WT + BT$.

### 5. [[Waiting Time]] ($WT$)
The time a process spends waiting in the ready queue.
$$WT = TAT - BT$$

### 6. [[Response Time]] ($RT$)
The time from submission until the **first** response is produced (first time CPU is allocated).
$$RT = (\text{Time of first CPU allocation}) - AT$$
*Note: For non-preemptive algorithms, $RT = WT$.*

### 7. [[Throughput]]
Number of processes completed per unit time.

### 8. [[CPU Utilization]]
Percentage of time the CPU is busy.

## Quick Revision Sheet

- **$TAT = CT - AT$**
- **$WT = TAT - BT$**
- **$RT = \text{First CPU Time} - AT$**
- **Throughput** = Processes / Time
- **In non-preemptive**: $WT = RT$.

## Revision Checklist
- [ ] I can derive $WT$ from $CT$, $AT$, and $BT$.
- [ ] I understand why $RT$ differs from $WT$ in preemptive scheduling.
