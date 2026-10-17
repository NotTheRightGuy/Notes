---
study_order: 9
tags:
  - GATE/CS
  - GATE/Engineering-Mathematics
  - Linear-Algebra
aliases:
  - Matrix Inverse
  - Invertible Matrix
date_created: 2026-04-30
difficulty: ⭐⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Engineering Mathematics]]
**Parent Topic:** [[Linear Algebra]]
**Sibling Topics:** [[Adjoint of a Matrix]], [[Determinants]]
**Leads To:** [[Gaussian Elimination]], [[Systems of Linear Equations]], [[Cayley-Hamilton Theorem]]

> 📍 **GATE Syllabus Mapping:** Inverse of a matrix, systems of linear equations.

## 💡 Motivation & Intuition
In scalar math, the inverse of $x$ is $1/x$ such that $x \cdot (1/x) = 1$. In Matrix Algebra, we don't have "division." Instead, we have the **Inverse Matrix** ($A^{-1}$).

**Core Idea:** If $A$ is a transformation, $A^{-1}$ is the "Undo" button. It returns space to its original state. 
$$A \cdot A^{-1} = A^{-1} \cdot A = I$$

## 📖 Theory

### 1. Condition for Existence
A square matrix $A$ has an inverse **if and only if** it is Non-Singular ($|A| \neq 0$).

### 2. The Adjoint Formula
$$A^{-1} = \frac{\text{adj}(A)}{|A|}$$
Where $\text{adj}(A)$ is the [[Adjoint of a Matrix]].

### 3. Key Properties
1.  **Reversal Law:** $(AB)^{-1} = B^{-1} A^{-1}$
2.  **Transpose:** $(A^T)^{-1} = (A^{-1})^T$
3.  **Determinant:** $|A^{-1}| = \frac{1}{|A|}$
4.  **Double Inverse:** $(A^{-1})^{-1} = A$
5.  **Orthogonal Matrix:** If $A^T = A^{-1}$, the matrix is [[Orthogonal Matrix]].
6.  **Diagonal Matrix:** If $D = \text{diag}(d_1, d_2, \dots)$, then $D^{-1} = \text{diag}(1/d_1, 1/d_2, \dots)$.

### 4. Alternative Methods
- **[[Gaussian Elimination]]:** Transform $[A | I]$ into $[I | A^{-1}]$ using row operations.
- **[[Cayley-Hamilton Theorem]]:** Use the characteristic equation to express $A^{-1}$ as a polynomial in $A$.

## ⏱️ Complexity Analysis
| Method | Complexity | Best For |
| :--- | :--- | :--- |
| **Adjoint Method** | $O(n^4)$ or $O(n!)$ | Small matrices ($2 \times 2, 3 \times 3$) |
| **Gaussian Elimination** | $O(n^3)$ | Large matrices |

## 🔢 Worked Example ($3 \times 3$)
Let $A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$. Find $A^{-1}$.

1.  **Find $|A|$:** $(1 \times 4) - (2 \times 3) = 4 - 6 = -2$.
2.  **Find $\text{adj}(A)$:** $\begin{bmatrix} 4 & -2 \\ -3 & 1 \end{bmatrix}$. (Using [[Adjoint of a Matrix]] shortcut)
3.  **Apply Formula:**
    $$A^{-1} = \frac{1}{-2} \begin{bmatrix} 4 & -2 \\ -3 & 1 \end{bmatrix} = \begin{bmatrix} -2 & 1 \\ 1.5 & -0.5 \end{bmatrix}$$

## 🎯 GATE Questions

**Question (GATE):** If $A$ and $B$ are non-singular matrices, then $(AB)^{-1}$ is:
- (A) $A^{-1} B^{-1}$
- (B) $B^{-1} A^{-1}$
- (C) $A B$
- (D) $B A$

<details>
<summary>💡 Solution</summary>
**Answer: (B)**
This is the Reversal Law. To undo the operation "Put on socks, then put on shoes," you must "Take off shoes, then take off socks."
</details>

## ⚠️ Edge Cases & Traps
- [ ] **Singular Matrix:** If $|A|=0$, the inverse does **not** exist. GATE loves asking for the inverse of a matrix where one row is a multiple of another.
- [ ] **$(A+B)^{-1} \neq A^{-1} + B^{-1}$**: Inverse is NOT additive.
- [ ] **Non-Square Matrices:** Only square matrices can have a standard inverse (though pseudo-inverses exist for rectangular ones, they are outside the standard GATE syllabus).

## ⚖️ Comparisons
| Feature | Adjoint Method | Gaussian Elimination |
| :--- | :--- | :--- |
| **Effort** | High for $n > 3$ | Systematic |
| **Result** | Exact fractions | Might involve decimals |
| **Used in** | Theoretical proofs | Computer Algos |

## 🧠 Memory Hooks
- **"Socks and Shoes"**: For the reversal law $(AB)^{-1} = B^{-1}A^{-1}$.
- **"The Determinant Divider"**: Don't forget to divide the adjoint by the determinant!

## 🕸️ Connections Web
- [[Determinants]] — Determines if inverse exists.
- [[Adjoint of a Matrix]] — The numerator in the inverse formula.
- [[Gaussian Elimination]] — Practical method for finding inverse.
- [[Orthogonal Matrix]] — Where $A^{-1} = A^T$.
- [[Cayley-Hamilton Theorem]] — Another way to find $A^{-1}$.

## ✅ Revision Checklist
- [ ] I can verify an inverse by checking $A \cdot A^{-1} = I$.
- [ ] I can find the inverse of a $2 \times 2$ matrix in under 15 seconds.
- [ ] I know how to use the Reversal Law for $(ABC)^{-1}$.
