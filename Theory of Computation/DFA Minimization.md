---
study_order: 5
subject: Theory of Computation
topic: DFA Minimization
tags: [TheoryOfComputation, FiniteAutomata, GATE-CS, TOC]
status: to-review
last_modified: 2026-04-12
---

# Context
Parent Index: [[Theory Of Computation Index]]
Related Concepts: [[DFA]], [[Regular Languages]], [[Equivalence Classes]], [[Myhill-Nerode Theorem]]

---

# DFA Minimization (Partitioning Algorithm)

DFA Minimization is the process of finding the **Minimal DFA** that accepts the same [[Regular Languages]] as a given [[DFA]]. A minimal DFA is unique (up to isomorphism) for any regular language.

## The "Why" behind Minimization
In [[Theory Of Computation]], efficiency matters. A DFA might have redundant states that perform the same "functional" role. Minimization reduces the space complexity of the hardware or software implementation of the automaton. 

Logic: Two states $p$ and $q$ are **equivalent** ($p \equiv q$) if for every possible input string $w$, the transitions $\hat{\delta}(p, w)$ and $\hat{\delta}(q, w)$ both lead to either a Final state or a Non-Final state.

---

## The Step-by-Step Procedure

### 1. Eliminate Unreachable States
Before starting the partitioning, remove any state that cannot be reached from the **Start State** via any sequence of transitions.
- *Tip*: Use a Simple BFS/DFS from the start state to identify reachable nodes.

### 2. Initial Partition ($P_0$)
Divide the set of states $Q$ into two groups:
- Group 1 ($G_1$): All **Non-Final States** ($Q - F$)
- Group 2 ($G_2$): All **Final States** ($F$)
$$P_0 = \{ \{Q-F\}, \{F\} \}$$

### 3. Successive Refinement ($P_{k+1}$)
For each group in the current partition $P_k$, check if the states within it are "equivalent" under all input symbols $\Sigma$.
- Two states $A$ and $B$ in the same group stay together in $P_{k+1}$ if for every $a \in \Sigma$, $\delta(A, a)$ and $\delta(B, a)$ fall into the **same group** in the current partition $P_k$.
- If they transition to different groups, they must be split.

### 4. Termination
Repeat Step 3 until $P_{k+1} = P_k$. No further splitting is possible. Each remaining group represents a single state in the **Minimal DFA**.

---

## Complexity Table
| Metric | Complexity | Note |
| :--- | :--- | :--- |
| **Time Complexity** | $O(k \cdot n^2)$ | Where $n$ is states, $k$ is $|\Sigma|$. Optimized (Hopcroft) is $O(k \cdot n \log n)$. |
| **Space Complexity** | $O(n^2)$ | To store the transition table/partitions. |

---

## Detailed Step-by-Step Example

**Given DFA**:
- States: $\{q_0, q_1, q_2, q_3, q_4, q_5\}$
- $\Sigma = \{0, 1\}$
- Start: $q_0$
- Final: $\{q_2, q_3, q_4\}$
- Transitions:
  - $\delta(q_0, 0)=q_1, \delta(q_0, 1)=q_3$
  - $\delta(q_1, 0)=q_0, \delta(q_1, 1)=q_3$
  - $\delta(q_2, 0)=q_1, \delta(q_2, 1)=q_4$
  - $\delta(q_3, 0)=q_5, \delta(q_3, 1)=q_5$
  - $\delta(q_4, 0)=q_5, \delta(q_4, 1)=q_5$
  - $\delta(q_5, 0)=q_5, \delta(q_5, 1)=q_5$

**Execution**:
1. **$P_0$**: $\{q_0, q_1, q_5\}$ (Non-Final) and $\{q_2, q_3, q_4\}$ (Final).
2. **Refining Non-Final $\{q_0, q_1, q_5\}$**:
   - $q_0$ on 0 $\to q_1 \in G_{NF}$, on 1 $\to q_3 \in G_F$
   - $q_1$ on 0 $\to q_0 \in G_{NF}$, on 1 $\to q_3 \in G_F$
   - $q_5$ on 0 $\to q_5 \in G_{NF}$, on 1 $\to q_5 \in G_{NF}$
   - *Result*: $q_0, q_1$ behave similarly, but $q_5$ differs on input '1'. Split $q_5$.
   - **$P_1$**: $\{q_0, q_1\}, \{q_5\}, \{q_2, q_3, q_4\}$.
3. **Refining Final $\{q_2, q_3, q_4\}$**:
   - Check $q_3, q_4$: Both go to $\{q_5\}$ on 0 and 1. They stay together.
   - Check $q_2$: On 0 $\to q_1 \in \{q_0, q_1\}$, on 1 $\to q_4 \in \{q_2, q_3, q_4\}$.
   - *Result*: $q_2$ splits from $\{q_3, q_4\}$.
   - **$P_2$**: $\{q_0, q_1\}, \{q_5\}, \{q_2\}, \{q_3, q_4\}$.
4. Further checks show no more splits. **Minimal DFA has 4 states.**

---

## Memory Hook: Pro-Tips for GATE
- **The "Dead State" Trap**: A Dead State (trap state) is a valid state and **must be included** in the minimization process (it will usually end up in its own partition or merge with other identical trap states).
- **The Initial Split**: Never forget to split Final and Non-Final first. This is based on $0$-equivalence.
- **Myhill-Nerode**: Remember that the number of states in a minimal DFA equals the number of distinct **Equivalence Classes** of the Myhill-Nerode relation $\approx_L$.

---

## GATE Sample Question
**Q**: What is the minimum number of states in a DFA that recognizes the language $L = \{w \in \{0,1\}^* \mid w \text{ ends with } 011\}$?
**A**: For a string of length $n$, the minimal DFA for "ends with" usually has $n+1$ states. Here, $n=3$, so states = 4. 
*Constraint*: This only holds if the pattern doesn't have overlapping self-similarities that allow further reduction, but for "ends with" $n$ bits, $n+1$ is the standard answer.
