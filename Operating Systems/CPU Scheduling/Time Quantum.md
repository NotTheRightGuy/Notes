---
study_order: 19
tags:
  - GATE/CS
  - GATE/OS
  - scheduling
aliases:
  - Time Slice
---

# Time Quantum

## Definition
The small unit of time (typically 10-100ms) for which a process is allowed to run in a preemptive scheduling system, specifically [[Round Robin]].

## Impact of Size ($q$)
- **If $q$ is too small**: 
    - Many context switches occur.
    - CPU spends more time switching than executing (low efficiency).
- **If $q$ is too large**:
    - [[Round Robin]] behaves like [[FCFS]].
    - [[Response Time]] increases (bad for interactive users).

## GATE Insight
The choice of Time Quantum is a trade-off between **Response Time** and **Context Switch Overhead**. A rule of thumb is that 80% of CPU bursts should be shorter than the time quantum.
