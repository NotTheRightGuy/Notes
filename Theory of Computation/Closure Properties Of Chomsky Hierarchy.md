---
study_order: 12
tags:
  - GATE/CS
  - GATE/TOC
  - closure-properties
  - chomsky-hierarchy
  - formal-languages
aliases:
  - Closure Properties Table
  - Chomsky Hierarchy Closures
date_created: 2026-04-14
difficulty: 
last_revised: 2026-04-14
pyq_frequency: High
---

# Closure Properties of Chomsky Hierarchy  Type 0 to Type 3

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Chomsky Hierarchy]]
**Sibling Topics:** [[Decision Properties]], [[Pumping Lemma]], [[Grammars]]
**Leads To:** [[Undecidability]], [[Complexity Theory]]

>  **GATE Syllabus Mapping:** Chomsky hierarchy of languages: regular, context-free, context-sensitive, and recursively enumerable; closure properties of language classes.

---

##  Motivation & Intuition
In [[Formal Language Theory]], a class of languages is **closed** under an operation if applying that operation to languages in the class always results in a language that stays within the same class.

Think of it like **integers under addition**: $5 + 3 = 8$ (still an integer). But integers are **not closed under division**: $5 / 2 = 2.5$ (not an integer). 

For GATE, knowing these properties is the "low-hanging fruit" that allows you to solve complex problems about language transformations and $L_1 \cap L_2$ style questions instantly.

---

##  Theory

### 1. The Chomsky Hierarchy Summary
The hierarchy defines the containment relationship: $\text{Regular} \subset \text{Context-Free} \subset \text{Context-Sensitive} \subset \text{Recursive} \subset \text{Recursively Enumerable}$.

| Type | Language Name | Machine (Acceptor) | Grammar Type |
| :--- | :--- | :--- | :--- |
| **Type 3** | [[Regular Language]] | [[Finite Automaton]] (DFA/NFA) | Regular Grammar |
| **Type 2** | [[Context-Free Language]] | [[Pushdown Automaton]] (PDA) | Context-Free Grammar |
| **Type 1** | [[Context-Sensitive Language]] | [[Linear Bounded Automaton]] (LBA) | Context-Sensitive Grammar |
| **Type 0** | [[Recursively Enumerable Language]] | [[Turing Machine]] (TM) | Unrestricted Grammar |

---

##  Closure Properties Table
This table is the core reference for GATE.

| **Property**                           | **Regular (Type 3)** | **Context-Free (Type 2)** | **Context-Sensitive (Type 1)** | **Rec. Enumerable (Type 0)** |
| :------------------------------------- | :------------------: | :-----------------------: | :----------------------------: | :--------------------------: |
| **Union** ($L_1 \cup L_2$)             |       **Yes**        |          **Yes**          |            **Yes**             |           **Yes**            |
| **Intersection** ($L_1 \cap L_2$)      |       **Yes**        |          **No**           |            **Yes**             |           **Yes**            |
| **Concatenation** ($L_1 \cdot L_2$)    |       **Yes**        |          **Yes**          |            **Yes**             |           **Yes**            |
| **Kleene Star** ($L^*$)                |       **Yes**        |          **Yes**          |            **Yes**             |           **Yes**            |
| **Complement** ($\bar{L}$)             |       **Yes**        |          **No**           |            **Yes**             |            **No**            |
| **Difference** ($L_1 - L_2$)           |       **Yes**        |          **No**           |            **Yes**             |            **No**            |
| **Reversal** ($L^R$)                   |       **Yes**        |          **Yes**          |            **Yes**             |           **Yes**            |
| **Homomorphism** ($h(L)$)              |       **Yes**        |          **Yes**          |             **No**             |           **Yes**            |
| **Inverse Homomorphism** ($h^{-1}(L)$) |       **Yes**        |          **Yes**          |            **Yes**             |           **Yes**            |
| **Int. with Regular** ($L \cap R$)     |       **Yes**        |          **Yes**          |            **Yes**             |           **Yes**            |
| **Substitution**                       |       **Yes**        |          **Yes**          |             **No**             |           **Yes**            |
| **Subset**                             |        **No**        |          **No**           |             **No**             |            **No**            |


##  Complexity Analysis & Justification
- **Regular Languages:** Use the **Product Construction** for intersection/union and the **State Flipping** (in DFA) for complementation.
- **CFLs:** Intersection fails because a PDA only has **one stack**. To find $L_1 \cap L_2$, you'd need two stacks to track both languages simultaneously, which effectively creates a [[Turing Machine]] power level.
- **CSLs:** The proof for closure under complement (ImmermanSzelepcsnyi theorem) was a major breakthrough in complexity theory.
- **RELs:** Complement fails because if both $L$ and $\bar{L}$ were recursively enumerable, $L$ would be **Recursive** (Decidable). Since many RELs are undecidable, they cannot be closed under complement.

