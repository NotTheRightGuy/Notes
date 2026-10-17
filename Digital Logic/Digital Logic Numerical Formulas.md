---
tags:
  - GATE/CS
  - GATE/DigitalLogic
  - Formulas
aliases:
  - Digital Logic Formula Sheet
  - Numerical Formulas Digital Logic
date_created: 2026-10-17
difficulty: 3
last_revised: 2026-10-17
pyq_frequency: High
---

# Digital Logic: Numerical Formulas

Companion to [[Cheatsheet]] (Boolean laws). This note covers the counting and numeric formulas.

## 1. Number Systems

- Value of $(d_{n-1}\dots d_0 . d_{-1}\dots d_{-m})_r = \sum d_i\, r^i$
- Digits needed for $N$ values in base $r$: $\lceil \log_r N \rceil$. Bits for $N$ values: $\lceil \log_2 N \rceil$.
- Max unsigned value with $n$ bits: $2^n - 1$.
- Base conversion: bin to oct groups 3 bits; bin to hex groups 4 bits.
- BCD: 4 bits per decimal digit. Excess-3 = BCD + 3.
- Binary to Gray: $g_{n-1}=b_{n-1}$, $g_i = b_{i+1}\oplus b_i$. Gray to binary: $b_i = b_{i+1}\oplus g_i$. See [[Gray Code]].

## 2. Signed Number Representation ($n$ bits)

| Representation | Range | Zeros | Negation |
|---|---|---|---|
| Sign-magnitude | $-(2^{n-1}-1)$ to $2^{n-1}-1$ | 2 | flip sign bit |
| 1's complement | $-(2^{n-1}-1)$ to $2^{n-1}-1$ | 2 | flip all bits |
| 2's complement | $-2^{n-1}$ to $2^{n-1}-1$ | 1 | flip bits, add 1 |

- $r$'s complement of $N$ ($n$ digits): $r^n - N$. $(r-1)$'s complement: $r^n - 1 - N$.
- 2's complement value: $-b_{n-1}2^{n-1} + \sum_{i<n-1} b_i 2^i$.
- Sign extension keeps the value. Overflow in addition: carry into MSB $\ne$ carry out of MSB (equivalently, two operands of same sign give opposite-sign result).

## 3. Boolean Function Counting

- Functions of $n$ variables: $2^{2^n}$ (2 vars: 16, 3 vars: 256).
- Minterms/maxterms: $2^n$. Number of literals in a minterm: $n$.
- Number of true minterms $k$ gives $\binom{2^n}{k}$ functions with that count.
- Self-dual functions of $n$ variables: $2^{2^{n-1}}$.
- Symmetric functions of $n$ variables: $2^{n+1}$.
- Monotone (positive unate) functions: 2 vars = 6, 3 vars = 20 (Dedekind numbers).
- $f(\text{XOR of } n \text{ vars}) = 1$ for $2^{n-1}$ minterms. See [[XOR Gate]].
- $n$-input AND/OR/NAND/NOR needs $n-1$ two-input gates.
- Two-input gate equivalents: $n$-input XOR needs $n-1$ XORs.

## 4. K-Map and Minimization

- Cells $=2^n$. A group of $2^k$ cells eliminates $k$ variables, leaving $n-k$ literals.
- Max prime-implicant count for $n$ vars: $3^n/n$ (upper bound).
- Essential PIs must be in every minimal cover. See [[K-Map Minimization]], [[Implicants and Prime Implicants]].
- Worst-case SOP size (parity function): $2^{n-1}$ terms, each with $n$ literals.

## 5. Universal Gates

- NAND count to build: NOT = 1, AND = 2, OR = 3, XOR = 4, XNOR = 5.
- NOR count to build: NOT = 1, OR = 2, AND = 3, XOR = 5, XNOR = 4.
- Only NAND or NOR is functionally complete. See [[Universal Gates]], [[Functional Completeness]].

## 6. Adders and Subtractors

- Half adder: $S = A\oplus B$, $C = AB$. See [[Half Adder]].
- Full adder: $S = A\oplus B\oplus C_{in}$, $C_{out} = AB + C_{in}(A\oplus B)$.
- Full adder = 2 half adders + 1 OR. Full adder = 9 NAND gates; half adder = 5 NAND gates (4 for XOR, sharing the first NAND, plus 1 inverter-NAND for carry).
- Half subtractor: $D = A\oplus B$, $B_{out} = A'B$.
- Full subtractor: $D = A\oplus B\oplus B_{in}$, $B_{out} = A'B + (A\odot B)B_{in}$.
- Ripple carry adder delay (n bits): $\approx n\,t_{carry}$ (carry path) .
- Carry lookahead: $G_i = A_iB_i$, $P_i = A_i\oplus B_i$ (or $A_i+B_i$), $C_{i+1} = G_i + P_iC_i$. Delay is constant in $n$ for full lookahead.
- Gate delay of CLA: about 4 gate delays for sum.
- Adder-subtractor: XOR each $B_i$ with mode $M$, set $C_0=M$.
- BCD adder: add, if sum $>9$ or carry, add 6.

## 7. Comparators, Decoders, Encoders, MUX

