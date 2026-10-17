---
study_order: 19
tags:
  - GATE/CS
  - GATE/Mathematics
  - Linear-Algebra
aliases:
  - Cayley Hamilton
date_created: 2026-04-30
difficulty: ⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Characteristic Equation]], [[Properties of Eigenvalues]]

## 💡 Motivation & Intuition
The Cayley-Hamilton Theorem is a powerful bridge between [[Matrix]] algebra and polynomial algebra. It states that every matrix "behaves like its eigenvalues". If you know the polynomial that its eigenvalues satisfy, the matrix itself satisfies that same polynomial.

**Why use it?**
1. To calculate **large powers** of a matrix ($A^{100}$).
2. To find the **Inverse** ($A^{-1}$) without using the adjugate method.

## 📖 Theory
### Theorem Statement
Every square matrix $A$ satisfies its own **[[Characteristic Equation]]**.

If the characteristic polynomial of $A$ is:
$$P(\lambda) = \det(A - \lambda I) = \lambda^n + c_{n-1}\lambda^{n-1} + \dots + c_1\lambda + c_0 = 0$$
Then:
$$A^n + c_{n-1}A^{n-1} + \dots + c_1A + c_0I = O$$
Where $I$ is the [[Identity Matrix]] and $O$ is the [[Zero Matrix]].

## 🔢 Worked Example: Finding $A^{-1}$
**Matrix $A$:**
$$A = \begin{pmatrix} 2 & 1 \\ 3 & 4 \end{pmatrix}$$
**Characteristic Eq:** $\lambda^2 - 6\lambda + 5 = 0$.

**Apply Cayley-Hamilton:**
$$A^2 - 6A + 5I = O$$

**To find $A^{-1}$:**
Multiply the equation by $A^{-1}$:
$$A - 6I + 5A^{-1} = O$$
$$5A^{-1} = 6I - A$$
$$A^{-1} = \frac{1}{5}(6I - A)$$

## 🎯 GATE Questions
**Question (GATE CS 2008):**
The characteristic equation of a matrix $A$ is $\lambda^2 - \lambda - 1 = 0$. Then $A^{-1}$ is:
- (A) $A + I$
- (B) $A - I$
- (C) $I - A$
- (D) $-A - I$

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (B)**

**Step-by-step reasoning:**
1. By Cayley-Hamilton: $A^2 - A - I = O$.
2. Multiply by $A^{-1}$:
   $A^{-1}(A^2) - A^{-1}(A) - A^{-1}(I) = O$
   $A - I - A^{-1} = O$
3. Rearrange: $A^{-1} = A - I$.

</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Identity Matrix:** Don't forget to multiply the constant term $c_0$ by $I$ when converting from a polynomial in $\lambda$ to a matrix equation.
- [ ] **Singular Matrix:** If $c_0 = 0$, the matrix is not invertible, and you cannot find $A^{-1}$ this way (as expected).

## ⚖️ Comparisons
| Method | Use Case | Complexity |
| :--- | :--- | :--- |
| **Cayley-Hamilton** | $A^{-1}$ and $A^n$ | Fast for small $n$ |
| **Adjugate Method** | $A^{-1}$ only | High ($O(n!)$ or $O(n^3)$) |
| **[[Diagonalization]]** | $A^n$ for very large $n$ | High setup, very fast execution |

## 🧠 Memory Hooks
- **"Matrix eats its own roots"**: The matrix $A$ fits into the equation designed for its roots ($\lambda$).
- **"Inverse trick"**: Move $I$ to one side, multiply by $A^{-1}$.

## 🕸️ Connections Web
- [[Characteristic Equation]]
- [[Invertible Matrix]]
- [[Identity Matrix]]
- [[Minimal Polynomial]] — (Related advanced concept).

---
## ✅ Revision Checklist
- [ ] I can state the theorem correctly.
- [ ] I can use it to derive an expression for $A^3$ in terms of $A^2, A, I$.
- [ ] I can find $A^{-1}$ using the theorem.
