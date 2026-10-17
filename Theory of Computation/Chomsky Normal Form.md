---
study_order: 13
tags:
  - GATE/CS
  - GATE/TOC
  - ContextFreeGrammars
aliases:
  - CNF
  - Chomsky Normal Form
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: High
---

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Context Free Grammars]]
**Sibling Topics:** [[Greibach Normal Form]], [[CYK Algorithm]]
**Leads To:** [[Pumping Lemma For CFLs]], [[Parsing Algorithms]]

>  **GATE Syllabus Mapping:** Context-free languages and pushdown automata; Context-free grammars and their properties; Chomsky Normal Form.

##  Motivation & Intuition
In general [[Context Free Grammars]], productions can be messy: they can have mixed terminals and variables, empty strings ($\epsilon$), or long chains of variables. This variety makes it hard to design efficient algorithms for parsing or to prove theorems about the language.

**The Core Idea:** Every Context-Free Language (that doesn't contain $\epsilon$) can be represented by a grammar where every production is either a **binary branch** ($A \to BC$) or a **terminal leaf** ($A \to a$). This turns every [[Parse Tree]] into a strict **Binary Tree**, which is computationally much easier to handle.

##  Theory
### Formal Definition
A [[Context Free Grammar]] $G = (V, \Sigma, R, S)$ is in **Chomsky Normal Form (CNF)** if all its production rules are of the form:
1. $A \rightarrow BC$ (Exactly two variables)
2. $A \rightarrow a$ (Exactly one terminal)
3. $S \rightarrow \epsilon$ (Only if $\epsilon \in L(G)$, and $S$ does not appear on the RHS of any production)

Where $A, B, C \in V$ and $a \in \Sigma$.

### Why CNF Matters?
- **[[CYK Algorithm]]:** This $O(n^3)$ membership algorithm strictly requires the grammar to be in CNF.
- **Path Lengths:** In a CNF parse tree, a derivation of a string of length $n$ always takes exactly $2n-1$ steps.
- **Height vs Length:** If a parse tree in CNF has height $h$, the maximum length of the string generated is $2^{h-1}$. This is crucial for proving the [[Pumping Lemma For CFLs]].

##  Conversion Steps (The Pipeline)
To convert any CFG to CNF, follow these steps in **strict order**:

### 1. Eliminate $\epsilon$-productions
Find all **nullable** variables (variables that can derive $\epsilon$).
For a rule $A \to BCD$ where $B$ and $D$ are nullable, add all combinations: $A \to BCD | CD | BC | C$.

### 2. Eliminate Unit Productions ($A \to B$)
If $A \to B$ and $B \to \alpha$, add $A \to \alpha$. Repeat until all $A \to B$ forms are gone. Use a **Unit Dependency Graph** to avoid missing cycles.

### 3. Eliminate Useless Symbols
- **Non-generating:** Symbols that cannot derive a string of terminals.
- **Unreachable:** Symbols that cannot be reached from the start symbol $S$.

### 4. Replace Terminals in Mixed Body
For rules like $A \to aB$, replace $a$ with a new variable $X_a$ and add $X_a \to a$. Now $A \to X_a B$.

### 5. Break Long Productions
For $A \to B_1 B_2 B_3$, replace with:
$A \to B_1 C_1$
$C_1 \to B_2 B_3$

##  Visuals
### CNF Tree Structure
```text
      [A]          <-- Internal Node (A -> BC)
     /   \
   [B]   [C]
   / \    |
 [D] [E] [f]       <-- Leaf Node (C -> f)
```
*In CNF, every internal node has exactly two children (Variables) or one child (Terminal).*

##  Complexity Analysis
| Property | Value | Notes |
| :--- | :--- | :--- |
| **Derivation Steps** | $2n-1$ | For a string of length $n$ |
| **Max String Length** | $2^{h-1}$ | Where $h$ is tree height |
| **Conversion Complexity** | $O(|G|^2)$ | Size of grammar might increase quadratically |

##  Worked Example
**Grammar:**
$S \to aSb | ab$

**Step 1 & 2:** No $\epsilon$ or unit productions.
**Step 3:** No useless symbols.
**Step 4 (Terminals):**
Introduce $X_a \to a, X_b \to b$.
$S \to X_a S X_b | X_a X_b$
**Step 5 (Binary):**
$S \to X_a S_1 | X_a X_b$
$S_1 \to S X_b$
$X_a \to a$
$X_b \to b$

##  GATE Questions
**Question 1 (GATE-style):**
Which of the following productions is NOT allowed in CNF?
(A) $A \to BC$
(B) $A \to a$
(C) $A \to BCD$
(D) $S \to \epsilon$ (if S is start and not on RHS)
<details>
<summary>Solution</summary>
**Answer: (C)**
CNF allows only $A \to BC$ or $A \to a$. $A \to BCD$ has 3 variables, violating the binary branching rule.
</details>

##  Edge Cases & Traps
- **The $\epsilon$ Trap:** If you eliminate $\epsilon$-productions, the start symbol might become nullable. Only $S \to \epsilon$ is allowed in CNF if $\epsilon \in L$.
- **Order Matters:** If you eliminate useless symbols *before* unit productions, you might end up with new useless symbols. **Standard Order:** $\epsilon \to$ Unit $\to$ Useless.

##  Comparisons
| Feature | [[Chomsky Normal Form]] | [[Greibach Normal Form]] |
| :--- | :--- | :--- |
| **Form** | $A \to BC$ or $A \to a$ | $A \to a\alpha$ |
| **Parse Tree** | Binary Tree | General Tree |
| **Algorithm** | [[CYK Algorithm]] | PDA construction |

##  Connections Web
- [[Context Free Grammars]]  Base definition.
- [[CYK Algorithm]]  Applications.
- [[Pumping Lemma For CFLs]]  Uses CNF for proof.
- [[Pushdown Automata]]  Equivalent machine model.

##  Revision Checklist
- [ ] Can I define the two allowed forms of CNF?
- [ ] Do I remember the order of conversion? ($\epsilon \to$ Unit $\to$ Useless)
- [ ] Can I relate tree height to string length ($2^{h-1}$)?
