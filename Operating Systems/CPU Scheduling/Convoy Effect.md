---
study_order: 15
tags:
  - GATE/CS
  - GATE/OS
  - scheduling
---

# Convoy Effect

## Definition
A phenomenon associated with [[FCFS]] where several small processes (usually I/O-bound) are blocked behind one large, long-running process (CPU-bound).

## Why it happens
1. A large process takes the CPU and holds it for a long time.
2. Smaller processes arrive and wait in the Ready Queue.
3. While the CPU is busy, I/O devices are idle.
4. When the large process finally finishes, smaller processes quickly use the CPU and then wait for I/O.
5. Now the CPU is idle.

## Consequence
- Significant decrease in [[CPU Utilization]] and [[Throughput]].
- Poor device utilization.

## Solution
Use preemptive algorithms like [[Round Robin]] or shortest-job-first variants ([[SJF]], [[SRTF]]).
