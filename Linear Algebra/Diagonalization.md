---
study_order: 20
tags:
  - GATE/CS
  - GATE/Mathematics
  - Linear-Algebra
aliases:
  - Diagonalizable matrix
  - Similarity transformation
  - Modal Matrix
  - Matrix Diagonalization
date_created: 2026-05-10
difficulty: ⭐⭐⭐⭐
last_revised: 2026-05-10
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Eigenvectors and Eigenspaces]], [[Properties of Eigenvalues]], [[Cayley-Hamilton Theorem]]
**Leads To:** [[Applications of Eigenvalues]], Orthogonal Diagonalization, Quadratic Forms

> 📍 **GATE Syllabus Mapping:** "Linear Algebra: Matrix algebra, systems of linear equations, eigenvalues and eigenvectors." (Diagonalization is the primary application of these concepts).

---

## 💡 Motivation & Intuition
**The Problem:** Calculating $A^{100}$ for a dense matrix $A$ requires 99 matrix multiplications, which is computationally expensive and prone to error.
**The Insight:** Multiplying a **Diagonal Matrix** $D$ is trivial—you just raise the diagonal elements to that power.
**The Solution:** If we can "re-orient" our coordinate system such that the transformation $A$ acts only as scaling along specific axes (the [[Eigenvectors]]), $A$ becomes a diagonal matrix $D$ in that system. 

**Core Idea:** Diagonalization is the process of finding an invertible matrix $P$ such that $P^{-1}AP = D$. This decomposes $A$ into its fundamental scaling components.

---

## 📖 Theory

### 1. Formal Definition
A square matrix $A$ of order $n$ is said to be **Diagonalizable** if it is [[Similarity Transformation|Similar]] to a diagonal matrix $D$. That is, there exists an invertible matrix $P$ such that:
$$D = P^{-1}AP \quad \text{or} \quad A = PDP^{-1}$$

### 2. The Components: Modal and Diagonal Matrices
- **[[Modal Matrix]] ($P$):** A matrix whose columns are the **linearly independent eigenvectors** of $A$.
- **[[Diagonal Matrix]] ($D$):** A diagonal matrix whose entries are the corresponding **eigenvalues** of $A$.
- **Requirement:** For $P$ to be invertible, its columns must be [[Linear Dependency of Vectors|Linearly Independent]]. Thus, $A$ is diagonalizable **if and only if** it has $n$ linearly independent eigenvectors.

### 3. Algebraic Multiplicity (AM) vs Geometric Multiplicity (GM)
This is the most critical concept for GATE:
- **[[Algebraic Multiplicity]] (AM):** The number of times an eigenvalue $\lambda$ appears as a root of the [[Characteristic Equation]].
- **[[Geometric Multiplicity]] (GM):** The number of linearly independent eigenvectors associated with $\lambda$. It is calculated as the dimension of the null space of $(A - \lambda I)$:
  $$GM(\lambda) = n - \text{rank}(A - \lambda I)$$

### 4. Diagonalization Theorems
1. **The Fundamental Theorem:** An $n \times n$ matrix is diagonalizable iff it has $n$ linearly independent eigenvectors.
2. **The Multiplicity Condition:** $A$ is diagonalizable iff for **every** eigenvalue $\lambda_i$:
   $$AM(\lambda_i) = GM(\lambda_i)$$
3. **Sufficient Condition:** If $A$ has $n$ **distinct** eigenvalues, it is guaranteed to be diagonalizable (because distinct eigenvalues always produce linearly independent eigenvectors).
4. **Symmetric Matrices:** Every real [[Symmetric Matrix]] is always diagonalizable (specifically, orthogonally diagonalizable).

---

## 🖼️ Visual Representation
Imagine a transformation $A$ that rotates and stretches a circle into an ellipse.
1. **Standard Basis:** The transformation looks messy (off-diagonal elements).
2. **Eigenvector Basis ($P$):** We align our axes with the major and minor axes of the ellipse.
3. **Diagonal Transformation ($D$):** In this new system, the transformation is just a simple scaling along the new axes.

```text
Input Vector x  ───(A)───> Output Vector Ax
      │                         ^
     (P⁻¹)                     (P)
      v                         │
Vector in Eigen-basis ──(D)──> Scaled Vector
```

---

## ⏱️ Complexity & Matrix Powers
### Derivation of $A^k$
If $A = PDP^{-1}$, then:
$$A^2 = (PDP^{-1})(PDP^{-1}) = PD(P^{-1}P)DP^{-1} = PD^2P^{-1}$$
By induction:
$$A^k = PD^kP^{-1}$$
Where $D^k = \text{diag}(\lambda_1^k, \lambda_2^k, \dots, \lambda_n^k)$.

---

## 🔢 Step-by-Step Worked Example
**Task:** Diagonalize $A = \begin{pmatrix} 1 & 1 \\ 0 & 2 \end{pmatrix}$.

1. **Find Eigenvalues:**
   $\det(A - \lambda I) = (1-\lambda)(2-\lambda) - 0 = 0 \implies \lambda_1 = 1, \lambda_2 = 2$.