---

##  Worked Example

**Problem:** Given $L_1$ is a [[Context-Free Language]] and $L_2$ is a [[Regular Language]], is $L_1 - L_2$ context-free?

**Step-by-step reasoning:**
1. Express Difference using other operations: $L_1 - L_2 = L_1 \cap \bar{L_2}$.
2. We know [[Regular Language]] is closed under **Complement**: So $\bar{L_2}$ is also Regular.
3. We know [[Context-Free Language]] is closed under **Intersection with Regular**: $L_{CFL} \cap L_{REG} = L_{CFL}$.
4. Therefore, $L_1 \cap \bar{L_2}$ is Context-Free.
5. **Result:** Yes, $L_1 - L_2$ is Context-Free.

---

##  GATE Questions

**Question 1  GATE 2015:**
Which of the following language classes is NOT closed under complementation?
- (A) Regular Languages
- (B) Context-Free Languages
- (C) Context-Sensitive Languages
- (D) Recursive Languages

<details>
<summary> Solution (click to reveal)</summary>

**Answer: (B)**

**Step-by-step reasoning:**
- (A) Regular: Closed (Flip final/non-final states in DFA).
- (B) **CFL: NOT Closed.** Example: $L_1 = \{a^n b^n c^m\}$ and $L_2 = \{a^m b^n c^n\}$. Their intersection is not CFL. If they were closed under complement, they would be closed under intersection (via De Morgan's), which they aren't.
- (C) CSL: Closed (ImmermanSzelepcsnyi theorem).
- (D) Recursive: Closed (Swap 'Halt-Accept' and 'Halt-Reject' on TM).

**Trap to avoid:** Confusing **Deterministic CFLs** with General CFLs. DCFLs are closed under complement, but General CFLs are not!

</details>

---

##  Edge Cases & Traps
- [ ] **DCFL vs CFL:** Deterministic CFLs are closed under **Complement** but NOT under Union or Intersection.
- [ ] **Homomorphism vs CSL:** CSL is NOT closed under homomorphism (it can "shrink" the string length, violating the $\alpha \to \beta, |\alpha| \le |\beta|$ rule). However, it is closed under **$\epsilon$-free Homomorphism**.
- [ ] **Recursive vs REL:** Recursive languages are closed under **Complement**, but Recursively Enumerable (REL) are NOT.
- [ ] **Subset/Superset:** Just because $L_1 \subset L_2$ and $L_2$ is Regular, it does NOT mean $L_1$ is Regular.

---

##  Comparisons

| Feature | Regular | CFL | DCFL | REL |
| :--- | :--- | :--- | :--- | :--- |
| **Union** |  |  |  |  |
| **Intersection** |  |  |  |  |
| **Complement** |  |  |  |  |

---

##  Memory Hooks
1. **The "Everything" Class:** [[Regular Language]] is the "Golden Child"it is closed under every operation you'll see in GATE.
2. **CFL Intersection/Complement Fail:** Think of the "Single Stack Limitation." You can't match two independent counts (Intersection) or easily negate a non-deterministic process (Complement).
3. **REL Complement Fail:** If $L$ and $\bar{L}$ are both RE, the language is Decidable (Recursive). This is the foundation of [[Undecidability]] proofs.

---

##  Connections Web
**Prerequisite Knowledge:**
- [[Set Theory]]  Union, Intersection, Complement definitions.
- [[Finite Automaton]]  To understand Regular closure.

**Builds Upon This Topic:**
- [[Undecidability]]  Uses REL closure properties.
- [[Complexity Classes]]  P vs NP closures.

**Standard References:**
- [[Ulman/Hopcroft/Motwani]] Chapter 7 & 11.
- [[Peter Linz]] Section 8.3.

---

##  Revision Checklist
- [ ] I can reproduce the closure table for CFLs and RELs from memory.
- [ ] I understand why CFL is closed under $L \cap R$ but not $L \cap L$.
- [ ] I can derive the closure of $(L_1 - L_2)$ for any two language types.
- [ ] I know the distinction between CFL and DCFL closure properties.

---
 Note created: Closure Properties of Chomsky Hierarchy.md
   Sections: 13/13 complete
   Wiki Links: 15 found
   Estimated read time: 6 minutes
