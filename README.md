<!-- solve-problem:dcbc1079-19d3-4f2e-b1c2-8785472bc4d0 -->
# Polynomial-size explicit hitting sets for general circuits

A [Tangle Solve problem](https://solve.tangle.tools/problems/dcbc1079-19d3-4f2e-b1c2-8785472bc4d0).

## What is the problem?

Polynomial identity testing (PIT): given an arithmetic circuit C over a field F computing a polynomial f ∈ F[x₁,…,xₙ] of degree poly(s), where s is the circuit size, decide whether f ≡ 0. In the **black-box** model, we cannot inspect C; we may only evaluate it. A **hitting set** H ⊆ Fⁿ (or over an extension field) is a set such that for every nonzero f computed by a size-s circuit, some point of H has f(a) ≠ 0. A random set of size poly(s) hits w.h.p. (Schwartz–Zippel). The problem: **construct, deterministically in poly(s) time, a hitting set of size poly(s) for the class of all arithmetic circuits of size s computing degree-poly(s) polynomials** (n is part of the input; H depends on s, n, degree, and the field). Equivalently, derandomize black-box PIT for general circuits. Assumptions to fix: field F should be large enough (or allow extension fields, as in the standard statement); typically F is a field of characteristic 0 or large characteristic with efficient arithmetic. Note the class is all poly-size circuits — no depth, multilinearity, or read-restriction — which is what makes the problem open.

## Why does it matters?

Black-box PIT derandomization would give deterministic identity testing wherever circuits are accessible only by evaluation — certified program verification, symbolic-numeric computation, and deterministic sampling in numerical analysis. It would also imply circuit lower bounds: by Heintz–Schnorr and the Kabanets–Impagliazzo framework, explicit polynomial-size hitting sets for general circuits yield explicit functions requiring large arithmetic circuits (exponential lower bounds for related models). It is one of the central derandomization goals of algebraic complexity, alongside VP ⊊ VNP-type questions.

## What's already known?

- **Generic hitting sets exist nonconstructively**: Heintz and Schnorr (1980) showed hitting sets of size poly(s) exist for size-s circuits, and any such set, viewed as truth tables, yields hard polynomials — but their construction is probabilistic/existential, not explicit.
- **White-box PIT remains open too** for general circuits; even white-box derandomization is unknown. The black-box problem is strictly harder.
- **Positive results for restricted classes**: poly-time hitting sets / deterministic PIT are known for depth-3 (read-once and bounded-depth variants), depth-4 powering/read-once formulas, sparse polynomials, set-multilinear models, commuting/read-once branching programs, etc. See the Shpilka–Yehudayoff (2010) survey for the landscape to that date; Forbes–Saptharishi–Shpilka and later work pushed to depth-4 and beyond (verify exact attributions).
- **Hardness-to-hitting-set connections**: Kabanets–Impagliazzo (2004, Boolean analogue) and agrawall et al. in the arithmetic setting show that lower bounds (e.g., for NEXP or permanent-type polynomials) would give derandomization; conversely derandomization gives lower bounds.
- **Hu–van Melkebeek–Morgan (2024)**: recent work on the interplay between hitting sets and circuit lower bounds (verify precise statement before relying on it).

Why approaches fall short: universal hitting-set generators reduce PIT to computing a "hard" polynomial (the generator's component functions); no explicit polynomial with the required hardness (roughly exponential arithmetic circuit lower bounds for an explicit family) is known. All restricted-class techniques (rank arguments, shifted derivative, partial derivatives) exploit structure absent in the general model.

## What would count as solving it?

Solved (fully) by: **a deterministic algorithm that, on input (n, s, d) in unary, outputs in poly(n,s,d) time a set H ⊆ F̄ⁿ (or Fⁿ after extension) of size poly(n,s,d) that provably hits every nonzero polynomial computed by some arithmetic circuit of size s and degree ≤ d** — with a proof of correctness over the stated field class.

Partial/variant results that also count as major progress:
1. A hitting set of size poly(s) computable in subexponential time (quasi-polynomial would be a breakthrough, since even 2^{polylog s} is unknown for general circuits).
2. A conditional result: an explicit hitting set of polynomial size from a well-stated, plausible lower-bound assumption, made tight both directions.
3. Negative/barrier results are less central but a proof that black-box PIT requires superpolynomial hitting sets (impossible by Heintz–Schnorr existence — so this direction is closed; do not pursue).

## How to start

1. **Read Shpilka–Yehudayoff (2010), "Arithmetic Circuits: A Survey of Recent Results and Open Questions,"** Section on PIT, to absorb the known restricted-model toolkit (generators, rank methods).
2. **Read Heintz–Schnorr (1980)** to understand the generator construction: hitting sets correspond to a low-dimensional variety parametrization, and the size bound comes from counting; the missing piece is *explicitness*.
3. **Study the hardness-to-derandomization framework** (Kabanets–Impagliazzo 2004 for the Boolean case; its arithmetic analogues) to see exactly which lower bound suffices — this tells you the target hardness: roughly, an explicit polynomial family requiring 2^{Ω(n)}-size circuits with usable uniformity.
4. Natural attack: design a pseudorandom generator G: F^t → F^n with t = O(log s) whose components are explicit and hard; the obstacle is that all known explicit polynomials have only mild (quadratic-ish) lower bounds. Consider intermediate targets: hitting sets for depth-d circuits for growing d, or bootstrapping results that lift weak hitting sets upward (verify recent "bootstrapping" literature, e.g., Dvir et al.).

## Key references

- **Heintz, J., Schnorr, C.-P. (1980), "Testing Polynomials Which Are Easy to Compute," STOC 1980 (also L'Enseignement Mathématique 1982).** Proves existential poly-size hitting sets for small circuits and initiates the connection between hitting sets and circuit lower bounds. (verify venue details)
- **Shpilka, A., Yehudayoff, A. (2010), "Arithmetic Circuits: A Survey of Recent Results and Open Questions," Foundations and Trends in Theoretical Computer Science.** Comprehensive survey of arithmetic circuit lower bounds and PIT up to 2010, including the black-box PIT problem and generator framework. https://dx.doi.org/10.1561/0400000039
- **Hu, Y., van Melkebeek, D., Morgan, A. (2024).** Recent work relating hitting sets, derandomization, and arithmetic circuit lower bounds (verify exact title/statement before use).
- **Kabanets, V., Impagliazzo, R. (2004), "Derandomizing Polynomial Identity Tests Means Proving Circuit Lower Bounds," STOC 2003 / Computational Complexity 2004.** Establishes the equivalence (in the Boolean setting) between PIT derandomization and circuit lower bounds; the arithmetic analogue guides hardness targets. https://dx.doi.org/10.1145/780542.780595

## Warnings

- **White-box vs black-box**: even white-box PIT for general circuits is open; don't accidentally claim a black-box result from a white-box technique.
- **Small fields**: over finite fields, hitting sets may need to live in extension fields; specify the field model up front.
- **Heintz–Schnorr is existential**: their hitting sets exist but are not efficiently constructible; citing it as a "solution" is a classic error.
- **Restricted-model results do not compose**: PIT for depth-4 is not known to imply PIT for general circuits; be wary of "depth-4 suffices" claims — that reduction (for lower bounds, Gupta–Kamath–Kayal–Saptharishi) works in the lower-bound direction, not directly for hitting sets.
- The 2026 source record is machine-generated (verify); treat the Hu–van Melkebeek–Morgan citation with caution.

---
*`ALGO-000045` · unverified*

## Acceptance guidance

Solved (fully) by: **a deterministic algorithm that, on input (n, s, d) in unary, outputs in poly(n,s,d) time a set H ⊆ F̄ⁿ (or Fⁿ after extension) of size poly(n,s,d) that provably hits every nonzero polynomial computed by some arithmetic circuit of size s and degree ≤ d** — with a proof of correctness over the stated field class.

Partial/variant results that also count as major progress:
1. A hitting set of size poly(s) computable in subexponential time (quasi-polynomial would be a breakthrough, since even 2^{polylog s} is unknown for general circuits).
2. A conditional result: an explicit hitting set of polynomial size from a well-stated, plausible lower-bound assumption, made tight both directions.
3. Negative/barrier results are less central but a proof that black-box PIT requires superpolynomial hitting sets (impossible by Heintz–Schnorr existence — so this direction is closed; do not pursue).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/dcbc1079-19d3-4f2e-b1c2-8785472bc4d0?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000045.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000045)
