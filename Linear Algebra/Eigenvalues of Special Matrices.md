---
study_order: 18
tags:
  - GATE/CS
  - GATE/Mathematics
  - Linear-Algebra
aliases:
  - Eigenvalues of triangular matrices
  - Eigenvalues of symmetric matrices
date_created: 2026-04-30
difficulty: ⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Properties of Eigenvalues]], [[Diagonalization]]

## 💡 Motivation & Intuition
In many GATE problems, the matrix provided has a special structure. Recognizing these structures allows you to "see" the eigenvalues instantly without solving any polynomials. This saves crucial time.

## 📖 Theory

### 1. Diagonal & Triangular Matrices
For **Diagonal**, **Upper Triangular**, and **Lower Triangular** matrices, the eigenvalues are simply the **entries on the main diagonal**.

**Example:**
$$A = \begin{pmatrix} 5 & 2 & 9 \\ 0 & 1 & 4 \\ 0 & 0 & -3 \end{pmatrix} \implies \lambda = 5, 1, -3$$

### 2. Symmetric Matrices
A matrix where $A = A^T$.
- Eigenvalues are **always real**.
- Eigenvectors corresponding to distinct eigenvalues are **orthogonal** (perpendicular).
- Always [[Diagonalization|Diagonalizable]].

### 3. Skew-Symmetric Matrices
A matrix where $A = -A^T$.
- Eigenvalues are either **zero** or **purely imaginary**.

### 4. Orthogonal Matrices
A matrix where $A^T A = I$.
- Eigenvalues have an absolute value (modulus) of **1**. ($|\lambda| = 1$).

### 5. Idempotent Matrices
A matrix where $A^2 = A$.
- Eigenvalues are only **0 or 1**.

### 6. Nilpotent Matrices
A matrix where $A^k = O$ for some $k$.
- All eigenvalues are **0**.

## 🔢 Summary Table

| Matrix Type | Condition | Eigenvalues ($\lambda$) |
| :--- | :--- | :--- |
| **Identity** | $A = I$ | All $\lambda = 1$ |
| **Triangular** | $a_{ij}=0$ for $i>j$ or $i<j$ | Main diagonal elements |
| **Symmetric** | $A = A^T$ | Always Real |
| **Skew-Symmetric**| $A = -A^T$ | $0$ or Purely Imaginary |
| **Orthogonal** | $A^T A = I$ | $|\lambda| = 1$ |
| **Idempotent** | $A^2 = A$ | $0, 1$ |
| **Nilpotent** | $A^k = O$ | $0$ |

## 🎯 GATE Questions
**Question (GATE-style):**
If $A$ is a real $3 \times 3$ skew-symmetric matrix, then which of the following is definitely an eigenvalue of $A$?
- (A) 1
- (B) -1
- (C) 0
- (D) $i$

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (C)**

**Reasoning:**
For a $3 \times 3$ skew-symmetric matrix, the characteristic polynomial is of degree 3. Complex eigenvalues must occur in conjugate pairs. Since there's an odd number of eigenvalues, at least one must be real. For skew-symmetric matrices, real eigenvalues must be 0.
Also, the determinant of an odd-order skew-symmetric matrix is always 0, so at least one $\lambda = 0$.

</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Real vs Complex:** A symmetric matrix with **complex** entries might not have real eigenvalues. The property $A=A^T$ only guarantees real eigenvalues for **real** matrices.
- [ ] **Skew-Symmetric Order:** Even-order skew-symmetric matrices can have a non-zero determinant (and thus no zero eigenvalues).

## 🧠 Memory Hooks
- **"Triangular is transparent"**: You can see the eigenvalues right on the diagonal.
- **"Symmetric is Solid/Real"**: Real symmetric $\implies$ Real eigenvalues.
- **"Orthogonal is One"**: Magnitude of eigenvalue is 1.

## 🕸️ Connections Web
- [[Matrix]]
- [[Symmetric Matrix]]
- [[Orthogonal Matrix]]
- [[Diagonalization]]

---
## ✅ Revision Checklist
- [ ] I can identify eigenvalues of a triangular matrix in 2 seconds.
- [ ] I know the eigenvalue properties of symmetric and skew-symmetric matrices.
- [ ] I understand the magnitude constraint for orthogonal matrices.
