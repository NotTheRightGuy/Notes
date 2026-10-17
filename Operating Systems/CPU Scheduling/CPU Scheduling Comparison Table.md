---
study_order: 23
tags:
  - GATE/CS
  - GATE/OS
  - scheduling
topic: CPU Scheduling
difficulty: ⭐⭐
---

# CPU Scheduling Comparison Table

| Algorithm | Mode | Criteria | [[Starvation]]? | [[Convoy Effect]]? | Best Use Case |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **[[FCFS]]** | Non-Preemptive | [[Arrival Time]] | No | **Yes** (Major) | Simple Batch Systems |
| **[[SJF]]** | Non-Preemptive | [[Burst Time]] | Yes | No | Optimal for Avg Wait Time |
| **[[SRTF]]** | Preemptive | Rem. [[Burst Time]] | Yes | No | Dynamic optimal avg wait |
| **[[RR]]** | Preemptive | [[Time Quantum]] | **No** | No | Interactive / Time-sharing |
| **[[HRRN]]** | Non-Preemptive | [[Response Ratio]] | **No** | No | Balanced efficiency/fairness |

## Summary of Key Properties for GATE

- **Optimal Avg Wait Time**: [[SRTF]] (preemptive) > [[SJF]] (non-preemptive).
- **No Starvation**: [[FCFS]], [[RR]], [[HRRN]].
- **Interactive Performance**: [[RR]] is king.
- **Fairness**: [[RR]] and [[FCFS]].
- **Overhead**: [[SRTF]] and [[RR]] have high overhead due to frequent preemption and context switching.

## Common GATE Pattern
1. "Which algorithm is optimal?" $\rightarrow$ [[SRTF]]/[[SJF]].
2. "Which algorithm avoids starvation?" $\rightarrow$ [[RR]]/[[HRRN]]/[[FCFS]].
3. "Effect of increasing time quantum?" $\rightarrow$ [[RR]] becomes [[FCFS]].
