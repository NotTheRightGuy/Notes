---
study_order: 26
tags:
  - GATE/CS
  - GATE/TOC
  - Post-Correspondence-Problem
aliases:
  - PCP
  - Domino Problem
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: Medium
---

##  Context
**Subject:** [[Theory Of Computation Index]]
**Parent Topic:** [[Undecidability In Toc]]
**Sibling Topics:** [[Rices Theorem]], [[Decidability Core Definition]]
**Leads To:** [[Decision Properties Of Cfls]]

>  **GATE Syllabus Mapping:** Undecidability; PCP.

---

##  Motivation & Intuition
If [[Undecidability In Toc|Undecidability]] is a computer problem, **PCP** is a **puzzle problem**. It's the standard way to prove that even simple string-matching problems can be unsolvable.

**Analogy:** You have several different types of Lego bricks (dominoes). Each brick has a top part and a bottom part (both are strings). Can you arrange these bricks in some order (using as many as you want) such that the string formed on top is **exactly** the string on the bottom?

**Core Idea:** Finding a sequence of strings where the concatenated prefix equals the concatenated suffix is **Undecidable**.

---

##  Theory

### 1. Formal Statement
Given two lists of strings $A = (w_1, w_2, \dots, w_n)$ and $B = (v_1, v_2, \dots, v_n)$ over an alphabet $\Sigma$, is there a sequence of indices $i_1, i_2, \dots, i_k$ (where $1 \leq i_j \leq n$) such that:
$$w_{i_1} w_{i_2} \dots w_{i_k} = v_{i_1} v_{i_2} \dots v_{i_k}$$

### 2. Status
- **General PCP:** Undecidable (proved by reduction from $A_{TM}$).
- **RE status:** Recursively Enumerable (RE). If a solution exists, we can eventually find it by searching all possible sequences.
- **Special Case (Small Alphabet):** Even with $|\Sigma| = 2$, it's undecidable.
- **Special Case (Single String):** If $n=1$, it is decidable (trivial).

### 3. Modified PCP (MPCP)
In MPCP, the sequence of indices **must start** with index 1 ($i_1 = 1$).
- MPCP is also undecidable.
- $A_{TM} \leq_m \text{MPCP} \leq_m \text{PCP}$.

---

##  Diagrams & Visuals

### Domino Visual
Suppose $A = \{a, ab, bba\}$ and $B = \{baa, aa, bb\}$.
Indices:
1. $\left[ \frac{a}{baa} \right]$
2. $\left[ \frac{ab}{aa} \right]$
3. $\left[ \frac{bba}{bb} \right]$

A solution might look like sequence $(3, 2, 1)$:
Top: $bba + ab + a = bbaaba$
Bottom: $bb + aa + baa = bbaaba$
**Yes, a match!**

---

##  Complexity Analysis
- Finding if a solution exists is **Undecidable**.
- However, if a solution exists, the language of all solvable PCP instances is **Recursively Enumerable**.
- The complement (instances with no solution) is **Not RE**.

---

##  Worked Example

**Question:** Is the following PCP instance solvable?
- $w_1 = b$, $v_1 = bb$
- $w_2 = ba$, $v_2 = a$

**Steps:**
1. Let's try starting with index 1:
   - Top: $b$
   - Bottom: $bb$
   - Difference: bottom has an extra $b$ at the end.
2. We need something that starts with $b$ to match it. Only index 1 starts with $b$.
   - Index 1 again: Top: $bb$, Bottom: $bbb$.
   - Difference: bottom is still longer.
3. This will never end because $v_1$ is always longer than $w_1$, and $w_2$ can't help because $v_2$ starts with $a$.
**Conclusion:** No solution. (This instance is decidable, but the general problem is not).

---

##  GATE Questions

**Question 1 (GATE-2002):**
Which of the following problems is undecidable?
- (A) Membership for CFGs.
- (B) Emptiness for CFGs.
- (C) Ambiguity of a CFG.
- (D) Finiteness of a CFG.

<details>
<summary> Solution (click to reveal)</summary>

**Answer: (C)**

**Reasoning:**
- (A), (B), (D) are all **Decidable** for [[Decision Properties Of Cfls|Context-Free Languages]].
- (C) **Ambiguity of a CFG** is undecidable. This is typically proved by reducing from **PCP**. If we could decide ambiguity, we could solve PCP.

</details>

---

##  Edge Cases & Traps
- [ ] **"Is L(G) ambiguous?"**: Undecidable.
- [ ] **"Is L(G) = *?"**: Undecidable for CFGs. (Compare: [[Decision Properties Of Regular Languages|Decidable For Regular]]).
- [ ] **RE vs Decidable:** Remember PCP is RE, but not decidable.

---

##  Comparisons

| Feature | Regular Languages | Context-Free Languages |
| :--- | :--- | :--- |
| **Membership** | Decidable | Decidable |
| **Emptiness** | Decidable | Decidable |
| **Ambiguity** | Decidable | **Undecidable (via PCP)** |
| **L = *** | Decidable | **Undecidable** |

---

##  Memory Hooks
- **"PCP = Puzzle"**: If it looks like a string puzzle, it's PCP.
- **"PCP  CFG"**: Use PCP to remember that almost all "Equivalence" or "Ambiguity" problems in Context-Free Languages are undecidable.

---

##  Connections Web
- [[Decision Properties Of Cfls]] $\rightarrow$ Uses PCP for proofs.
- [[Undecidability In Toc]] $\rightarrow$ The family it belongs to.
- [[Recursively Enumerable Languages]] $\rightarrow$ PCP is a member.
- [[Theory Of Computation Index]] $\rightarrow$ The main roadmap.

---

##  Revision Checklist
- [ ] I can state the PCP problem.
- [ ] I know that PCP is undecidable but RE.
- [ ] I understand the relationship between PCP and CFG ambiguity.
- [ ] I can trace a small PCP instance to find a solution.

---
 Note created: Post_Correspondence_Problem.md
   Sections: 13/13 complete
   Wiki Links: 11 found
   Estimated read time: 6 minutes
