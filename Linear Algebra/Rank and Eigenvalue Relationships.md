---
study_order: 22
tags:
  - GATE/CS
  - GATE/LinearAlgebra
  - GATE/Eigenvalues
aliases:
  - Rank-Eigenvalue Relationship
  - Rank and Non-zero Eigenvalues
date_created: 2026-05-05
difficulty: ⭐⭐⭐⭐
last_revised: 2026-05-05
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Diagonalization]], [[Properties of Eigenvalues]], [[Rank and Solutions of Ax = b]]
**Leads To:** [[Singular Value Decomposition]], [[Quadratic Forms]]

> 📍 **GATE Syllabus Mapping:** Linear Algebra: Matrix algebra, systems of linear equations, eigenvalues and eigenvectors.

## 💡 Motivation & Intuition
In the world of Linear Algebra, **Rank** tells us about the "information density" or "dimensionality" of a matrix's output space. **Eigenvalues** tell us about the "scaling factors" along specific invariant directions. 

The relationship between them is the bridge between the **Geometry** (Rank/Nullity) and the **Arithmetic** (Characteristic Equation) of a matrix.

**Analogy:** If a matrix is a telescope, the **Rank** is the number of distinct directions you can actually point it, while the **Eigenvalues** are the zoom levels in those directions. If an eigenvalue is $0$, the telescope is broken in that direction (it collapses a dimension), directly reducing the **Rank**.

**Core Idea:** The number of non-zero eigenvalues (counting multiplicities) provides a lower bound for the rank, and for diagonalizable matrices, they are exactly equal.

---

## 📖 Theory

### 1. Key Definitions
- **Rank ($r$):** The number of linearly independent rows or columns in a matrix $A \in \mathbb{F}^{n \times n}$.
- **[[Nullity]] ($k$):** The dimension of the Null Space ($Ax=0$).
- **[[Eigenvalues]] ($\lambda_i$):** Scalars such that $Ax = \lambda x$ for non-zero $x$.
- **[[Algebraic Multiplicity]] (AM):** The number of times an eigenvalue appears as a root of the [[Characteristic Equation]].
- **[[Geometric Multiplicity]] (GM):** The dimension of the eigenspace associated with $\lambda$ (i.e., $nullity(A - \lambda I)$).

### 2. The Rank-Nullity Connection to $\lambda = 0$
An eigenvalue $\lambda = 0$ is the most direct link to Rank.
- If $\lambda = 0$ is an eigenvalue, then $Ax = 0x = 0$ has a non-trivial solution.
- This means the matrix is **Singular** ($|A| = 0$).
- **Theorem:** The **Geometric Multiplicity** of $\lambda = 0$ is exactly equal to the **Nullity** of the matrix.
  $$GM(0) = \text{dim}(\text{Null}(A)) = n - \text{rank}(A)$$

### 3. General Multiplicity Bounds
For any eigenvalue $\lambda$:
$$1 \le GM(\lambda) \le AM(\lambda)$$
This implies that for $\lambda = 0$:
$$n - \text{rank}(A) \le AM(0)$$
Rearranging gives the **Fundamental Bound**:
$$\text{rank}(A) \ge n - AM(0)$$
*In plain English: The rank is at least the number of non-zero eigenvalues (including their AM).*

### 4. Special Case: Diagonalizable Matrices
If $A$ is [[Diagonalization|Diagonalizable]], then $GM(\lambda) = AM(\lambda)$ for all $\lambda$.
In this case:
$$\text{rank}(A) = \text{Number of non-zero eigenvalues (counting AM)}$$

### 5. Determinant and Trace
- **[[Determinant]]**: $|A| = \prod_{i=1}^n \lambda_i$. If any $\lambda_i = 0$, $|A| = 0 \implies \text{rank}(A) < n$.
- **[[Trace]]**: $Tr(A) = \sum_{i=1}^n \lambda_i$. Trace does not directly determine rank but provides a constraint on eigenvalues.

---

## 🖼️ Diagrams & Visuals

### Geometric Interpretation of GM(0)
Imagine a 3D space being transformed by a matrix $A$ of rank 2.
1. The matrix collapses one dimension onto a plane.
2. Every vector along that collapsed dimension is sent to $\vec{0}$.
3. These vectors are the **Eigenvectors** corresponding to $\lambda = 0$.
4. The dimension of this "collapsed space" is the **Nullity**, which is the **Geometric Multiplicity** of 0.

**ASCII Representation:**
```
Input Space (R^3) ----[ Matrix A ]----> Output Space (R^2 Plane)
      |                                       ^
      V                                       |
Null Space (Line) ----------------------> Origin (0,0,0)
(GM of λ=0 is 1)                         (Rank is 2)
```

---

## ⏱️ Complexity Analysis
While not an algorithm, calculating these values has costs:
- **Finding Rank:** $O(n^3)$ via Gaussian Elimination.
- **Finding Eigenvalues:** Theoretically no closed-form for $n > 4$ (Abel-Ruffini), practically $O(n^3)$ via QR algorithm.
- **Relationship Verification:** Once eigenvalues and rank are known, verification is $O(1)$ or $O(n)$ to sum multiplicities.

