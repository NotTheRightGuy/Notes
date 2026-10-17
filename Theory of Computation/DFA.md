---
study_order: 2
subject: Theory of Computation
topic: DFA
tags: [TheoryOfComputation, FiniteAutomata, GATE-CS, TOC]
status: reviewed
---

# Context
Parent Index: [[Theory Of Computation Index]]
Related Concepts: [[Nfa]], [[DFA Minimization]], [[Regular Languages]]

---

# Deterministic Finite Automata (DFA)

A **Deterministic Finite Automaton (DFA)** is a 5-tuple $M = (Q, \Sigma, \delta, q_0, F)$ that recognizes a [[Regular Languages]].

## 5-Tuple Definition
1. $Q$: Finite set of states.
2. $\Sigma$: Finite set of input symbols (alphabet).
3. $\delta: Q \times \Sigma \to Q$: The **Transition Function**.
4. $q_0 \in Q$: The **Start State**.
5. $F \subseteq Q$: The set of **Final (Accepting) States**.

## Key Logical Requirement: "Deterministic"
For every state $q \in Q$ and every symbol $a \in \Sigma$, there is **exactly one** transition defined. No choice is allowed, unlike an [[Nfa]].

---

## DFA Characteristics for GATE
- **Trap States**: If a DFA must reject any further input after a specific condition, it transitions to a **Dead State** (trap state), where it stays for all subsequent symbols in $\Sigma$.
- **Language Equivalence**: Every [[Nfa]] can be converted into an equivalent DFA. The number of states in the DFA may be up to $2^n$ where $n$ is the number of states in the NFA.
- **Minimization**: To find the smallest possible DFA for a language, use the [[DFA Minimization]] partitioning algorithm.

## Complexity Table
| Operation | Complexity | Note |
| :--- | :--- | :--- |
| **Membership Testing** | $O(w)$ | Where $w$ is the length of the string. |
| **NFA to DFA** | $O(2^n)$ | Exponential worst-case state explosion. |
| **DFA Minimization** | $O(n^2)$ | Standard Partitioning Algorithm. |

---

## Step-by-Step Example: String ending with 'ab' over $\Sigma = \{a, b\}$
- $Q = \{q_0, q_a, q_{ab}\}$
- $\Sigma = \{a, b\}$
- $q_0$: Initial state (no characters seen)
- $q_a$: Last character seen was 'a'
- $q_{ab}$: Last characters seen were 'ab' (Accept state)

**Transitions**:
- $\delta(q_0, a) = q_a, \delta(q_0, b) = q_0$
- $\delta(q_a, a) = q_a, \delta(q_a, b) = q_{ab}$
- $\delta(q_{ab}, a) = q_a, \delta(q_{ab}, b) = q_0$

---

## Memory Hook: Pro-Tips for GATE
- **Complete Transition Table**: In GATE, ensure you check if every state has a transition for every symbol in $\Sigma$. If not, it's not a valid DFA.
- **The "Ends With" Rule**: For any string of length $n$ as a suffix, the minimal DFA will always have $n+1$ states.
- **The "Divisible By" Rule**: For a DFA to accept binary numbers divisible by $k$, it will have $k$ states representing the remainders $\{0, 1, \dots, k-1\}$.
