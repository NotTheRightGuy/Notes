---
study_order: 16
tags:
  - GATE/CS
  - GATE/TOC
  - Algorithm
aliases:
  - Generating Variables Algorithm
  - Productive Variables
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: High
---

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Useless Variables In Cfl]]
**Sibling Topics:** [[Reachable Variables Algorithm]]

>  **Definition:** A variable $A$ is **generating** if $A \implies^* w$ for some $w \in \Sigma^*$.

---

##  Intuition
Think of it as a "bottom-up" check. Terminals already exist. If $A$ can directly produce terminals, $A$ exists. If $B$ can produce something that eventually becomes $A$ (which is already known to exist), then $B$ exists.

---

##  Algorithm (Formal)

```
Algorithm FIND_GENERATING(G=(V, T, P, S)):
    1. Let G_set = T (Set of all terminals)
    2. While G_set changes:
        For each production A ->  in P:
            If all symbols in  are in G_set:
                Add A to G_set
    3. Generating_Variables = G_set  V
```

---

##  Step-by-Step Example

**Grammar:**
1. $S \to AB \mid a$
2. $A \to b$
3. $B \to BC$
4. $C \to c$

**Trace:**
1. **Initial G_set:** $\{a, b, c\}$ (Terminals)
2. **Iteration 1:**
   - $S \to a$: $a \in G\_set \implies S$ added.
   - $A \to b$: $b \in G\_set \implies A$ added.
   - $C \to c$: $c \in G\_set \implies C$ added.
   - $B \to BC$: $C \in G\_set$, but $B \notin G\_set$. Can't add $B$.
   - **G_set now:** $\{a, b, c, S, A, C\}$
3. **Iteration 2:**
   - $B \to BC$: $C \in G\_set$, but $B$ still $\notin G\_set$.
   - No more changes.
4. **Final Result:** $\{S, A, C\}$ are generating. $B$ is **non-generating**.

---

##  Complexity
$O(|G|)$, where $|G|$ is the total length of all production strings. Each symbol is processed a constant number of times.

---

##  Connections Web
- [[Useless Variables In Cfl]]  Core application.
- [[Context-Free Grammar]]  Foundation.
- [[Epsilon Productions]]  Note that $\epsilon \in \Sigma^*$, so $A \to \epsilon$ makes $A$ generating.

---

##  Revision Checklist
- [ ] Can I identify generating variables in a grammar with $\epsilon$-productions?
- [ ] Can I identify a non-generating cycle (e.g., $A \to B, B \to A$)?
- [ ] Do I understand why we start with terminals?

---
 Note created: Generating Variables Algorithm.md
   Estimated read time: 3 minutes
