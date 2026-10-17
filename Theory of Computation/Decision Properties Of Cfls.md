---
study_order: 22
tags:
  - GATE/CS
  - GATE/TOC
  - DecisionProperties
aliases:
  - Decidability of CFLs
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: Very High
---

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Context Free Languages]]
**Sibling Topics:** [[Decision Properties Of Regular Languages]], [[Closure Properties Of CFLs]]
**Leads To:** [[Undecidability]]

>  **GATE Syllabus Mapping:** Context-free languages and pushdown automata; Decidability and undecidability of language properties.

##  Motivation & Intuition
If I give you a grammar, can you tell me if it produces *any* string at all (Emptiness)? Or if it's infinite? Or if it's the same as another grammar?
**The "Stack Rule of Thumb":** If you can solve it by looking for paths in a [[Parse Tree]] or using [[CYK Algorithm]], it's usually **Decidable**. If it requires "matching" two different stacks or universal coverage, it's probably **Undecidable**.

##  Theory
### Decidable Properties (We have algorithms)
1. **Membership ($w \in L$):** Use the [[CYK Algorithm]] ($O(n^3)$).
2. **Emptiness ($L = \emptyset$):** Check if any terminals can be generated from the start symbol $S$. This is just a **reachability** test in the grammar graph.
3. **Finiteness ($L$ is finite):** In a reduced grammar (no useless symbols), $L$ is infinite if and only if there's a **cycle** in the variable dependency graph.
4. **Generating Symbols:** Determining which variables generate strings.

### Undecidable Properties (No algorithm exists!)
1. **Universality ($L = \Sigma^*$):** Does the CFG generate every possible string? (Unlike Regular, this is **undecidable** for CFLs).
2. **Equivalence ($L_1 = L_2$):** Are two CFGs generating the same language?
3. **Intersection-Emptiness ($L_1 \cap L_2 = \emptyset$):** Because intersection isn't a CFL, we can't test this.
4. **Inclusion ($L_1 \subseteq L_2$):** If inclusion were decidable, equivalence would be too.
5. **Regularity ($L$ is Regular?):** Can this CFL be represented by a [[Finite Automata]]?
6. **Ambiguity:** Is this CFG ambiguous?

##  Decision Table (Regular vs CFL)
| Problem | Regular | CFL | DCFL |
| :--- | :---: | :---: | :---: |
| Membership ($w \in L$) |  |  |  |
| Emptiness ($L = \emptyset$) |  |  |  |
| Finiteness ($L$ is finite) |  |  |  |
| **Universality ($L = \Sigma^*$)** |  |  |  |
| **Equivalence ($L_1 = L_2$)** |  |  |  |
| **Ambiguity** |  |  |  |

*( = Decidable,  = Undecidable)*

##  GATE Questions
**Question 1 (GATE):**
Which of the following problems is decidable for context-free languages?
(A) Is $L_1 \cap L_2 = \emptyset$?
(B) Is $L = \Sigma^*$?
(C) Is $L$ finite?
(D) Is $L_1 = L_2$?
<details>
<summary>Solution</summary>
**Answer: (C)**
Emptiness, Finiteness, and Membership are the **Big Three Decidables** for CFLs. The rest are undecidable.
</details>

##  Edge Cases & Traps
- **DCFL Power:** Notice that **Universality** and **Equivalence** are **Decidable for DCFLs**. This is because DCFLs are closed under complement, allowing us to check $L_1 = L_2$ via symmetric difference.
- **Regular Intersection Decidability:** Is "$L \cap R = \emptyset$" decidable for CFL $L$ and Regular $R$? **Yes!** Because $L \cap R$ is a CFL, and emptiness of CFLs is decidable. This is a very common GATE question.

##  Memory Hooks
- **"Members (Membership), Empty (Emptiness), Fine (Finiteness)":** These are the only things you can definitely tell about a CFL.
- **"Regular can do anything, CFL can only do a little, DCFL can do more":** A hierarchy of decidability.

##  Connections Web
- [[Decision Properties Of Regular Languages]]  Comparison.
- [[CYK Algorithm]]  Solution for membership.
- [[Chomsky Normal Form]]  Used in CYK.

##  Revision Checklist
- [ ] Can I list the three decidable properties for CFLs?
- [ ] Do I know why $L_1 \cap L_2 = \emptyset$ is undecidable?
- [ ] Can I remember which properties become decidable for **DCFLs**?
- [ ] Do I understand why $L \cap R = \emptyset$ is decidable?
