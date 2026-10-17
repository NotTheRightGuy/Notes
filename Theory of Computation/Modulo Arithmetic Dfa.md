---
study_order: 3
title: Modulo Arithmetic DFA (Residue/Remainder Machine)
subject: Theory of Computation
tags:
  - #TheoryOfComputation
  - #DFA
  - #GATE_Preparation
status: to-review
---

# Modulo Arithmetic DFA (Residue/Remainder Machine)

**Context**: [[Theory Of Computation Index]] | [[DFA]] | [[DFA Minimization]]

---

## 1. Definition
A **Modulo Arithmetic DFA** (also known as a Residue or Remainder DFA) is a specialized [[DFA]] designed to determine the remainder of a number $N$ when divided by a constant $n$. This is a classic [[Gate]] topic where numbers are typically represented as strings in some base $b$ (usually binary, $b=2$, or decimal, $b=10$).

The DFA "computes" the remainder as it reads digits from left to right (Most Significant Digit to Least Significant Digit).

## 2. Construction Principle: Why $n$ States?
For a DFA to compute $(N \mod n)$, it must remember the remainder of the prefix processed so far.
- In any division by $n$, the possible remainders are $\{0, 1, 2, \dots, n-1\}$.
- Each remainder maps to a unique state in the DFA.
- Thus, a "Mod $n$" machine always has exactly **$n$ states**: $Q = \{q_0, q_1, \dots, q_{n-1}\}$.
- **State Interpretation**: If the DFA is in state $q_i$ after reading a string $w$, it means the integer value represented by $w \equiv i \pmod n$.

## 3. The Transition Rule (The "Why")
If we have a number $N$ and we append a new digit $d$ in base $b$, the new value $N'$ becomes:
$$N' = N \times b + d$$

To find the new remainder:
$$(N \times b + d) \mod n = [(N \mod n) \times b + d] \mod n$$

This gives us the **Transition Function**:
$$\delta(q_i, d) = q_{(i \times b + d) \mod n}$$
Where:
- $q_i$ is the current state (current remainder).
- $b$ is the base of the input (e.g., $2$ for binary).
- $d$ is the input digit ($0 \le d < b$).

## 4. Example: Binary Strings Divisible by 3 (Mod 3)
**Objective**: Construct a DFA for $L = \{w \in \{0, 1\}^* \mid \text{value}(w) \mod 3 = 0 \}$.

- **States**: $q_0$ (rem 0), $q_1$ (rem 1), $q_2$ (rem 2).
- **Base ($b$)**: 2 (Binary).
- **Start State**: $q_0$ (Empty string or leading zeros $\equiv 0 \pmod 3$).
- **Final State**: $q_0$ (Since we want divisibility, i.e., remainder 0).

### Transition Calculations:
1. **From $q_0$ (Rem 0)**:
   - Input `0`: $(0 \times 2 + 0) \mod 3 = 0 \to q_0$
   - Input `1`: $(0 \times 2 + 1) \mod 3 = 1 \to q_1$
2. **From $q_1$ (Rem 1)**:
   - Input `0`: $(1 \times 2 + 0) \mod 3 = 2 \to q_2$
   - Input `1`: $(1 \times 2 + 1) \mod 3 = 3 \mod 3 = 0 \to q_0$
3. **From $q_2$ (Rem 2)**:
   - Input `0`: $(2 \times 2 + 0) \mod 3 = 4 \mod 3 = 1 \to q_1$
   - Input `1`: $(2 \times 2 + 1) \mod 3 = 5 \mod 3 = 2 \to q_2$

### State Transition Table:
| Current Remainder | Input `0` | Input `1` |
| :--- | :--- | :--- |
| **$\rightarrow * q_0$ (0)** | $q_0$ | $q_1$ |
| **$q_1$ (1)** | $q_2$ | $q_0$ |
| **$q_2$ (2)** | $q_1$ | $q_2$ |

---

## 5. Visual Representation (Flowchart Logic)
Imagine the states arranged in a circle or a line. The transitions act as "shifts and adds" in the modulo space. 
- For "Divisible by $n$ in Binary", state $q_0$ always has a self-loop on `0` and goes to $q_1$ on `1`.
- The pattern often reflects the binary properties of the divisor.

---

## 6. Edge Cases & Complexity
- **Leading Zeros**: Modulo DFAs naturally handle leading zeros correctly because $0 \times b + 0 = 0$.
- **Empty String ($\epsilon$)**: Usually, the empty string is considered to have a value of 0, so it is accepted by $q_0$.
- **Non-prime Divisors**: If $n$ is not prime, the DFA might still be minimal with $n$ states, but some patterns might differ.

---

## 7. Memory Hook & GATE Pro-Tips 
- **The $N$-State Rule**: For any "Divisible by $n$" problem, the minimal DFA will have exactly $n$ states **IF** the base $b$ and $n$ are relatively prime (Coprime). If they share factors, minimization might (rarely) reduce it, but for $n=3, b=2$ (GATE favorite), it's always $n$ states.
- **Start/Final Logic**: For divisibility, $q_0$ is both start and final. For "remainder is $k$", $q_0$ is start and $q_k$ is final.
- **Reverse Strings**: If the question says "Binary number read from **Right to Left**", the construction is entirely different and much harder. The standard "Mod Machine" assumes **Left to Right** (MSD first).

---

## 8. Previous Year Question (Sample)
**Q**: Number of states in a minimal DFA accepting binary strings whose decimal equivalent is divisible by 5?
**A**: Following the "Mod $n$" rule, $n=5$. Since $\gcd(2, 5) = 1$, the DFA is minimal with **5 states**.
**Calculation**: $\delta(q_i, d) = (2i + d) \mod 5$.

---
**Related Concepts**: [[Finite Automata]], [[Equivalence Classes]], [[Regular Languages]].
