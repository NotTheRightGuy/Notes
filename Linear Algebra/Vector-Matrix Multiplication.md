---
study_order: 3
tags:
  - GATE/CS
  - GATE/LinearAlgebra
aliases:
  - Vector-Matrix Multiplication
  - Ax=b
  - Linear Combination of Columns
date_created: 2026-05-10
difficulty: ⭐⭐⭐⭐⭐
last_revised: 2026-05-10
pyq_frequency: Very High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Matrix Multiplication]]
**Sibling Topics:** [[Linear Transformation]], [[System of Linear Equations]]
**Leads To:** [[Basis and Dimension]], [[Column Space]], [[Null Space]], [[Eigenvectors]]

> 📍 **GATE Syllabus Mapping:** Systems of linear equations, LU decomposition.

---

## 💡 Motivation & Intuition
If Matrix Multiplication is the "Big One", **$Ax = b$** is the **heartbeat** of Linear Algebra.

### The Three Lenses of $Ax = b$
1. **The Machine (Transformation View):** Matrix $A$ is a machine. You put vector $x$ in, it stretches/rotates it, and spits out vector $b$.
2. **The Recipe (Column View):** You have a pantry of ingredients (Columns of $A$). Vector $x$ tells you **how much** of each ingredient to mix to get the final dish $b$.
3. **The Perspective (Row View):** Each row of $A$ is a "sensor". $b_i$ is how much $x$ aligns with sensor $i$ (dot product).

**Core Idea:** Solving $Ax = b$ is asking: *"What input $x$ was fed into machine $A$ to get output $b$?"* or *"What recipe $x$ creates dish $b$ using ingredients $A$?"*

---

## 📖 Theory

### 1. The Column Picture (Crucial for GATE)
Given $A = [\mathbf{a_1} \dots \mathbf{a_n}]$ and $x = \begin{bmatrix} x_1 \\ \vdots \\ x_n \end{bmatrix}$:
$$Ax = x_1\mathbf{a_1} + x_2\mathbf{a_2} + \dots + x_n\mathbf{a_n}$$
**Conclusion:** $Ax$ is a **linear combination of the columns of $A$**.
- If $b$ is in the [[Column Space]] of $A$, the system $Ax=b$ is consistent (has a solution).

### 2. The Row Picture
Each element $b_i$ of the result is:
$$b_i = (\text{Row}_i \text{ of } A) \cdot x$$
- This represents $m$ separate equations (hyperplanes) in $n$-dimensional space.
- The solution $x$ is the **intersection** of these hyperplanes.

---

## 🖼️ Visual Representation
### Transformation Geometry
Imagine $A = \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}$ and $x = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$.
- **Column View:** $1 \cdot \begin{bmatrix} 0 \\ 1 \end{bmatrix} + 0 \cdot \begin{bmatrix} -1 \\ 0 \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$.
- **Geometric View:** $A$ is a $90^\circ$ rotation matrix. It took the $x$-axis vector and turned it into the $y$-axis vector.

```text
    y
    ^
    | (0,1)  <-- b
    |
    +-----> x (1,0)
```

---

## ⏱️ Complexity Analysis
- **Time Complexity:** $O(m \cdot n)$ for $A_{m \times n}$ and $x_{n \times 1}$.
- **Significance:** This is much faster than $O(n^3)$ matrix-matrix multiplication. In Deep Learning, most of the work is $Ax$ (Forward pass).

---

## 🔢 Worked Example
Let $A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$ and $x = \begin{bmatrix} 5 \\ 6 \end{bmatrix}$. Find $Ax$.

**Method 1: Dot Product (Rows)**
- $b_1 = (1, 2) \cdot (5, 6) = 5 + 12 = 17$
- $b_2 = (3, 4) \cdot (5, 6) = 15 + 24 = 39$

**Method 2: Column Combination (Intuitive)**
$Ax = 5 \begin{bmatrix} 1 \\ 3 \end{bmatrix} + 6 \begin{bmatrix} 2 \\ 4 \end{bmatrix} = \begin{bmatrix} 5 \\ 15 \end{bmatrix} + \begin{bmatrix} 12 \\ 24 \end{bmatrix} = \begin{bmatrix} 17 \\ 39 \end{bmatrix}$

---

## 🎯 GATE Questions

**Question 1:**
If $Ax = 0$ for some non-zero vector $x$, then which of the following is true for the square matrix $A$?
- (A) $A$ is invertible.
- (B) $det(A) = 0$.
- (C) $A$ must be the zero matrix.
- (D) The columns of $A$ are linearly independent.

<details>
<summary>💡 Solution</summary>
**Answer: (B)**

**Reasoning:**
- If $Ax=0$ for $x \neq 0$, then $x$ is in the [[Null Space]] of $A$.
- This means the columns of $A$ are **Linearly Dependent** (you can combine them with non-zero weights $x_i$ to get zero).
- If columns are dependent, the matrix is singular $\implies det(A) = 0$.
**Key Link:** This is the definition of an [[Eigenvector]] with $\lambda = 0$.
</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Dimension Check:** $A_{m \times n}$ can only multiply a vector $x$ of size $n \times 1$. The result is $m \times 1$.
- [ ] **Zero Vector:** $A\mathbf{0}$ is always $\mathbf{0}$. This means linear transformations always fix the origin.
- [ ] **Identity Matrix:** $Ix = x$. The "No-Op" transformation.

---

## ⚖️ Comparisons

| View | Process | Best for... |
| :--- | :--- | :--- |
| **Row View** | Intersection of planes | Solving systems manually. |
| **Column View** | Combination of vectors | Understanding [[Rank of a Matrix]] and [[Column Space]]. |
| **Transformation** | Function mapping | Understanding [[Eigenvalues]] and Graphics. |

---

## 🧠 Memory Hooks
- **Ax = b is a Recipe:** $A$ are the ingredients on the shelf, $x$ is the shopping list, $b$ is the cake.
- **The "Span" Link:** All possible $Ax$ vectors form the **Span** of the columns of $A$.

---

## 🕸️ Connections Web
- [[System of Linear Equations]] — $Ax=b$ is the compact form.
- [[Linear Transformation]] — $A$ is the matrix representation.
- [[Basis and Dimension]] — Columns of $A$ form a basis for the output space if $A$ is invertible.
- [[Null Space]] — The set of all $x$ such that $Ax=0$.

---

## ✅ Revision Checklist
- [ ] Do I immediately see $Ax$ as a linear combination of columns?
- [ ] Can I relate $Ax=0$ to the [[Rank of a Matrix]]?
- [ ] Do I understand why $Ax$ is the core operation in Neural Networks?