- 1-bit comparator: $A>B = AB'$, $A=B = A\odot B$, $A<B = A'B$. See [[Magnitude Comparator]].
- $n$-bit equality: $\prod (A_i\odot B_i)$.
- Decoder $n\to 2^n$: $2^n$ AND gates of $n$ inputs. Enable input doubles as demux.
- Larger decoders from smaller ones: 4:16 from 2:4 needs 5 decoders; 3:8 from 2:4 needs 2 (using 2 with enable, plus a 1:2 for the MSB, i.e. 3 with a NOT).
- Encoder $2^n\to n$ ; priority encoder resolves multiple inputs.
- MUX $2^n\!:\!1$ has $n$ select lines. Can implement any $(n+1)$-variable function (with $n$ selects and inputs from $\{0,1,X,X'\}$). See [[Multiplexer]].
- Building $2^n:1$ from $2:1$ MUXes: $2^n - 1$. Building $4^k:1$ from $4:1$: $(4^k-1)/3$.
- MUX with $n$ selects, implement $n$-variable function: all data inputs tied to 0/1.
- Function from $m$-input decoder + OR: OR of selected minterm lines (use NAND on active low outputs).

## 8. Memory/ROM/PLA/PAL

- ROM size: $2^{n}\times m$ bits ($n$ address lines, $m$ outputs). Address lines $=\log_2(\text{words})$.
- ROM as lookup: any $m$ functions of $n$ variables.
- PLA: programmable AND and OR; products shared across outputs. PAL: programmable AND, fixed OR.
- PLA fuses $= 2n\cdot p + p\cdot m$ ($p$ product terms).

## 9. Sequential Circuits: Flip Flops

| FF | Characteristic | Excitation (Q to Q+) |
|---|---|---|
| SR | $Q^+ = S + R'Q$, $SR=0$ | 0to0: S=0,R=X; 0to1: S=1,R=0; 1to0: S=0,R=1; 1to1: S=X,R=0 |
| JK | $Q^+ = JQ' + K'Q$ | 0to0: J=0,K=X; 0to1: J=1,K=X; 1to0: J=X,K=1; 1to1: J=X,K=0 |
| D | $Q^+ = D$ | D = Q+ |
| T | $Q^+ = T\oplus Q$ | T = Q $\oplus$ Q+ |

See [[Flip Flops]], [[SR Flip Flop]], [[JK Flip Flop]], [[D Flip Flop]], [[T Flip Flop]], [[Master Slave Flip Flop]], [[Latches]].

- Conversion: $J=K=T$ turns JK into T; $J=D, K=D'$ turns JK into D; $D = T\oplus Q$ turns D into T.
- Timing constraint: $T_{clk} \ge t_{cq} + t_{comb} + t_{setup}$ (+ clock skew). Max frequency $f_{max} = 1/T_{clk}$.
- Hold constraint: $t_{cq} + t_{comb,min} \ge t_{hold} + t_{skew}$.
- Race-around occurs when $t_{pd} < T_{clk,high}$ for level-triggered JK with $J=K=1$. It is avoided when the clock pulse width is shorter than $t_{pd}$, or by using edge triggering or master-slave.

## 10. Counters

- $n$ flip flops give modulus up to $2^n$. FFs needed for MOD-$N$: $\lceil \log_2 N\rceil$.
- Ripple (async) counter delay: $n\cdot t_{pd}$. Max clock period: $T \ge n\,t_{pd} + t_{strobe}$ (so $f_{max} \le 1/(n\,t_{pd})$).
- Synchronous counter: $T\ge t_{pd,FF} + t_{pd,gate}$.
- Output frequency of MOD-$N$ counter: $f_{in}/N$. Each FF divides frequency by 2.
- Ring counter: $n$ FFs gives $n$ states (one-hot). Johnson (twisted ring): $n$ FFs gives $2n$ states.
- Unused states: Ring $2^n - n$; Johnson $2^n - 2n$.
- Johnson counter needs $n$ FFs, with decoding using 2-input gates only.
- Up/down counter: toggle condition $T_i = \prod_{j<i}Q_j$ (up) or $\prod_{j<i}Q_j'$ (down).
- Count sequence length with $k$ FFs in feedback shift register: max $2^k - 1$ (LFSR).
- Mod of cascaded counters: MOD-$M$ followed by MOD-$N$ gives MOD-$MN$.

## 11. Shift Registers

- $n$-bit serial in: $n$ clocks to load; parallel load: 1 clock.
- Shift left by one = multiply by 2; shift right = divide by 2 (arithmetic shift preserves sign).
- Serial adder: 1 FF for carry, $n$ clocks for $n$-bit add.

## 12. Fan-in/Fan-out and Timing

- Propagation delay $t_{pd} = (t_{PLH}+t_{PHL})/2$.
- Noise margin: $NM_H = V_{OH,min} - V_{IH,min}$, $NM_L = V_{IL,max} - V_{OL,max}$.
- Fan-out $=\min(I_{OH}/I_{IH},\; I_{OL}/I_{IL})$.
- Power dissipation: $P = P_{static} + P_{dynamic}$, $P_{dyn} = \alpha C V^2 f$.
- Critical path delay = longest delay over any input-output path; clock period $\ge$ that plus overheads.

## 13. Converters

- $n$-bit DAC resolution $= V_{ref}/2^n$ (or $V_{ref}/(2^n-1)$ full scale). Output $V_o = \text{code}\cdot \text{resolution}$.
- $n$-bit flash ADC needs $2^n - 1$ comparators. Counter-type ADC worst conversion time $2^n$ clocks. Successive approximation: $n$ clocks.
- Quantization step: $\Delta = V_{FS}/2^n$. Max quantization error $\pm \Delta/2$.

## 14. Quick Traps

- Number of functions of $n$ vars is $2^{2^n}$, not $2^n$.
- 2's complement range is asymmetric.
- Ripple counter has no common clock, so use $n\,t_{pd}$.
- Johnson counter has $2n$ states, ring has $n$.
- MUX $2^n:1$ implements $(n+1)$-variable functions with free inverter and constants.
- Full adder built from NAND is 9 gates.

## Links

[[Boolean Algebra]], [[Canonical and Standard Forms]], [[Combinational Circuit]], [[Duality and Complement of Boolean Functions]], [[XNOR Gate]], [[Cheatsheet]]
