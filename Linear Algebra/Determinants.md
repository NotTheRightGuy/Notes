---
study_order: 6
tags:
  - GATE/CS
  - GATE/Engineering-Mathematics
  - Linear-Algebra
aliases:
  - Determinant
  - Determinants
date_created: 2026-04-30
difficulty: ⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Engineering Mathematics]]
**Parent Topic:** [[Linear Algebra]]
**Sibling Topics:** [[Cofactor]], [[Rank of a Matrix]], [[Systems of Linear Equations]]
**Leads To:** [[Eigenvalues and Eigenvectors]], [[Cramer's Rule]], [[Inverse of a Matrix]]

> 📍 **GATE Syllabus Mapping:** Matrices, determinants, systems of linear equations.

## 💡 Motivation & Intuition
The **Determinant** is a single scalar value that captures the "essence" of a square matrix. 

**Analogy:** If a matrix is a transformation that stretches or squishes space, the determinant is the **scaling factor**. 
- If $\det(A) = 2$, the transformation doubles the area/volume.
- If $\det(A) = 0$, the transformation collapses space into a lower dimension (a line or a point), meaning the matrix is **Singular** and cannot be reversed.

**Core Idea:** The determinant tells us if a system of equations has a unique solution and if a matrix is invertible.

## 📖 Theory

### 1. Definition by Size
- **$1 \times 1$ Matrix:** If $A = [a]$, then $\det(A) = a$.
- **$2 \times 2$ Matrix:** If $A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}$, then $\det(A) = ad - bc$.
- **$3 \times 3$ Matrix (Sarrus Rule):**
  $$\det(A) = a(ei - fh) - b(di - fg) + c(dh - eg)$$
- **$n \times n$ Matrix (Laplace Expansion):**
  The determinant is defined recursively using [[Cofactor]] expansion along any row $i$:
  $$\det(A) = \sum_{j=1}^{n} a_{ij} C_{ij}$$
  where $C_{ij}$ is the cofactor.

### 2. Crucial Properties
Let $A$ and $B$ be $n \times n$ matrices:
1.  **Multiplicative:** $\det(AB) = \det(A)\det(B)$
2.  **Transpose:** $\det(A^T) = \det(A)$
3.  **Scalar Multiplication:** $\det(kA) = k^n \det(A)$ (Very common GATE trap!)
4.  **Inverse:** $\det(A^{-1}) = \frac{1}{\det(A)}$, provided $\det(A) \neq 0$.
5.  **Row Operations:**
    - Swapping two rows: $\det(A)$ becomes $-\det(A)$.
    - Multiplying a row by $k$: $\det(A)$ becomes $k \det(A)$.
    - Adding a multiple of one row to another: $\det(A)$ remains **unchanged**.
6.  **Triangular Matrices:** For Upper/Lower triangular or Diagonal matrices, $\det(A) = \prod \text{diagonal elements}$.

### 3. Singular vs Non-Singular
- **Singular:** $\det(A) = 0$. The matrix has no [[Inverse of a Matrix]]. Rows are linearly dependent.
- **Non-Singular:** $\det(A) \neq 0$. The matrix is invertible.

## 🖼️ Diagrams & Visuals
### Geometric Interpretation (2D)
```text
      ^
      |    /-------/ (Area = det(A))
      |   /       /
   v2 |  /       /
      | /_______/ > v1
      |_________________
```
The determinant is the signed area of the parallelogram formed by the column vectors $v_1, v_2$.

## ⏱️ Complexity Analysis
- **Cofactor Expansion:** $O(n!)$ - Impractical for large $n$.
- **Gaussian Elimination:** $O(n^3)$ - By converting to a triangular matrix and multiplying diagonals.

## 🔢 Worked Example ($3 \times 3$)
Find $\det(A)$ for $A = \begin{bmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 5 & 6 & 0 \end{bmatrix}$.

Expanding along Row 2 (it has a zero):
$$\det(A) = -0 \cdot M_{21} + 1 \cdot \begin{vmatrix} 1 & 3 \\ 5 & 0 \end{vmatrix} - 4 \cdot \begin{vmatrix} 1 & 2 \\ 5 & 6 \end{vmatrix}$$
$$\det(A) = 1(0 - 15) - 4(6 - 10)$$
$$\det(A) = -15 - 4(-4) = -15 + 16 = 1$$

## 🎯 GATE Questions

**Question 1 (GATE-CS):**
If $A$ is a $3 \times 3$ matrix with $\det(A) = 5$, what is $\det(2A)$?
- (A) 10
- (B) 20
- (C) 40
- (D) 80

<details>
<summary>💡 Solution</summary>
**Answer: (C)**
Using the property $\det(kA) = k^n \det(A)$:
Here $k=2, n=3, \det(A)=5$.
$\det(2A) = 2^3 \cdot 5 = 8 \cdot 5 = 40$.
**Trap:** Forgetting to raise the constant to the power of $n$.
</details>

## ⚠️ Edge Cases & Traps
- [ ] **$\det(A+B) \neq \det(A) + \det(B)$**: Determinant is NOT additive.
- [ ] **Matrix Size:** Always check $n$ before applying $k^n$.
- [ ] **Row Swaps:** If you swap rows an odd number of times, the sign flips. If even, it stays the same.

## ⚖️ Comparisons
| Property | Determinant | [[Rank of a Matrix]] |
| :--- | :--- | :--- |
| **Output** | Scalar value | Integer (0 to $n$) |
| **Square only?** | Yes | No |
| **Zero value** | Means singular | Means dependent |

## 🧠 Memory Hooks
- **"The Cross Product Ancestor"**: Think of the $2 \times 2$ determinant as the "ad-bc" cross.
- **"Diagonal Product"**: Whenever you see a triangular matrix, stop calculating cofactors—just multiply the diagonal!

## 🕸️ Connections Web
- [[Cofactor]] — Fundamental unit of Laplace expansion.
- [[Adjoint of a Matrix]] — Uses cofactors to find the inverse.
- [[Inverse of a Matrix]] — Exists only if $\det(A) \neq 0$.
- [[Eigenvalues and Eigenvectors]] — Characteristic equation is $\det(A - \lambda I) = 0$.
- [[Cramer's Rule]] — Solving equations using determinants.

## ✅ Revision Checklist
- [ ] I can derive $\det(kA)$.
- [ ] I know the effect of all 3 elementary row operations.
- [ ] I can solve a $3 \times 3$ determinant in < 60 seconds.