2. **Find Eigenvectors:**
   - For $\lambda_1 = 1$: $(A - I)x = 0 \implies \begin{pmatrix} 0 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = 0 \implies x_2 = 0$. Eigenvector $v_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$.
   - For $\lambda_2 = 2$: $(A - 2I)x = 0 \implies \begin{pmatrix} -1 & 1 \\ 0 & 0 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = 0 \implies x_1 = x_2$. Eigenvector $v_2 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$.
3. **Form $P$ and $D$:**
   $$P = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}, \quad D = \begin{pmatrix} 1 & 0 \\ 0 & 2 \end{pmatrix}$$
4. **Verify:** Calculate $P^{-1} = \begin{pmatrix} 1 & -1 \\ 0 & 1 \end{pmatrix}$ and check if $P^{-1}AP = D$.

---

## 🎯 GATE Questions

**Question 1 (GATE CS 2010):**
Which of the following is true for an $n \times n$ real matrix $A$?
- (A) If $A$ has $n$ distinct eigenvalues, it is diagonalizable.
- (B) If $A$ is diagonalizable, it must have $n$ distinct eigenvalues.
- (C) If $A$ is upper triangular, it is diagonalizable.
- (D) If $A$ is idempotent ($A^2 = A$), it is not diagonalizable.

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (A)**

**Reasoning:**
- **(A) is True:** Distinct eigenvalues guarantee $n$ LI eigenvectors, which is the sufficient condition for diagonalization.
- (B) is False: The Identity matrix is diagonal (thus diagonalizable) but has repeated eigenvalues (all 1s).
- (C) is False: $\begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$ is upper triangular but not diagonalizable (defective).
- (D) is False: Idempotent matrices are always diagonalizable (eigenvalues are only 0 or 1, and they are always non-defective).

**Trap to avoid:** Confusing "Sufficient" with "Necessary". Distinct eigenvalues are NOT necessary for diagonalization.
</details>

---

**Question 2 (Numerical):**
If $A = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$, what are the AM and GM of the eigenvalue $\lambda = 2$? Is it diagonalizable?

<details>
<summary>💡 Solution (click to reveal)</summary>

- **AM:** The characteristic eq is $(2-\lambda)^2 = 0$, so $\lambda=2$ appears twice. **AM = 2**.
- **GM:** $\text{rank}(A - 2I) = \text{rank}\begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix} = 0$.
  $GM = n - \text{rank} = 2 - 0 = \mathbf{2}$.
- **Conclusion:** Since $AM = GM = 2$, it **is diagonalizable**. In fact, it is already diagonal!
</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Defective Matrix:** If for any $\lambda$, $GM < AM$, the matrix is "short" on eigenvectors and **cannot** be diagonalized. 
- [ ] **Zero Eigenvalues:** A matrix can be diagonalizable even if it has $\lambda = 0$ (it just means the matrix is singular). Diagonalizability $\neq$ Invertibility.
- [ ] **The "1" on Super-diagonal Trap:** A matrix like $\begin{pmatrix} \lambda & 1 \\ 0 & \lambda \end{pmatrix}$ is the classic example of a non-diagonalizable (defective) matrix.
- [ ] **Order of Columns:** The order of eigenvectors in $P$ **must match** the order of eigenvalues in $D$.

---

## ⚖️ Comparisons

| Property | Diagonalizable Matrix | Non-Diagonalizable (Defective) |
| :--- | :--- | :--- |
| **Eigenvectors** | $n$ Linearly Independent | $< n$ Linearly Independent |
| **AM vs GM** | $AM = GM$ for all $\lambda$ | $GM < AM$ for at least one $\lambda$ |
| **Similarity** | $A \sim D$ (Diagonal) | $A \sim J$ ([[Jordan Canonical Form]]) |
| **Symmetric?** | All real symmetric are diag. | Never symmetric |

---

## 🧠 Memory Hooks
- **"The AM-GM equality"**: Just like in averages, for diagonalization, $AM$ must equal $GM$.
- **"Distinct is easy"**: If you see $n$ different eigenvalues, stop—it's diagonalizable.
- **"Modal Matrix $P$ is the Passport"**: It carries you from the world of $A$ to the simplified world of $D$.

---

## 🕸️ Connections Web
**Prerequisite Knowledge:**
- [[Eigenvalues and Eigenvectors Definition]] — basics
- [[Linear Independence]] — required for $P$ to exist
- [[Rank and Eigenvalue Relationships]] — calculating GM

**Builds Upon This Topic:**
- [[Applications of Eigenvalues]] — Computing $A^k$, solving differential equations
- [[Symmetric Matrix]] — Orthogonal diagonalization ($P^{-1} = P^T$)
- [[Jordan Canonical Form]] — What we do when we *can't* diagonalize

---

## ✅ Revision Checklist
- [ ] I can state the condition $AM = GM$ for diagonalization.
- [ ] I can construct the Modal Matrix $P$ from eigenvectors.
- [ ] I can use $A^k = PD^kP^{-1}$ to solve numerical problems.
- [ ] I can identify a defective matrix by checking the rank of $(A - \lambda I)$.
- [ ] I know that all symmetric matrices are diagonalizable.
