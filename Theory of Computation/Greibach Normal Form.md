---
study_order: 14
tags:
  - GATE/CS
  - GATE/TOC
  - GreibachNormalForm
aliases:
  - GNF
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: Low
---

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Context Free Grammars]]
**Sibling Topics:** [[Chomsky Normal Form]]
**Leads To:** [[Pushdown Automata]]

>  **GATE Syllabus Mapping:** Context-free languages and pushdown automata; Normal forms of context-free grammars.

##  Motivation & Intuition
In [[Chomsky Normal Form]], we have binary branches. In **Greibach Normal Form (GNF)**, we want every production to **generate exactly one terminal symbol** at the very beginning of its right-hand side.

**The "Stack Interaction" Intuition:** In a [[Pushdown Automata]] (PDA), we read one terminal symbol and then push some variables onto the stack. GNF mirrors this perfectly: $A \to a \alpha$ where $a$ is the terminal read and $\alpha$ are the variables pushed.

##  Theory
### Formal Definition
A [[Context Free Grammar]] $G = (V, \Sigma, R, S)$ is in **Greibach Normal Form (GNF)** if all its production rules are of the form:
$A \rightarrow a \alpha$
Where:
- $a \in \Sigma$ (Exactly one terminal at the start).
- $\alpha \in V^*$ (Zero or more variables follow).

### Why GNF Matters?
- **PDA Equivalence:** Directly translates to a 1-state PDA that accepts by empty stack.
- **Linear Derivations:** Every step in a derivation generates exactly one terminal symbol. For a string of length $n$, the derivation takes exactly $n$ steps.
- **No Infinite Loops:** Since every step produces a terminal, we can't have infinite loops of variable substitutions without generating terminals.

##  Conversion Sketch
Converting to GNF is significantly harder than CNF. It involves:
1. **Converting to CNF** first.
2. **Eliminating Left Recursion** ($A \to A \alpha \mid \beta$).
3. **Back-substitution** to ensure all rules start with a terminal.

##  Visuals
### GNF Tree Structure
```text
      [A]          <-- Internal Node
     / | \ \
    a [B][C][D]    <-- Terminal 'a' always on the left
```
*In GNF, every derivation step "consumes" a terminal and "produces" variables.*

##  Complexity Analysis
| Property | Value | Notes |
| :--- | :--- | :--- |
| **Derivation Steps** | $n$ | For a string of length $n$ |
| **Space Complexity** | $O(|G|^3)$ | The number of rules can explode |

##  Worked Example
**Grammar:**
$S \to aS | b$

**Is this in GNF?**
1. $S \to aS$: Starts with terminal $a$, followed by variable $S$. **Yes.**
2. $S \to b$: Starts with terminal $b$, followed by nothing. **Yes.**

**Conclusion:** This grammar is already in GNF.

##  GATE Questions
**Question (GATE-style):**
If a CFG is in GNF, what is the maximum length of a string that can be generated in $k$ derivation steps?
(A) $2^k$
(B) $k$
(C) $k-1$
(D) $2k$
<details>
<summary>Solution</summary>
**Answer: (B)**
In GNF, every step produces exactly one terminal symbol. Therefore, $k$ steps will always produce a string of length $k$.
</details>

##  Edge Cases & Traps
- **$\epsilon$ Exception:** GNF (like CNF) usually requires the language to be $\epsilon$-free. If $\epsilon \in L$, we handle it separately at the start symbol.
- **Mixing Terminals:** GNF forbids $A \to a B c$. You must replace $c$ with a variable $X_c \to c$ to get $A \to a B X_c$.

##  Comparisons
| Feature | [[Chomsky Normal Form]] | [[Greibach Normal Form]] |
| :--- | :--- | :--- |
| **Derivation length** | $2n-1$ steps | $n$ steps |
| **Form** | $A \to BC \mid A \to a$ | $A \to a \alpha$ |
| **Best used for** | [[CYK Algorithm]] | [[Pushdown Automata]] |

##  Connections Web
- [[Context Free Grammars]]  Base definition.
- [[Pushdown Automata]]  Relationship to 1-state PDAs.
- [[Chomsky Normal Form]]  Step 1 of GNF conversion.

##  Revision Checklist
- [ ] Can I define the GNF form? ($A \to a \alpha$)
- [ ] Do I understand why it takes exactly $n$ steps for a string of length $n$?
- [ ] Can I relate GNF to the behavior of a PDA's stack?
