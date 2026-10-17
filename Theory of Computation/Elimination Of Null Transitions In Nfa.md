---
study_order: 4
subject: Theory of Computation
topic: Elimination of null transitions in NFA
status: to-review
tags:
  - TOC
  - AutomataTheory
  - GATE-CS
---

# Elimination of Null Transitions (-NFA to NFA)

Context: [[Theory Of Computation Index]] | [[Nfa]]

## 1. Definition and Motivation
An **-NFA** (NFA with null transitions) allows a transition from one state to another without consuming any input symbol, denoted by $\epsilon$. While -NFAs are easier to construct for complex [[Regular Languages]], they are harder to implement. 

The goal of **Eliminating Null Transitions** is to convert an -NFA into an equivalent standard [[Nfa]] (without $\epsilon$) that accepts the same language.

---

## 2. Concept of -closure
The **-closure** of a state $q$, denoted as $ECL(q)$ or $\epsilon\text{-closure}(q)$, is the set of all states reachable from $q$ by following only $\epsilon$ transitions (including $q$ itself).

### Mathematical Definition
For an -NFA $M = (Q, \Sigma, \delta, q_0, F)$:
1. $q \in \epsilon\text{-closure}(q)$ (Reflexivity)
2. If $p \in \epsilon\text{-closure}(q)$ and $\delta(p, \epsilon) = r$, then $r \in \epsilon\text{-closure}(q)$.

---

## 3. Step-by-Step Construction (Conversion Algorithm)
To convert an -NFA $M = (Q, \Sigma, \delta, q_0, F)$ into an equivalent NFA $M' = (Q, \Sigma, \delta', q_0, F')$, follow these steps:

### Step A: Calculate -closure
Find the $\epsilon\text{-closure}$ for every state $q \in Q$.

### Step B: Define the New Transition Function ($\delta'$)
The new transition function $\delta'$ for a state $q$ and input $a \in \Sigma$ is defined as:
$$\delta'(q, a) = \epsilon\text{-closure}(\delta(\epsilon\text{-closure}(q), a))$$
In simpler terms:
1. Start at $q$.
2. See where you can go using only $\epsilon$ transitions ($ECL(q)$).
3. From those states, see where you can go using the input symbol $a$.
4. From those resulting states, see where you can go using only $\epsilon$ transitions ($ECL(\text{results})$).

### Step C: Determine New Final States ($F'$)
A state $q$ in the new NFA becomes a **Final State** if its $\epsilon\text{-closure}$ contains at least one final state from the original -NFA:
$$F' = \{q \in Q \mid \epsilon\text{-closure}(q) \cap F \neq \emptyset\}$$

---

## 4. Visual Representation & Example
Consider the -NFA:
$q_0 \xrightarrow{\epsilon} q_1 \xrightarrow{a} q_2$
Where $F = \{q_2\}$.

### Conversion Process:
1. **$\epsilon\text{-closures}$**:
   - $ECL(q_0) = \{q_0, q_1\}$
   - $ECL(q_1) = \{q_1\}$
   - $ECL(q_2) = \{q_2\}$

2. **New Transitions ($\delta'$)**:
   - $\delta'(q_0, a) = ECL(\delta(ECL(q_0), a)) = ECL(\delta(\{q_0, q_1\}, a)) = ECL(\{q_2\}) = \{q_2\}$
   - $\delta'(q_1, a) = ECL(\delta(ECL(q_1), a)) = ECL(\delta(\{q_1\}, a)) = ECL(\{q_2\}) = \{q_2\}$
   - $\delta'(q_2, a) = \emptyset$

3. **New Final States ($F'$)**:
   - $ECL(q_0) = \{q_0, q_1\}$ (No $q_2$) $\rightarrow$ Not Final.
   - $ECL(q_1) = \{q_1\}$ (No $q_2$) $\rightarrow$ Not Final.
   - $ECL(q_2) = \{q_2\}$ (Contains $q_2$) $\rightarrow$ **Final**.

**Resulting NFA**: $q_0 \xrightarrow{a} q_2$ and $q_1 \xrightarrow{a} q_2$, with $F' = \{q_2\}$.

---

## 5. Complexity Table

| Metric | -NFA | Resulting NFA |
| :--- | :--- | :--- |
| **State Count** | $n$ | $n$ (Remains Same) |
| **Transitions** | Fewer (includes $\epsilon$) | Potentially More |
| **Language Power** | [[Regular Languages]] | [[Regular Languages]] |

---

## 6. GATE Pro-Tips: The "Memory Hook"
> [!TIP]
> **The Triple-Jump Rule**: To find $\delta'(q, a)$, remember the sequence: **$\epsilon$-closure $\rightarrow$ Symbol $a$ $\rightarrow$ $\epsilon$-closure**.

- **Trap Alert**: The number of states **never increases** during this conversion. If a question asks if a 5-state -NFA can be converted to a 5-state NFA, the answer is always **Yes**.
- **Equivalence**: -NFA $\equiv$ NFA $\equiv$ [[DFA]]. They all recognize the same class of languages.
- **Initial State**: The start state remains the same, but it might become a final state if it can reach a final state via $\epsilon$ transitions.

---
**Related Concepts**:
- [[DFA]]
- [[Nfa]]
- [[Subset Construction]]
- [[Regular Expressions]]
