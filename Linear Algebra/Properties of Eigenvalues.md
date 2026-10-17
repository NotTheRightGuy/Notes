---
study_order: 17
tags:
  - GATE/CS
  - GATE/Mathematics
  - Linear-Algebra
aliases:
  - Eigenvalue properties
date_created: 2026-04-30
difficulty: ⭐⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Characteristic Equation]], [[Eigenvalues and Eigenvectors Definition]]

## 💡 Motivation & Intuition
In the GATE exam, you often don't need to calculate eigenvalues explicitly. Instead, you can use these "shortcuts" or properties to verify answers or solve for unknowns. These properties link eigenvalues directly to the structure of the [[Matrix]].

## 📖 Theory

Let $A$ be an $n \times n$ matrix with eigenvalues $\lambda_1, \lambda_2, \dots, \lambda_n$.

### 1. The Trace Property
The sum of the eigenvalues is equal to the **Trace** of the matrix (sum of main diagonal elements).
$$\sum_{i=1}^{n} \lambda_i = \text{tr}(A) = \sum_{i=1}^{n} a_{ii}$$

### 2. The Determinant Property
The product of the eigenvalues is equal to the **Determinant** of the matrix.
$$\prod_{i=1}^{n} \lambda_i = \det(A)$$
- **Corollary:** If at least one eigenvalue is $0$, then $\det(A) = 0$ (matrix is [[Singular Matrix]]).

### 3. Eigenvalues of $A^k$
If $\lambda$ is an eigenvalue of $A$, then $\lambda^k$ is an eigenvalue of $A^k$.
- *Example:* Eigenvalues of $A^2$ are $\lambda_1^2, \lambda_2^2, \dots$.

### 4. Eigenvalues of $A^{-1}$
If $A$ is invertible and $\lambda$ is an eigenvalue of $A$, then $\frac{1}{\lambda}$ is an eigenvalue of $A^{-1}$.

### 5. Eigenvalues of $A^T$
The eigenvalues of $A$ and its transpose $A^T$ are the same. (Note: Eigenvectors might differ).

### 6. Shifting Property
If $\lambda$ is an eigenvalue of $A$, then $(\lambda + k)$ is an eigenvalue of $(A + kI)$.

## 🔢 Worked Example
**Matrix $A$:**
$$A = \begin{pmatrix} 1 & 2 \\ 0 & 4 \end{pmatrix}$$
- **Trace** = $1 + 4 = 5$.
- **Determinant** = $(1 \times 4) - (2 \times 0) = 4$.
- Let eigenvalues be $\lambda_1, \lambda_2$.
- $\lambda_1 + \lambda_2 = 5$
- $\lambda_1 \times \lambda_2 = 4$
- Solving these: $\lambda_1 = 1, \lambda_2 = 4$. (Note: For triangular matrices, eigenvalues are just the diagonal elements!)

## 🎯 GATE Questions
**Question 1 (GATE CS 2014):**
The determinant of a $2 \times 2$ matrix is 50 and its trace is 15. The eigenvalues are:
- (A) 5, 10
- (B) 2, 25
- (C) 5, 15
- (D) 10, 20

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (A)**

**Step-by-step reasoning:**
1. Sum of eigenvalues ($\lambda_1 + \lambda_2$) = Trace = 15.
2. Product of eigenvalues ($\lambda_1 \lambda_2$) = Det = 50.
3. Check options:
   - (A) $5 + 10 = 15$, $5 \times 10 = 50$. (Correct)
   - (B) $2 + 25 = 27 \neq 15$.
   - (C) $5 + 15 = 20 \neq 15$.
   - (D) $10 + 20 = 30 \neq 15$.

</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Algebraic Multiplicity:** If a matrix has repeated eigenvalues, they must all be counted in the sum and product.
- [ ] **Complex Conjugates:** For real matrices, complex eigenvalues always occur in conjugate pairs ($a+bi$ and $a-bi$).

## ⚖️ Comparisons
| Property | Formula | Use Case |
| :--- | :--- | :--- |
| **Sum** | $\sum \lambda = \text{tr}(A)$ | Quickly eliminate options in MCQs |
| **Product** | $\prod \lambda = \det(A)$ | Check for invertibility |
| **Inverse** | $1/\lambda$ | Finding eigenvalues of $A^{-1}$ |

## 🧠 Memory Hooks
- **"T-S"**: **T**race is **S**um.
- **"D-P"**: **D**eterminant is **P**roduct.
- **"Power power"**: $A^k \implies \lambda^k$.

## 🕸️ Connections Web
- [[Matrix Trace]]
- [[Determinant]]
- [[Invertible Matrix]]
- [[Diagonalization]] — relies on these properties.

---
## ✅ Revision Checklist
- [ ] I can state the Trace and Determinant properties.
- [ ] I can find the eigenvalues of $A^k$ given eigenvalues of $A$.
- [ ] I know how eigenvalues change when a constant is added to the diagonal ($A + kI$).
