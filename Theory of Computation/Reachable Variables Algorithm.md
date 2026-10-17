---
study_order: 17
tags:
  - GATE/CS
  - GATE/TOC
  - Algorithm
aliases:
  - Reachable Variables Algorithm
  - Accessible Variables
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: High
---

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Useless Variables In Cfl]]
**Sibling Topics:** [[Generating Variables Algorithm]]

>  **Definition:** A variable $A$ is **reachable** if $S \implies^* \alpha A \beta$ for some $\alpha, \beta \in (V \cup \Sigma)^*$.

---

##  Intuition
Think of it as a "top-down" check. We start at the "power source" (the Start symbol $S$). If we can follow a path through the productions to get to a variable $A$, then $A$ is reachable. If $A$ is not reachable, it doesn't matter how well it generates terminalsit's disconnected!

---

##  Algorithm (Formal)

```
Algorithm FIND_REACHABLE(G=(V, T, P, S)):
    1. Let R_set = { S }
    2. While R_set changes:
        For each variable A in R_set:
            For each production A -> :
                Add all variables and terminals in  to R_set
    3. Reachable_Symbols = R_set
```

---

##  Step-by-Step Example

**Grammar:**
1. $S \to a$
2. $A \to b$
3. $C \to c$

**Trace:**
1. **Initial R_set:** $\{ S \}$
2. **Iteration 1:**
   - From $S \to a$, add $a$ to $R\_set$.
   - **R_set now:** $\{ S, a \}$
3. **Iteration 2:**
   - No more productions from $S$.
   - $A$ and $C$ are not in $R\_set$.
   - No more changes.
4. **Final Result:** $\{ S, a \}$ are reachable. $A, C, b, c$ are **non-reachable**.

---

##  Complexity
$O(|V| + |P|)$, which is essentially a graph traversal (BFS or DFS) starting from $S$ through the dependency graph of the productions.

---

##  Connections Web
- [[Useless Variables In Cfl]]  Core application.
- [[Context-Free Grammar]]  Foundation.
- [[Simplified Cfg]]  Only reachable symbols are allowed in a simplified grammar.

---

##  Revision Checklist
- [ ] Can I identify reachable symbols using a dependency graph?
- [ ] Do I understand that symbols on the RHS of a non-reachable variable's production are also potentially non-reachable?
- [ ] Do I know that terminals can be non-reachable too?

---
 Note created: Reachable Variables Algorithm.md
   Estimated read time: 3 minutes
