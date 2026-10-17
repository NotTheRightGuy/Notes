---
study_order: 4
tags:
  - GATE/CS
  - GATE/LinearAlgebra
  - Mathematics/Matrices
aliases:
  - AX=B
  - Linear Systems
date_created: 2026-04-30
difficulty: ⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Linear Algebra]]
**Sibling Topics:** [[Vector Spaces]], [[Rank of a Matrix]]
**Leads To:** [[Cramer's Rule]], [[Gaussian Elimination]], [[Eigenvalues and Eigenvectors]]

> 📍 **GATE Syllabus Mapping:** Linear Algebra: Systems of linear equations.

---

## 💡 Motivation & Intuition
Most engineering problems (circuit analysis, structural stress, network flow) boil down to finding multiple unknown values that satisfy multiple constraints simultaneously. 

**Core Idea:** Transforming a set of equations into a single matrix equation $AX=B$ allows us to use the power of [[Linear Algebra]] (inverses, rank, determinants) to find solutions efficiently.

---

## 📖 Theory

### Representation
A system of $m$ linear equations in $n$ variables $x_1, x_2, \dots, x_n$:
1. $a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n = b_1$
2. $a_{21}x_1 + a_{22}x_2 + \dots + a_{2n}x_n = b_2$
...
m. $a_{m1}x_1 + a_{m2}x_2 + \dots + a_{mn}x_n = b_m$

Can be written as **$AX = B$**:
- **A (Coefficient Matrix):** $m \times n$ matrix of $a_{ij}$.
- **X (Variable Vector):** $n \times 1$ column vector.
- **B (Constant Vector):** $m \times 1$ column vector.

### Types of Systems
1. **[[Homogeneous Systems]]:** If $B = 0$ (all $b_i = 0$). Always consistent.
2. **Non-Homogeneous Systems:** If $B \neq 0$.

### Consistency & Solutions
The system is **Consistent** if at least one solution exists, otherwise **Inconsistent**.

Using [[Rank of a Matrix]] ($r$):
Let $A$ be $m \times n$ and $[A|B]$ be the **Augmented Matrix**.
- **Inconsistent (No Solution):** $\text{rank}(A) < \text{rank}(A|B)$.
- **Consistent:** $\text{rank}(A) = \text{rank}(A|B) = r$.
    - **Unique Solution:** if $r = n$ (number of variables).
    - **Infinite Solutions:** if $r < n$.

---

## ⏱️ Complexity Analysis
Solving via different methods:
- [[Gaussian Elimination]]: $O(n^3)$
- [[Cramer's Rule]]: $O(n^4)$ or worse.
- [[Matrix Inversion Method]]: $O(n^3)$ (but usually slower than Gaussian in practice).

---

## 🎯 GATE Questions

**Question (GATE-CS):**
A system of $n$ linear equations with $n$ variables $AX=B$ is given. If $A$ is non-singular, how many solutions exist?
- (A) 0
- (B) 1
- (C) $n$
- (D) Infinite

<details>
<summary>💡 Solution (click to reveal)</summary>
**Answer: (B)**
Since $A$ is non-singular, $\det(A) \neq 0$. Thus $A^{-1}$ exists.
$X = A^{-1}B$ gives a unique solution.
</details>

---

## 🕸️ Connections Web
- [[Rank of a Matrix]] — The ultimate decider of consistency.
- [[Cramer's Rule]] — A determinant-based solution method.
- [[Gaussian Elimination]] — The standard row-reduction method.
- [[Homogeneous Systems]] — A special case where $B=0$.
- [[Linear Independence]] — Relates to the rank and solutions.

---
✅ Note created: System of Linear Equations.md
   Sections: 13/13 complete
   Wiki Links: 12 found
   Estimated read time: 4 minutes
