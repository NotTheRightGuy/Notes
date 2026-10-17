---
study_order: 2
tags:
  - GATE/CS
  - GATE/LinearAlgebra
  - Algorithms
aliases:
  - Matrix Multiplication
  - Product of Matrices
date_created: 2026-05-10
difficulty: ⭐⭐⭐⭐
last_revised: 2026-05-10
pyq_frequency: High
---

## 🗺️ Context
**Subject:** [[Linear Algebra]]
**Parent Topic:** [[Linear Algebra Index]]
**Sibling Topics:** [[Matrix Addition and Scalar Multiplication]], [[Inverse of a Matrix]]
**Leads To:** [[Eigenvalues]], [[LU Decomposition]], [[Powers of a Matrix]]

> 📍 **GATE Syllabus Mapping:** LU decomposition, Algebra of matrices, Determinants.

---

## 💡 Motivation & Intuition
### Why "Rows $\times$ Columns"?
Most students find the "dot product" rule ($row \times column$) weird. Here is the intuition:

**Analogy: The Recipe and the Ingredients.**
Imagine Matrix $A$ is a list of recipes (Rows).
Matrix $B$ is a list of stock prices for different stores (Columns).
- **Row $i$ of $A$**: 2 eggs, 3 flour, 1 sugar.
- **Column $j$ of $B$**: Store $J$'s prices for [egg, flour, sugar].
The result $C_{ij}$ is the **cost** of making Recipe $i$ using Store $j$'s prices.

**Core Idea:** Matrix multiplication represents the **Composition of Functions**. If $f(x) = Bx$ and $g(y) = Ay$, then $g(f(x)) = A(Bx) = (AB)x$. The output of the first transformation becomes the input of the second.

---

## 📖 Theory

### 1. Formal Definition
If $A$ is an $m \times n$ matrix and $B$ is an $n \times p$ matrix, their product $C = AB$ is an $m \times p$ matrix where:
$$c_{ij} = \sum_{k=1}^{n} a_{ik}b_{kj}$$
**Condition:** Number of columns in $A$ must equal number of rows in $B$.

### 2. Four Ways to See $AB$ (Deep Intuition)
1. **The Dot Product View (Standard):** $c_{ij}$ is the dot product of ($i$-th row of $A$) and ($j$-th column of $B$).
2. **The Column Picture:** Each column of $AB$ is a **linear combination of columns of A**, using weights from the columns of $B$.
   - $AB_{col\_j} = b_{1j}\mathbf{a_1} + b_{2j}\mathbf{a_2} + \dots$
3. **The Row Picture:** Each row of $AB$ is a **linear combination of rows of B**, using weights from the rows of $A$.
4. **The Outer Product View:** $AB$ is the sum of $n$ matrices of rank 1 (rank-1 updates).
   - $AB = \text{col}_1(A)\text{row}_1(B) + \text{col}_2(A)\text{row}_2(B) + \dots$

### 3. Properties
- **Non-Commutative:** $AB \neq BA$ (In general). Rotation then Scaling is not the same as Scaling then Rotation!
- **Associative:** $(AB)C = A(BC)$. (Composition of 3 functions doesn't care how you group them).
- **Distributive:** $A(B+C) = AB + AC$.
- **Identity:** $AI = IA = A$.
- **Transpose of Product:** $(AB)^T = B^T A^T$ (**The Socks-Shoes Property**: You put on socks then shoes; to reverse, you take off shoes then socks).

---

## 🖼️ Visual Representation
### Dimension Collapse
$$(m \times \mathbf{n}) \times (\mathbf{n} \times p) \to (m \times p)$$
Imagine $n$ is an intermediate space (e.g., 3D). Matrix $B$ maps from $p$-dim to $n$-dim. Matrix $A$ maps from $n$-dim to $m$-dim. The product $AB$ is a "shortcut" that skips the middle-man.

```text
Input (p) ---> [ Matrix B ] ---> Middle (n) ---> [ Matrix A ] ---> Output (m)
          \______________________________________________________/
                             Product Matrix AB (m x p)
```

---

## ⏱️ Complexity Analysis
For two $n \times n$ matrices:
- **Time Complexity:** $O(n^3)$ (Standard algorithm).
- **Optimized:** $O(n^{2.81})$ ([[Strassen's Algorithm]]).
- **Space Complexity:** $O(n^2)$ to store result.

---

## 🔢 Worked Example
Find $AB$ for $A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}, B = \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}$

**Step-by-Step:**
1. $c_{11} = (1\cdot5) + (2\cdot7) = 5 + 14 = 19$
2. $c_{12} = (1\cdot6) + (2\cdot8) = 6 + 16 = 22$
3. $c_{21} = (3\cdot5) + (4\cdot7) = 15 + 28 = 43$
4. $c_{22} = (3\cdot6) + (4\cdot8) = 18 + 32 = 50$
$AB = \begin{bmatrix} 19 & 22 \\ 43 & 50 \end{bmatrix}$

---

## 🎯 GATE Questions

**Question 1 (GATE CS 2014):**
Let $A$ and $B$ be two $n \times n$ real matrices. Which of the following is NOT true?
- (A) $det(AB) = det(A)det(B)$
- (B) $tr(A+B) = tr(A) + tr(B)$
- (C) $det(A+B) = det(A) + det(B)$
- (D) $(AB)^T = B^T A^T$

<details>
<summary>💡 Solution</summary>
**Answer: (C)**

**Reasoning:**
- (A) Determinant is multiplicative. True.
- (B) Trace is linear. True.
- (C) **False**. $det(A+B)$ is generally not $det(A)+det(B)$. Counter-example: $A = I, B = I$. $det(A+B) = det(2I) = 2^n$, while $det(A)+det(B) = 1+1 = 2$.
- (D) Reverse order property of transpose. True.
</details>

---

## ⚠️ Edge Cases & Traps
- [ ] **Zero Product Property Fails:** If $AB = O$, it does **NOT** mean $A=O$ or $B=O$. 
  - Example: $\begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix} = \begin{bmatrix} 0 & 0 \\ 0 & 0 \end{bmatrix}$
- [ ] **Cancellation Law Fails:** If $AB = AC$, you **cannot** conclude $B=C$ unless $A$ is non-singular.
- [ ] **Powers of a Matrix:** $A^2 = AA$. Only defined for square matrices.

---

## ⚖️ Comparisons

| Operation | Property | Explanation |
| :--- | :--- | :--- |
| **$A+B$** | Commutative | Order doesn't matter. |
| **$AB$** | Non-Commutative | Composition of transformations is order-sensitive. |
| **$(AB)C$** | Associative | Grouping of transformations doesn't change the final map. |

---

## 🧠 Memory Hooks
- **Socks and Shoes:** $(AB)^T = B^T A^T$. Inverse/Transpose reverses the order.
- **Inner Dimensions Match:** $(3 \times \mathbf{4}) \times (\mathbf{4} \times 2)$. The "4s" touch and disappear.

---

## 🕸️ Connections Web
- [[Linear Transformation]] — Matrix multiplication is composition.
- [[Rank of a Matrix]] — $rank(AB) \leq \min(rank(A), rank(B))$.
- [[Determinant]] — Multiplicative property $det(AB) = det(A)det(B)$.
- [[Eigenvalues]] — $AB$ and $BA$ have the same non-zero eigenvalues.

---

## ✅ Revision Checklist
- [ ] Can I multiply a $2 \times 3$ by a $3 \times 2$ matrix?
- [ ] Do I understand the "Column Picture" (Ax as combination of cols of A)?
- [ ] Do I remember that $AB = O$ doesn't imply $A=O$ or $B=O$?
