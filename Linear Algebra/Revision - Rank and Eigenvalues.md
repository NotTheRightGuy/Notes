---
study_order: 23
tags:
  - GATE/CS
  - GATE/LinearAlgebra
  - Revision
aliases:
  - Eigenvalue Cheat Sheet
date_created: 2026-05-05
---

# 🚀 One-Page Revision: Rank & Eigenvalues

## 📌 The "Big Three" Relationships
1. **The Singularity Link:**
   $\text{rank}(A) < n \iff |A| = 0 \iff \text{At least one } \lambda = 0$.
2. **The Nullity Identity:**
   $\text{Nullity}(A) = GM(0) = n - \text{rank}(A)$.
3. **The Multiplicity Bound:**
   $\text{rank}(A) \ge n - AM(0)$.
   *(Equality holds if and only if $A$ is diagonalizable at $\lambda = 0$)*.

## ⚡ Special Matrix Shortcuts
| Matrix Type | Eigenvalue Property | Rank Property |
| :--- | :--- | :--- |
| **[[Idempotent Matrix\|Idempotent]] ($A^2=A$)** | $\lambda \in \{0, 1\}$ | $\text{rank}(A) = \text{trace}(A) = \text{number of 1s}$ |
| **[[Nilpotent Matrix\|Nilpotent]] ($A^k=0$)** | All $\lambda = 0$ | $\text{rank}(A) < n$ (can be $>0$) |
| **[[Symmetric Matrix\|Symmetric]] ($A=A^T$)** | All $\lambda \in \mathbb{R}$, Always Diagonalizable | $\text{rank}(A) = \text{Number of non-zero } \lambda$ |
| **[[Invertible Matrix\|Invertible]]** | No $\lambda = 0$ | $\text{rank}(A) = n$ |

## 🚫 Common Misconceptions (The "GATE Traps")
- **Trap 1:** "Rank = Number of non-zero eigenvalues." 
  - **Correction:** Only true for diagonalizable matrices. For others, $\text{Rank} \ge \text{Count}(\lambda \neq 0)$.
- **Trap 2:** "If $|A|=0$, then rank is 0."
  - **Correction:** If $|A|=0$, rank is just **less than $n$**. It could be $n-1$.
- **Trap 3:** "Trace = Rank."
  - **Correction:** Only true for Idempotent matrices.

## 🔗 Quick Links
- [[Rank and Eigenvalue Relationships]] (Detailed Theory)
- [[Properties of Eigenvalues]]
- [[Diagonalization]]
- [[Eigenvalues of Special Matrices]]
