---
study_order: 10
tags:
  - GATE/CS
  - GATE/TOC
  - DecisionProperties
aliases:
  - Decidable Problems for Regular Languages
date_created: 2026-04-13
difficulty: 
last_revised: 2026-04-13
pyq_frequency: High
---

##  Context
**Subject:** [[Theory Of Computation]]
**Parent Topic:** [[Regular Languages Definition]]
**Sibling Topics:** [[Closure Properties Of Regular Languages]]
**Leads To:** [[Decision Properties Of Cfls]]

>  **GATE Syllabus Mapping:** Regular expressions and finite automata. Decision properties of regular languages.

##  Motivation & Intuition
If I give you a machine, what can you tell me about it? Can you tell me if it accepts any strings at all? Can you tell me if it accepts an infinite number of strings? For **Regular Languages**, these questions are all **decidable**. This means there is an algorithm (a computer program) that will always give the correct answer and eventually terminate.

**Core Idea:** Almost every question about Regular Languages is **decidable**.

##  Theory
A decision problem is **decidable** if there's an algorithm to solve it. For a regular language $L$:

### 1. Membership Problem
- **Problem:** Given $w \in \Sigma^*$, is $w \in L$?
- **Solution:** Run $w$ on the DFA for $L$. If it ends in an accept state, YES; else NO.
- **Complexity:** $O(|w|)$.

### 2. Emptiness Problem
- **Problem:** Is $L = \emptyset$?
- **Solution:** In the DFA graph, check if any **accepting state** is reachable from the **start state** (using BFS or DFS).
- **Complexity:** $O(n+e)$ where $n, e$ are states/transitions.

### 3. Finiteness Problem
- **Problem:** Is $L$ finite?
- **Solution:** In the DFA graph (after removing states that cannot reach an accepting state), check if there are any **cycles**. If a cycle exists, $L$ is infinite.
- **Complexity:** $O(n+e)$.

### 4. Equivalence Problem
- **Problem:** Is $L_1 = L_2$?
- **Solution:** Construct the DFA for $(L_1 \cap \overline{L_2}) \cup (\overline{L_1} \cap L_2)$. If this DFA's language is **empty**, then $L_1 = L_2$.
- **Complexity:** $O(n_1 \times n_2)$.

### 5. Subset Problem
- **Problem:** Is $L_1 \subseteq L_2$?
- **Solution:** Check if $L_1 \cap \overline{L_2} = \emptyset$. If YES, then $L_1 \subseteq L_2$.

##  Complexity Summary
| Problem | Algorithm | Time Complexity |
|---------|-----------|-----------------|
| Membership | DFA simulation | $O(|w|)$ |
| Emptiness | Graph Reachability | $O(V+E)$ |
| Finiteness | Cycle detection | $O(V+E)$ |
| Equivalence | Product DFA + Emptiness | $O(n_1 \cdot n_2)$ |

##  Worked Example
**Is $L = (a+b)^*(ab+ba)$ infinite?**
1. **DFA:** Build the DFA.
2. **Cycle Test:** The state after seeing `ab` or `ba` is an accepting state. From there, you can see `a` or `b` to go back to other states that eventually reach the same or other accepting states.
3. **Observation:** There's a self-loop on the accepting state (or a cycle involving it).
4. **Conclusion:** YES, $L$ is infinite.

##  GATE Questions
**Question:** Which of the following is UNDECIDABLE?
(A) Is $L$ empty (for regular $L$)?
(B) Is $L$ finite (for regular $L$)?
(C) Is $L_1 = L_2$ (for regular $L_1, L_2$)?
(D) None of the above.

<details>
<summary> Solution</summary>
**Answer: (D)**
All properties of regular languages (membership, emptiness, finiteness, equivalence, containment) are **decidable**. This is a major contrast to [[Context Free Languages]], where equivalence and containment are undecidable.
</details>

##  Edge Cases & Traps
- [ ] **Cycle vs. Useful Cycle:** A cycle only makes the language infinite if it can be reached from the start AND can reach an accept state.
- [ ] **NFA vs. DFA:** For equivalence, converting NFAs to DFAs takes exponential time ($2^n$), but it remains **decidable**.

##  Comparisons
| Problem | Regular | Context-Free |
|---------|---------|--------------|
| Membership |  Yes |  Yes |
| Emptiness |  Yes |  Yes |
| Finiteness |  Yes |  Yes |
| Equivalence |  **Yes** |  **No** |
| Intersection is empty? |  Yes |  No |

##  Memory Hooks
- **"The All-Decidable Class":** If it's regular, you can always solve it.
- **Trap:** For context-free, $L_1 = L_2$ is NOT decidable. Don't mix them up!

##  Connections Web
- [[Dfa Deterministic Finite Automata]]  The engine for all algorithms here.
- [[Closure Properties Of Regular Languages]]  Used to prove equivalence and subset decidability.
- [[Context Free Languages]]  To understand where decidability starts to break down.

##  Revision Checklist
- [ ] I can describe the emptiness test using BFS.
- [ ] I know why finiteness requires checking for cycles in useful states.
- [ ] I understand how intersection and complement are used for equivalence.
