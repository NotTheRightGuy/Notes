---
study_order: 14
tags:
  - GATE/CS
  - GATE/Mathematics
  - Linear-Algebra
aliases:
  - Eigenvalue
  - Eigenvector
  - Characteristic Value
  - Proper Vector
date_created: 2026-04-30
difficulty: ⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Characteristic Equation]], [[Eigenvectors and Eigenspaces]]
**Leads To:** [[Diagonalization]], [[Linear Transformation]]

> 📍 **GATE Syllabus Mapping:** "Linear Algebra: Matrices, determinants, system of linear equations, eigenvalues and eigenvectors."

## 💡 Motivation & Intuition
Most [[Linear Transformation]]s "move" or "rotate" vectors in space. However, for any given transformation represented by a matrix $A$, there are certain special directions (vectors $x$) that do **not change direction**. They only get scaled by a factor $\lambda$.

**Analogy:** Imagine stretching a rubber sheet. Most points move to new locations and directions. But points along the axis of stretch only move further away or closer to the center, staying on the same line. These "lucky" directions are the **Eigenvectors**, and the stretching factor is the **Eigenvalue**.

**Core Idea:** An eigenvector is a non-zero vector that changes only by a scalar factor when that linear transformation is applied to it.

## 📖 Theory
### Formal Definition
Let $A$ be an $n \times n$ square [[Matrix]]. A non-zero vector $x \in \mathbb{R}^n$ is called an **Eigenvector** of $A$ if there exists a scalar $\lambda$ (called the **Eigenvalue**) such that:

$$Ax = \lambda x$$

Where:
- $A$: The transformation matrix.
- $x$: The **Eigenvector** ($x \neq 0$).
- $\lambda$: The **Eigenvalue**.

### Key Constraints
1. **Square Matrix:** Eigenvalues are only defined for square matrices.
2. **Non-zero Vector:** By definition, $x = 0$ is NOT an eigenvector (it would make the equation trivially true for any $\lambda$).
3. **Scalar $\lambda$:** $\lambda$ can be zero, positive, negative, or even complex.

## ⏱️ Complexity Analysis
Finding all eigenvalues for an $n \times n$ matrix typically involves solving an $n$-th degree polynomial.
- **For $2 \times 2$:** $O(1)$ (quadratic formula).
- **For $n \times n$:** Generally $O(n^3)$ using numerical methods like the QR algorithm.

## 🎯 GATE Questions
**Question 1 (GATE-style):**
If $x$ is an eigenvector of $A$, then which of the following is true?
- (A) $Ax$ is parallel to $x$.
- (B) $Ax$ is perpendicular to $x$.
- (C) $Ax$ is always equal to $x$.
- (D) $x$ must be a unit vector.

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (A)**

**Reasoning:** Since $Ax = \lambda x$, the vector $Ax$ is just a scalar multiple of $x$. In vector geometry, $v = k u$ means $v$ and $u$ are parallel (collinear).

</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Zero Eigenvalue:** $\lambda = 0$ is possible. It implies $Ax = 0x = 0$, meaning $A$ is [[Singular Matrix]] (non-invertible).
- [ ] **Zero Vector:** $x=0$ is NEVER an eigenvector.
- [ ] **Complex Eigenvalues:** Even if $A$ is real, eigenvalues can be complex (common in rotation matrices).

## ⚖️ Comparisons
| Feature | [[Eigenvalue]] | [[Eigenvector]] |
| :--- | :--- | :--- |
| **Nature** | Scalar ($\lambda$) | Vector ($x$) |
| **Role** | Scaling factor | Directional invariant |
| **Existence** | $\det(A - \lambda I) = 0$ | $(A - \lambda I)x = 0$ |

## 🧠 Memory Hooks
- **"Eigen"** means "own" or "characteristic" in German. It's the matrix's "own" natural frequency/direction.
- **Formula Recall:** $Ax = \lambda x$. Remember: "Matrix times Vector = Scaling of Vector".

## 🕸️ Connections Web
- [[Determinant]] — used to find eigenvalues.
- [[Null Space]] — eigenvectors for $\lambda$ live in the null space of $(A - \lambda I)$.
- [[Linear Transformation]] — eigenvalues describe how the transformation scales space.

---
## ✅ Revision Checklist
- [ ] I can write the fundamental equation $Ax = \lambda x$.
- [ ] I understand why $x$ cannot be the zero vector.
- [ ] I can explain the geometric meaning of an eigenvalue.
