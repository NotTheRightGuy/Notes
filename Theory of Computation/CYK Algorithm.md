---
study_order: 15
tags:
  - GATE/CS
  - GATE/TOC
  - Parsing
aliases:
  - Cocke-Younger-Kasami
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: Medium
---

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Chomsky Normal Form]]
**Sibling Topics:** [[Context Free Grammars]]
**Leads To:** [[Earley Parser]], [[Parsing Algorithms]]

>  **GATE Syllabus Mapping:** Context-free languages and pushdown automata; Membership testing algorithms.

##  Motivation & Intuition
If I give you a CFG and a string $w$, how do you check if $w \in L(G)$? A simple derivation might take forever (infinite paths).
**The CYK Algorithm** uses **Dynamic Programming**. It builds the solution from small substrings upwards. It answers: *"Can this variable derive this specific part of the string?"*

##  Theory
### Prerequisites
The algorithm **requires** the grammar to be in **[[Chomsky Normal Form]]**.
1. $A \to BC$
2. $A \to a$

### The DP Table
For a string $w = w_1 w_2 \dots w_n$:
Let $T[i, j]$ be the set of variables that can derive the substring $w[i \dots i+j-1]$ (substring starting at $i$ with length $j$).

**Initialization (Length 1):**
$T[i, 1] = \{ A \mid A \to w_i \in G \}$

**Recursive Step (Length $j > 1$):**
To check if $A$ derives $w[i \dots i+j-1]$, we split the substring into two parts of lengths $k$ and $j-k$.
$T[i, j] = \{ A \mid A \to BC \text{ is a rule, } B \in T[i, k], C \in T[i+k, j-k] \text{ for some } 1 \le k < j \}$

**Acceptance Condition:**
The string $w$ is in $L(G)$ if $S \in T[1, n]$.

##  Visuals
### CYK Table (Bottom-Up)
```text
j=3 | T[1,3] |       |       | (Length 3 - Root)
j=2 | T[1,2] | T[2,2] |       | (Length 2)
j=1 | T[1,1] | T[2,1] | T[3,1] | (Length 1 - Terminals)
-----+-------+-------+-------+
      w1      w2      w3
```

##  Complexity Analysis
| Dimension | Complexity |
| :--- | :--- |
| **Time Complexity** | $O(n^3 \cdot |G|)$ |
| **Space Complexity** | $O(n^2 \cdot |G|)$ |

- $n^2$ cells in the table.
- $n$ splits per cell.
- $|G|$ production rules per split.

##  Worked Example
**Grammar:**
$S \to AB$
$A \to a$
$B \to b$
**String:** $w = ab$

1. **Length 1:**
   $T[1, 1] = \{ A \}$ (because $A \to a$)
   $T[2, 1] = \{ B \}$ (because $B \to b$)
2. **Length 2:**
   $T[1, 2]$ needs split $k=1$:
   Check $A \to BC$ where $B \in T[1, 1]$ and $C \in T[2, 1]$.
   Is there a rule $S \to AB$? Yes.
   So $T[1, 2] = \{ S \}$.
3. **Acceptance:** $S \in T[1, 2]$, so $ab$ is accepted.

##  GATE Questions
**Question (GATE-style):**
In a CYK table for a string of length $n$, how many total cells are filled?
(A) $n$
(B) $n^2$
(C) $n(n+1)/2$
(D) $2n$
<details>
<summary>Solution</summary>
**Answer: (C)**
The table is a triangle:
Row 1 has $n$ cells.
Row 2 has $n-1$ cells.
... Row $n$ has 1 cell.
Total = $\sum_{i=1}^n i = \frac{n(n+1)}{2}$.
</details>

##  Edge Cases & Traps
- **Pre-requisite:** If the grammar is NOT in CNF, CYK will not work. You must convert it first!
- **Ordering:** Fill the table by **length** (rows), not by starting position (columns).

##  Connections Web
- [[Chomsky Normal Form]]  Required format.
- [[Dynamic Programming]]  Algorithm paradigm.
- [[Context Free Grammars]]  Base model.

##  Revision Checklist
- [ ] Do I understand the $T[i, j]$ notation?
- [ ] Can I fill a small CYK table ($n=3$ or $4$) by hand?
- [ ] Do I know the $O(n^3)$ derivation?
