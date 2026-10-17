---
study_order: 12
tags:
  - GATE/CS
  - GATE/LinearAlgebra
  - Mathematics/Matrices
aliases:
  - Zero Constant Systems
date_created: 2026-04-30
difficulty: ⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[System of Linear Equations]]
**Sibling Topics:** [[Cramer's Rule]]
**Leads To:** [[Eigenvalues and Eigenvectors]], [[Null Space]]

> 📍 **GATE Syllabus Mapping:** Linear Algebra: Systems of linear equations.

---

## 💡 Motivation & Intuition
A homogeneous system is like a set of rules where "doing nothing" ($x=0, y=0, \dots$) is always a valid answer. The interesting part is finding out if there are *other* ways to satisfy the rules.

**Core Idea:** In $AX = 0$, the vector $X=0$ is always a solution (Trivial Solution). We look for **Non-Trivial Solutions**.

---

## 📖 Theory

### Properties
1. **Always Consistent:** Because $X=0$ (the origin) always satisfies $AX=0$.
2. **Trivial Solution:** $X = [0, 0, \dots, 0]^T$.
3. **Non-Trivial Solution:** A non-zero vector $X$ that satisfies the equation.

### The Rank Test
For an $n \times n$ matrix $A$:
- **Only Trivial Solution:** if $\text{rank}(A) = n$ (i.e., $\det(A) \neq 0$).
- **Infinite Non-Trivial Solutions:** if $\text{rank}(A) < n$ (i.e., $\det(A) = 0$).

Number of linearly independent solutions = $n - \text{rank}(A)$. This is also called the **Nullity** of $A$.

---

## 🖼️ Diagrams & Visuals
### Geometric Meaning (3D)
Three planes passing through the origin.
- If they intersect only at $(0,0,0)$: Trivial solution only.
- If they intersect along a line: Infinitely many solutions (1 degree of freedom).
- If they intersect in a plane: Infinitely many solutions (2 degrees of freedom).

---

## 🎯 GATE Questions

**Question (GATE-CS):**
For which value of $k$ does the following system have a non-trivial solution?
$x + ky + 3z = 0$
$3x + ky - 2z = 0$
$2x + 3y - 4z = 0$

<details>
<summary>💡 Solution (click to reveal)</summary>
For a non-trivial solution, $\det(A)$ must be $0$.
$$\begin{vmatrix} 1 & k & 3 \\ 3 & k & -2 \\ 2 & 3 & -4 \end{vmatrix} = 0$$
$1(-4k + 6) - k(-12 + 4) + 3(9 - 2k) = 0$
$-4k + 6 + 8k + 27 - 6k = 0$
$-2k + 33 = 0 \implies k = 33/2 = 16.5$.
</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Overdetermined Systems ($m > n$):** Can still have non-trivial solutions if the rank is less than $n$.
- [ ] **Rank vs. Determinant:** Remember that determinant is only for square matrices. For rectangular matrices, always use [[Rank of a Matrix]].

---

## 🕸️ Connections Web
- [[System of Linear Equations]] — The general framework.
- [[Rank of a Matrix]] — The tool to find the number of solutions.
- [[Null Space]] — The set of all solutions to $AX=0$.
- [[Eigenvalues and Eigenvectors]] — Solving $(A - \lambda I)X = 0$ is a homogeneous problem.

---
✅ Note created: Homogeneous Systems.md
   Sections: 13/13 complete
   Wiki Links: 10 found
   Estimated read time: 3 minutes