---

## 🔢 Worked Examples

### Example 1: Non-Diagonalizable Matrix
Let $A = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}$
- **Eigenvalues:** $\lambda^2 = 0 \implies \lambda = 0, 0$. (AM of 0 is 2).
- **Rank:** Row 2 is all zeros, Row 1 is independent. $\text{rank}(A) = 1$.
- **Nullity:** $n - \text{rank} = 2 - 1 = 1$.
- **Check:** $GM(0) = \text{Nullity} = 1$. Note that $1 < AM(0)$, so $A$ is not diagonalizable.
- **Rank vs Non-zero $\lambda$:** Here, non-zero $\lambda$ count is 0, but rank is 1. (Rank $\ge$ Non-zero $\lambda$ count holds).

### Example 2: Symmetric Matrix
Let $A = \begin{bmatrix} 1 & 2 \\ 2 & 4 \end{bmatrix}$
- **Determinant:** $4 - 4 = 0$. One eigenvalue is 0.
- **Trace:** $1 + 4 = 5$. Sum of eigenvalues is 5.
- **Eigenvalues:** $\lambda_1 = 0, \lambda_2 = 5$.
- **Rank:** Rows are proportional ($R2 = 2R1$). $\text{rank}(A) = 1$.
- **Verify:** Since $A$ is symmetric, it's diagonalizable. $\text{rank} = \text{count of non-zero } \lambda = 1$.

---

## 🎯 GATE Questions

**Question 1 — GATE-style (Multiple Select):**
Which of the following statements are ALWAYS true for an $n \times n$ matrix $A$?
- (A) $\text{rank}(A) = \text{number of non-zero eigenvalues}$.
- (B) $\text{rank}(A) \ge \text{number of non-zero eigenvalues}$.
- (C) If $\lambda = 0$ is an eigenvalue with $AM=k$, then $\text{rank}(A) \le n - k$.
- (D) If $\text{rank}(A) = n$, then $0$ is not an eigenvalue.

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (B), (D)**

**Reasoning:**
- (A) False. Counter-example: Nilpotent matrix $\begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}$ has 0 non-zero eigenvalues but rank 1.
- (B) **True.** The rank is always greater than or equal to the count of non-zero eigenvalues (specifically, the sum of their AMs is not always the rank, but the rank is bounded). More accurately, $\text{rank}(A) \ge n - AM(0)$.
- (C) False. $\text{rank}(A) \ge n - AM(0)$. If $AM(0)=k$, then $\text{rank}(A) \ge n-k$.
- (D) **True.** $\text{rank}(A) = n \implies |A| \neq 0 \implies \prod \lambda_i \neq 0 \implies$ No $\lambda_i = 0$.

**Trap:** Confusing AM and GM. Rank is directly tied to GM of 0, not AM.

</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Nilpotent Matrices:** $A^k = 0$. All eigenvalues are 0, but rank can be up to $n-1$.
- [ ] **Idempotent Matrices:** $A^2 = A$. Eigenvalues are only 0 or 1. For these, **$\text{rank}(A) = \text{trace}(A) = \text{number of eigenvalues equal to 1}$**. (Highly targeted in GATE).
- [ ] **Algebraic Multiplicity of 0:** If $AM(0) = k$, it does **not** mean $\text{rank} = n-k$. It means $\text{rank} \ge n-k$.

---

## ⚖️ Comparisons

| Feature | Diagonalizable Matrix | General Matrix |
| :--- | :--- | :--- |
| **Rank** | Count of non-zero $\lambda$ | $\ge$ Count of non-zero $\lambda$ |
| **Nullity** | $AM(0)$ | $GM(0)$ |
| **Relation** | $AM(\lambda) = GM(\lambda)$ | $AM(\lambda) \ge GM(\lambda)$ |

---

## 🧠 Memory Hooks
- **"Zero is the Hero of Nullity":** The number of independent directions sent to zero (GM of 0) is exactly the Nullity.
- **"Rank is Reality, Eigenvalues are Expectations":** Rank tells you how many dimensions actually exist. Non-zero eigenvalues are the ones that survive the transformation without being crushed to zero.

---

## 🕸️ Connections Web
**Prerequisite Knowledge:**
- [[Determinants]] — product of eigenvalues.
- [[Rank and Solutions of Ax = b]] — basic definition of rank.
- [[Linear Dependency of Vectors]] — basis of GM.

**Builds Upon This Topic:**
- [[Singular Value Decomposition]] — non-zero singular values related to rank.
- [[Diagonalization]] — condition for $AM=GM$.

---

## ✅ Revision Checklist
- [ ] I can explain why $GM(0) = \text{Nullity}$.
- [ ] I know that $\text{rank}(A) = n \iff$ all $\lambda_i \neq 0$.
- [ ] I can identify why a nilpotent matrix breaks the $\text{rank} = \text{count}(\lambda \neq 0)$ rule.
- [ ] I remember that for idempotent matrices, $\text{rank} = \text{trace}$.
