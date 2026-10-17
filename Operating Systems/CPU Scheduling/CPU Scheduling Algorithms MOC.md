---
study_order: 13
tags:
  - GATE/CS
  - GATE/OS
  - scheduling
topic: CPU Scheduling
difficulty: ⭐⭐
---

# CPU Scheduling Algorithms MOC

## 🗺️ Core Concept Map
The goal of [[CPU Scheduling]] is to allocate the CPU to processes in the **Ready Queue** to maximize [[CPU Utilization]] and [[Throughput]] while minimizing [[Waiting Time]], [[Turnaround Time]], and [[Response Time]].

### 📈 Metrics & Fundamental Concepts
- [[Scheduling Metrics]] (AT, BT, CT, TAT, WT, RT)
- [[Starvation]] — Indefinite blocking of low-priority processes.
- [[Convoy Effect]] — Small processes waiting for a long one.
- [[Time Quantum]] — Used specifically in [[Round Robin]].
- [[Response Ratio]] — Used in [[HRRN]].

### ⚙️ Scheduling Algorithms
1. [[FCFS]] (First Come First Serve) - The simplest, non-preemptive.
2. [[SJF]] (Shortest Job First) - Optimal for avg waiting time, non-preemptive.
3. [[SRTF]] (Shortest Remaining Time First) - Preemptive SJF.
4. [[RR]] (Round Robin) - Time-sharing, preemptive.
5. [[HRRN]] (Highest Response Ratio Next) - Prevents starvation, non-preemptive.

### ⚖️ Evaluation & Comparison
- [[CPU Scheduling Comparison Table]]

## 🕸️ Connections
- [[Process Management]]
- [[Context Switching]]
- [[Dispatcher]]
- [[Ready Queue]]
