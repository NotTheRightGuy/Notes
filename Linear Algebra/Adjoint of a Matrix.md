---
study_order: 8
tags:
  - GATE/CS
  - GATE/Engineering-Mathematics
  - Linear-Algebra
aliases:
  - Adjugate
  - Adjoint
date_created: 2026-04-30
difficulty: ⭐⭐⭐
last_revised: 2026-04-30
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Engineering Mathematics]]
**Parent Topic:** [[Linear Algebra]]
**Sibling Topics:** [[Cofactor]], [[Determinants]]
**Leads To:** [[Inverse of a Matrix]], [[Cramer's Rule]]

> 📍 **GATE Syllabus Mapping:** Matrices, determinants, and their properties.

## 💡 Motivation & Intuition
The **Adjoint** (also called Adjugate) is a bridge between a matrix and its inverse. It's essentially a matrix where every element is replaced by its "influence" on the determinant.

**Core Idea:** To get the Adjoint, you find all [[Cofactor|Cofactors]], arrange them in a matrix, and then **transpose** that matrix.

## 📖 Theory

### 1. Definition
For a square matrix $A$, the Adjoint is defined as:
$$\text{adj}(A) = (\text{Cofactor Matrix of } A)^T$$

### 2. The Golden Property
This is the most important formula for GATE:
$$A \cdot \text{adj}(A) = \text{adj}(A) \cdot A = |A| \cdot I$$
Where $|A|$ is the [[Determinants|Determinant]] and $I$ is the Identity matrix.

### 3. Properties of Adjoint
Let $A$ be an $n \times n$ matrix:
1.  **Inverse Relation:** $A^{-1} = \frac{\text{adj}(A)}{|A|}$
2.  **Product:** $\text{adj}(AB) = \text{adj}(B) \cdot \text{adj}(A)$ (Reverse order!)
3.  **Transpose:** $\text{adj}(A^T) = (\text{adj}(A))^T$
4.  **Scalar:** $\text{adj}(kA) = k^{n-1} \text{adj}(A)$ (Note the $n-1$ power!)
5.  **Determinant of Adjoint:** $|\text{adj}(A)| = |A|^{n-1}$
6.  **Double Adjoint:** $\text{adj}(\text{adj}(A)) = |A|^{n-2} \cdot A$
7.  **Determinant of Double Adjoint:** $|\text{adj}(\text{adj}(A))| = |A|^{(n-1)^2}$

### 4. $2 \times 2$ Shortcut
If $A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}$, then:
$$\text{adj}(A) = \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$$
*Strategy: Swap diagonal elements, change signs of off-diagonal elements.*

## 🖼️ Visual Workflow
```mermaid
graph LR
    A[Matrix A] --> B[Minors]
    B --> C[Cofactors]
    C --> D[Cofactor Matrix]
    D --> E[Transpose]
    E --> F[Adjoint]
```

## ⏱️ Complexity Analysis
- Since we calculate $n^2$ cofactors, each being a $(n-1) \times (n-1)$ determinant, the complexity is $O(n^4)$.
- For $n=3$, it's manageable. For larger $n$, we use properties.

## 🔢 Worked Example ($3 \times 3$)
Find $\text{adj}(A)$ for $A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$.
Using shortcut:
1. Swap diagonals: $\begin{bmatrix} 4 & \dots \\ \dots & 1 \end{bmatrix}$
2. Negate off-diagonals: $\begin{bmatrix} 4 & -2 \\ -3 & 1 \end{bmatrix}$
$\text{adj}(A) = \begin{bmatrix} 4 & -2 \\ -3 & 1 \end{bmatrix}$.

## 🎯 GATE Questions

**Question (GATE):** If $A$ is a $3 \times 3$ matrix and $|A| = 4$, then $|\text{adj}(A)|$ is:
- (A) 4
- (B) 16
- (C) 64
- (D) 12

<details>
<summary>💡 Solution</summary>
**Answer: (B)**
Property: $|\text{adj}(A)| = |A|^{n-1}$.
Here $n=3, |A|=4$.
$|\text{adj}(A)| = 4^{3-1} = 4^2 = 16$.
</details>

## ⚠️ Edge Cases & Traps
- [ ] **Forgot Transpose:** Most students calculate the cofactor matrix but forget to transpose it.
- [ ] **Scalar Property:** Remember $\text{adj}(kA) = k^{n-1}\text{adj}(A)$, not $k^n$.
- [ ] **Order of AB:** $\text{adj}(AB) = \text{adj}(B)\text{adj}(A)$. Order matters!

## ⚖️ Comparison
| Feature | Matrix $A$ | $\text{adj}(A)$ |
| :--- | :--- | :--- |
| **Determinant** | $|A|$ | $|A|^{n-1}$ |
| **Invertibility** | $|A| \neq 0$ | Always exists |

## 🧠 Memory Hooks
- **"Swap and Sign"**: The mnemonic for $2 \times 2$ adjoint.
- **"The Bridge"**: Adjoint bridges the gap between the Matrix and its Inverse.

## 🕸️ Connections Web
- [[Cofactor]] — The building blocks of Adjoint.
- [[Determinants]] — Used in Adjoint properties.
- [[Inverse of a Matrix]] — Defined as $\text{adj}(A) / |A|$.
- [[Cramer's Rule]] — Uses determinants of modified matrices, related to cofactors.

## ✅ Revision Checklist
- [ ] I can write down all 7 properties of the Adjoint.
- [ ] I can compute a $2 \times 2$ adjoint in 5 seconds.
- [ ] I know the difference between the determinant of $A$ and the determinant of $\text{adj}(A)$.
