---
study_order: 16
tags:
  - GATE/CS
  - GATE/Mathematics
  - Linear-Algebra
aliases:
  - Eigenvector calculation
  - Null space of (A-λI)
date_created: 2026-04-30
difficulty: ⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: Medium
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Eigenvalues and Eigenvectors Definition]], [[Characteristic Equation]]

## 💡 Motivation & Intuition
Once we have the [[Eigenvalue]] ($\lambda$), we know *how much* the vector is scaled. Now we need to find the *direction* ($x$) that stays invariant. This direction is the **Eigenvector**. 

Finding eigenvectors is equivalent to finding the **Null Space** (kernel) of the shifted matrix $(A - \lambda I)$.

## 📖 Theory
### 1. The System of Equations
For a specific eigenvalue $\lambda_i$, the eigenvector $x_i$ satisfies:
$$(A - \lambda_i I)x_i = 0$$
This is a **Homogeneous [[System of Linear Equations]]**. Since $\det(A - \lambda_i I) = 0$, we are guaranteed to have infinitely many solutions (at least one free variable).

### 2. Eigenspace
The set of all eigenvectors corresponding to a specific eigenvalue $\lambda$, together with the zero vector, forms a subspace called the **Eigenspace** $E_\lambda$.
$$E_\lambda = \text{null}(A - \lambda I)$$

### 3. Geometric Multiplicity (GM)
The dimension of the eigenspace $E_\lambda$ (i.e., the number of linearly independent eigenvectors for $\lambda$) is called the **Geometric Multiplicity**.
- **Rule:** $1 \leq \text{GM} \leq \text{Algebraic Multiplicity}$.

## 🔢 Worked Example
**Matrix $A$:**
$$A = \begin{pmatrix} 4 & 1 \\ 2 & 3 \end{pmatrix}$$
From [[Characteristic Equation]], we found $\lambda_1 = 5, \lambda_2 = 2$.

**Finding Eigenvector for $\lambda = 5$:**
$$(A - 5I)x = 0$$
$$\begin{pmatrix} 4-5 & 1 \\ 2 & 3-5 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$
$$\begin{pmatrix} -1 & 1 \\ 2 & -2 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$
Row 1: $-x_1 + x_2 = 0 \implies x_1 = x_2$.
Row 2: $2x_1 - 2x_2 = 0$ (Redundant).
Let $x_2 = 1 \implies x_1 = 1$.
**Eigenvector for $\lambda=5$:** $v_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$.

## 🎯 GATE Questions
**Question (GATE-style):**
If a $3 \times 3$ matrix has eigenvalues 1, 2, and 2, what is the maximum possible number of linearly independent eigenvectors?
- (A) 1
- (B) 2
- (C) 3
- (D) 9

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (C)**

**Reasoning:**
Eigenvalues are 1, 2, 2.
- For $\lambda=1$, there is at least 1 eigenvector.
- For $\lambda=2$, the multiplicity is 2, so there can be up to 2 linearly independent eigenvectors.
Total max = $1 + 2 = 3$.

</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Linear Independence:** Eigenvectors corresponding to *distinct* eigenvalues are always **linearly independent**.
- [ ] **Defective Matrix:** If GM < AM for any eigenvalue, the matrix is "defective" and cannot be [[Diagonalization|Diagonalized]].
- [ ] **Zero Vector:** Don't forget that an eigenvector cannot be the zero vector. If you get only the zero vector, you made a mistake in calculating $\lambda$.

## ⚖️ Comparisons
| Concept | Definition | Significance |
| :--- | :--- | :--- |
| **Algebraic Multiplicity (AM)** | Number of times $\lambda$ appears as a root | Max possible GM |
| **Geometric Multiplicity (GM)** | Number of LI eigenvectors for $\lambda$ | Reality of the eigenspace |

## 🧠 Memory Hooks
- **"Eigenvector = Null space"**: Finding $x$ is just finding the null space of $(A - \lambda I)$.
- **"Free variable"**: You will always have at least one free variable when solving for an eigenvector.

## 🕸️ Connections Web
- [[Null Space]]
- [[System of Linear Equations]]
- [[Linear Independence]]
- [[Diagonalization]]

---
## ✅ Revision Checklist
- [ ] I can solve $(A - \lambda I)x = 0$ to find $x$.
- [ ] I understand the difference between AM and GM.
- [ ] I know that distinct eigenvalues lead to LI eigenvectors.
