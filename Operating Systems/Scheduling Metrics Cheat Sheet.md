---
study_order: 11
tags:
  - GATE/CS
  - GATE/OperatingSystems
  - CPUScheduling
aliases:
  - Scheduling Cheat Sheet
  - CPU Scheduling Summary
date_created: 2026-05-13
difficulty: ⭐
last_revised: 2026-05-13
pyq_frequency: High
---

# CPU Scheduling Metrics Cheat Sheet

This is a high-density summary for quick revision of all metrics used in [[CPU Scheduling]].

## 🚀 The Formula Core

| Metric | Formula | Description |
| :--- | :--- | :--- |
| **Turnaround Time (TAT)** | $CT - AT$ | Total life of process in system. |
| **Waiting Time (WT)** | $TAT - BT$ | Total time process spent in Ready Queue. |
| **Response Time (RT)** | $\text{First CPU} - AT$ | Time to first response. |
| **Throughput** | $N / \text{Makespan}$ | Processes finished per unit time. |
| **CPU Utilization** | $\frac{\sum BT}{\text{Makespan}} \times 100$ | % time CPU was busy. |

## ⚡ Key Relationships

1. **Non-Preemptive Rule**: $WT = RT$
2. **Preemptive Rule**: $WT \geq RT$
3. **Optimality**: [[SJF]] (Shortest Job First) is optimal for minimizing **Average Waiting Time**.
4. **Fairness**: [[Round Robin]] is designed to minimize **Response Time** for interactive users.

## ⚠️ The "Gantt Chart" Checklist

When drawing a [[Gantt Chart]]:
1. **Check $t=0$**: Does any process actually arrive at 0? If not, the CPU is idle.
2. **Handle Ties**: If two processes have the same priority/burst, usually use **FCFS** (lower PID) as a tie-breaker.
3. **Preemption Points**: In algorithms like [[SRTF]], check for preemption **every time a new process arrives**.
4. **Completion Time**: CT is the *right-hand* edge of the process's last block in the Gantt chart.

## 📉 Comparison Table for Algorithms

| Algorithm | Preemptive? | Optimal for? | Main Weakness |
| :--- | :--- | :--- | :--- |
| [[FCFS]] | No | Simplicity | [[Convoy Effect]] |
| [[SJF]] | No | Avg. Waiting Time | Starvation of long jobs |
| [[SRTF]] | Yes | Avg. Waiting Time | Starvation / High overhead |
| [[Round Robin]] | Yes | Response Time | High [[Context Switching]] |
| [[Priority]] | Both | Business logic | Starvation (Fix: [[Aging]]) |

## 🕸️ Quick Links
- [[CPU Scheduling Metrics]] (Deep Dive)
- [[Gantt Chart]]
- [[Preemptive vs Non-Preemptive]]
- [[Context Switching]]

## ✅ Quick Revision
- [ ] TAT = Finish - Arrival
- [ ] WT = TAT - Burst
- [ ] RT = First - Arrival
- [ ] Throughput = Count / TotalTime
