---
study_order: 15
tags:
  - GATE/CS
  - GATE/Mathematics
  - Linear-Algebra
aliases:
  - Eigenvalue calculation
  - det(A-λI)=0
date_created: 2026-04-30
difficulty: ⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Eigenvalues and Eigenvectors MOC]]
**Sibling Topics:** [[Eigenvalues and Eigenvectors Definition]], [[Properties of Eigenvalues]]

## 💡 Motivation & Intuition
To find the [[Eigenvalue]] $\lambda$, we need to solve the equation $Ax = \lambda x$. 
Rearranging gives: $(A - \lambda I)x = 0$.
For a non-zero eigenvector $x$ to exist, the matrix $(A - \lambda I)$ must be **singular** (non-invertible). 
A matrix is singular if and only if its [[Determinant]] is zero. 
This leads us to the **Characteristic Equation**.

## 📖 Theory
### 1. The Characteristic Equation
For an $n \times n$ matrix $A$, the characteristic equation is:
$$\det(A - \lambda I) = 0$$
where $I$ is the $n \times n$ [[Identity Matrix]].

### 2. The Characteristic Polynomial
Expanding the determinant results in a polynomial in $\lambda$ of degree $n$:
$$P(\lambda) = (-1)^n \lambda^n + c_{n-1} \lambda^{n-1} + \dots + c_0$$
The roots of this polynomial are the **Eigenvalues**.

### 3. Step-by-Step Algorithm
1. Subtract $\lambda$ from the main diagonal elements of $A$ to get $(A - \lambda I)$.
2. Calculate the determinant of $(A - \lambda I)$.
3. Set the resulting expression to $0$.
4. Solve for $\lambda$.

## 🔢 Worked Example
**Matrix $A$:**
$$A = \begin{pmatrix} 4 & 1 \\ 2 & 3 \end{pmatrix}$$

**Step 1: Form $(A - \lambda I)$**
$$(A - \lambda I) = \begin{pmatrix} 4-\lambda & 1 \\ 2 & 3-\lambda \end{pmatrix}$$

**Step 2: Calculate Determinant**
$$\det(A - \lambda I) = (4-\lambda)(3-\lambda) - (1 \times 2)$$
$$= 12 - 4\lambda - 3\lambda + \lambda^2 - 2$$
$$= \lambda^2 - 7\lambda + 10$$

**Step 3: Solve $\lambda^2 - 7\lambda + 10 = 0$**
$$(\lambda - 5)(\lambda - 2) = 0$$
**Eigenvalues:** $\lambda_1 = 5, \lambda_2 = 2$.

**Verification:**
- Trace = $4+3 = 7$. $\lambda_1 + \lambda_2 = 5+2 = 7$. (Matches!)
- Det = $(4 \times 3) - 2 = 10$. $\lambda_1 \times \lambda_2 = 10$. (Matches!)

## 🎯 GATE Questions
**Question (GATE-style):**
What is the characteristic equation of $A = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}$?
- (A) $\lambda^2 - 2\lambda = 0$
- (B) $\lambda^2 - 2\lambda + 1 = 0$
- (C) $\lambda^2 - 1 = 0$
- (D) $\lambda^2 = 0$

<details>
<summary>💡 Solution (click to reveal)</summary>

**Answer: (A)**

**Step-by-step reasoning:**
Trace = $1+1 = 2$.
Det = $1-1 = 0$.
The polynomial is $\lambda^2 - (\text{Trace})\lambda + \text{Det} = 0$.
$\lambda^2 - 2\lambda + 0 = 0$.

</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Algebraic Multiplicity:** A root might be repeated (e.g., $(\lambda-2)^2=0$). This means $\lambda=2$ is an eigenvalue with multiplicity 2.
- [ ] **Complex Roots:** Roots can be complex if the matrix is not symmetric.
- [ ] **Sign errors:** Be extremely careful with signs during determinant expansion.

## 🧠 Memory Hooks
- **"Lambda on the diagonal"**: Only subtract $\lambda$ from the diagonal.
- **"Roots are the fruit"**: The eigenvalues are the roots of the polynomial tree.

## 🕸️ Connections Web
- [[Determinant]]
- [[Identity Matrix]]
- [[Eigenvalues and Eigenvectors Definition]]
- [[Cayley-Hamilton Theorem]] — Uses this same polynomial.

---
## ✅ Revision Checklist
- [ ] I can set up $\det(A - \lambda I) = 0$.
- [ ] I can derive the polynomial for a $2 \times 2$ matrix quickly.
- [ ] I can use Trace and Det to check my polynomial.
