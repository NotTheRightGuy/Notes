# Boolean Algebra & Digital Logic Cheat Sheet (GATE)

## 1. Basic laws

|Law|AND form|OR form|
|---|---|---|
|Identity|A·1 = A|A + 0 = A|
|Null / Domination|A·0 = 0|A + 1 = 1|
|Idempotent|A·A = A|A + A = A|
|Complement|A·A' = 0|A + A' = 1|
|Involution|(A')' = A||
|Commutative|AB = BA|A + B = B + A|
|Associative|(AB)C = A(BC)|(A+B)+C = A+(B+C)|
|Distributive|A(B+C) = AB + AC|A + BC = (A+B)(A+C)|

## 2. Simplification theorems

- **Absorption:** A + AB = A, and A(A + B) = A
- **Redundancy:** A + A'B = A + B, and A(A' + B) = AB
- **Adjacency (combining):** AB + AB' = A, and (A+B)(A+B') = A
- **Consensus:** AB + A'C + BC = AB + A'C, and (A+B)(A'+C)(B+C) = (A+B)(A'+C)
- **Shannon expansion:** f = A·f(A=1) + A'·f(A=0)

## 3. De Morgan's laws

- (A + B)' = A'B'
- (AB)' = A' + B'
- Generalizes to n variables: (A₁ + A₂ + … + Aₙ)' = A₁'A₂'…Aₙ'

**Duality:** Swap · with + and 0 with 1. A function is **self-dual** if f = fᵈ.

## 4. XOR / XNOR

- A⊕B = AB' + A'B, and A⊙B = AB + A'B' = (A⊕B)'
- A⊕0 = A, A⊕1 = A', A⊕A = 0, A⊕A' = 1
- A⊕B = A'⊕B', and (A⊕B)' = A'⊕B = A⊕B'
- Commutative and associative. A(B⊕C) = AB⊕AC
- **n-input XOR = 1 when the number of 1s is odd.** n-input XNOR = 1 when the number of 1s is even (for even n).
- A + B = A⊕B⊕AB

## 5. Gates and functional completeness

- **Universal gates:** NAND and NOR.
- **Functionally complete sets:** {AND, NOT}, {OR, NOT}, {NAND}, {NOR}.
- NOT from NAND: tie inputs together, since (A·A)' = A'.
- NAND/NOR are commutative but **not associative**.
- XOR and XNOR alone are **not** functionally complete.

## 6. Counting results

- Number of minterms (or maxterms) of n variables = 2ⁿ
- Number of distinct Boolean functions of n variables = **2^(2ⁿ)**
- Number of self-dual functions of n variables = **2^(2^(n−1))**
- Minterm mᵢ = product term where each variable appears once. Maxterm Mᵢ = sum term, with Mᵢ = (mᵢ)'.
- f = Σm(…) = ΠM(rest), and f' swaps the minterm and maxterm lists.

## 7. K-map rules

- Group sizes must be powers of 2 (1, 2, 4, 8, …), and groups can wrap around edges.
- A group of 2ᵏ cells eliminates k variables.
- Use the largest groups and the fewest groups. Overlap is allowed.
- **Don't-cares (X)** can be used as 1 only if they help enlarge a group.
- **Essential prime implicant:** covers at least one 1 that no other prime implicant covers.
- For SOP, group the 1s. For POS, group the 0s and complement the variables.
- **Static-1 hazard** in SOP is removed by adding the consensus (redundant) term.

## 8. Combinational circuits

|Circuit|Equations|
|---|---|
|Half adder|S = A⊕B, C = AB|
|Full adder|S = A⊕B⊕Cin, Cout = AB + Cin(A⊕B)|
|Half subtractor|D = A⊕B, Borrow = A'B|
|Full subtractor|D = A⊕B⊕Bin, Bout = A'B + (A⊙B)Bin|

- A full adder = 2 half adders + 1 OR gate.
- **Ripple carry adder:** n full adders, with delay proportional to n.
- **Carry lookahead:** Generate Gᵢ = AᵢBᵢ, Propagate Pᵢ = Aᵢ⊕Bᵢ, Cᵢ₊₁ = Gᵢ + PᵢCᵢ.
- **Decoder:** n inputs give 2ⁿ outputs, with each output a minterm.
- **Encoder:** 2ⁿ inputs give n outputs.
- **MUX 2ⁿ:1:** n select lines. Any k-variable function can be built with a 2^(k−1):1 MUX.
- **Demux:** 1 input, n select lines, 2ⁿ outputs.
- An n-to-2ⁿ decoder with an OR gate can implement any function (as sum of minterms).
- A 2ⁿ:1 MUX can be built from smaller MUXes. For example, a 16:1 MUX needs five 4:1 MUXes.

## 9. Sequential circuits

|Flip-flop|Characteristic equation|Notes|
|---|---|---|
|SR|Q⁺ = S + R'Q|SR = 0 (S=R=1 is invalid)|
|JK|Q⁺ = JQ' + K'Q|J=K=1 toggles|
|D|Q⁺ = D||
|T|Q⁺ = T⊕Q|T=1 toggles|

- JK with J=K=1 and a level-triggered clock causes **race-around**. Edge triggering or master-slave fixes it.
- **Ripple (async) counter:** n flip-flops give modulus 2ⁿ.
- **Ring counter:** n flip-flops give n states.
- **Johnson (twisted ring) counter:** n flip-flops give **2n** states.
- **Mod-N counter:** needs ⌈log₂N⌉ flip-flops.
- Max clock frequency: f_max = 1 / (t_clk-to-Q + t_comb + t_setup).
- Hold condition: t_clk-to-Q + t_comb(min) ≥ t_hold.

## 10. Number systems

- **n-bit unsigned:** 0 to 2ⁿ − 1
- **2's complement:** −2^(n−1) to 2^(n−1) − 1 (one zero)
- **1's complement / sign-magnitude:** −(2^(n−1) − 1) to +(2^(n−1) − 1) (two zeros)
- 2's complement of N = 2ⁿ − N = (1's complement) + 1
- **Overflow in signed addition:** carry into MSB ≠ carry out of MSB (equivalently, two operands of the same sign give a result of the opposite sign).
- **Gray code:** G = B ⊕ (B >> 1). Binary from Gray: Bᵢ = Bᵢ₊₁ ⊕ Gᵢ.
- **BCD** uses 4 bits per digit (0–9). **Excess-3** = BCD + 3.
- Base conversion: an octal digit = 3 bits, a hex digit = 4 bits.

## 11. IEEE 754

|Format|Sign|Exponent|Mantissa|Bias|
|---|---|---|---|---|
|Single (32-bit)|1|8|23|127|
|Double (64-bit)|1|11|52|1023|

Value = (−1)^s × 1.M × 2^(E − bias) for normalized numbers.

## Quick tips for GATE

- Always try **absorption, redundancy and consensus** before reaching for a K-map.
- When you see XOR in an expression, expand it as AB' + A'B, then simplify.
- For equivalence questions, plug in a few input combinations rather than simplifying fully.
- Remember that "number of functions" formulas use **2^(2ⁿ)**, not 2ⁿ.