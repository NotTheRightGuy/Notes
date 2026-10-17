---
study_order: 21
tags:
  - GATE/CS
  - GATE/OS
  - scheduling
aliases:
  - Indefinite Blocking
---

# Starvation

## Definition
A situation where a process is ready to run but is never allocated the CPU because other processes are continuously given higher priority.

## In CPU Scheduling
- **Occurs in**: [[SJF]], [[SRTF]], and Priority Scheduling.
- **Reason**: Low-priority or long-burst jobs are constantly bypassed by new high-priority or short-burst arrivals.

## Solution: Aging
**Aging** is a technique that gradually increases the priority of processes that wait in the system for a long time. 
- Example: [[HRRN]] uses a form of aging by including [[Waiting Time]] in its scheduling criteria.

## Quick Comparison
- [[FCFS]]: No Starvation.
- [[RR]]: No Starvation.
- [[SJF]]: Starvation possible.
