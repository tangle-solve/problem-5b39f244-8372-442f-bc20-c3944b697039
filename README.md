<!-- solve-problem:5b39f244-8372-442f-bc20-c3944b697039 -->
# Optimal explicit restricted-isometry matrices

A [Tangle Solve problem](https://solve.tangle.tools/problems/5b39f244-8372-442f-bc20-c3944b697039).

## What is the problem?

Construct, deterministically and in time polynomial in the output size, an explicit \(m\times N\) real matrix \(\Phi\) satisfying the restricted isometry property (RIP) of order \(k\) with constant \(\delta\) — i.e., for every \(k\)-sparse vector \(x\in\mathbb{R}^N\),
\[
(1-\delta)\|x\|_2^2 \le \|\Phi x\|_2^2 \le (1+\delta)\|x\|_2^2
\]
(after normalizing columns to unit \(\ell_2\) norm) — with number of rows
\[
m = O(k\log(N/k)),
\]
for general \(N\), \(k\), and fixed \(\delta\in(0,1)\) (say \(\delta = 0.1\)). "Explicit" means a deterministic algorithm outputs the matrix in poly\((mN)\) time; randomness is allowed only inside the algorithm's analysis if the object itself is deterministic (a fully explicit algebraic description is even better). The precise targets:

- **Upper bound (construction):** deterministic poly-time family with \(m \le C\cdot k\log(N/k)\) for universal constant \(C=C(\delta)\).
- **Lower bound:** prove no explicit construction can do better (matching lower bounds for explicit/finitely-listable constructions are open; the information-theoretic optimum is \(\Theta(k\log(N/k))\), so random is optimal up to constants).

## Why does it matter?

RIP matrices are the workhorse guarantee for compressed sensing: they certify that \(\ell_1\)-minimization (Basis Pursuit) stably recovers any \(k\)-sparse signal from \(m\) linear measurements. All near-optimal instantiations currently use *random* matrices, so recovery guarantees are probabilistic and matrices cannot be verified or reused with certainty. An explicit construction would derandomize compressed sensing, connect to explicit codes and extractors (an RIP matrix of order \(k\) essentially yields good lossless condensers), and represent a major success for derandomization beyond combinatorial objects.

## What's already known?

- **Random is optimal:** Gaussian or random \(\pm1\) matrices satisfy RIP with \(m = O(k\log(N/k))\) with high probability (Candès–Romberg–Tao; Rudelson–Vershynin).
- **Explicit barriers:** the Welch/sqrt bound gives \(N \le m^2\) (up to constants) for RIP matrices of order \(k\gtrsim \log N\); hence the "square-root bottleneck."
- **Bourgain–Dilworth–Ford–Konyagin–Kutzarova (2011):** first explicit construction breaking the \(N\le m^2\) barrier, achieving \(m = O(k^{2-\epsilon(k)})\log^2 N\) — order \(k^{2-\epsilon}\) rows for a small \(\epsilon(k)>0\) — via additive combinatorics (Bourgain systems of sets).
- **Mixon (2014):** survey + refinement showing the BDFKK analysis actually yields \(m = O(k^{2-\epsilon(k)})\,\mathrm{poly}\log N\); bottleneck persists.
- **Connection:** good RIP matrices imply good lossless condensers (and extractors via related arguments); known explicit extractor constructions yield RIP with \(m = k \cdot 2^{O(\log\log^c N)}\) rows (various works; verify exact parameters). All known explicit constructions have \(m\) polynomially or quasi-polynomially worse than \(k\log(N/k)\).
- Hardness: proving NP-hardness to certify RIP is known for *verifying* the property, but no evidence rules out explicit constructions at the optimal scale.

## What would count as solving it?

1. **Full solve:** a deterministic algorithm running in poly\((mN)\) time outputting an order-\(k\) RIP matrix with fixed \(\delta\) and \(m \le C(\delta)\,k\log(N/k)\), for all \(N, k\) — plus a proof of the RIP property.
2. **Partial results of interest:** (a) explicit \(m = O(k^{1+\epsilon}\log N)\) for any fixed \(\epsilon>0\); (b) explicit \(m = k\,\mathrm{polylog}(N)\) (removing exponential-in-loglog losses); (c) a lower bound showing any *explicit* (or finitely descriptive) RIP family requires \(\omega(k\log(N/k))\) rows — this would be a striking "hardness of derandomization" theorem.
3. A referee would demand: rigorous RIP proof, explicit polynomial-time construction procedure (not merely existence), and clear parameter statement \((N,k,\delta)\mapsto m\).

## How to start

1. Read Mixon's arXiv:1403.3427 survey first — it cleanly states the sqrt-bottleneck, the Welch bound, and the BDFKK construction; then read the Bourgain et al. 2011 paper for the additive-combinatorics machinery.
2. Learn the RIP–pseudorandomness dictionary: RIP of order \(k\) with small \(m\) corresponds to strong lossless condensers (see e.g. work connecting extractors and RIP; verify). Then ask: do modern explicit condensers/extractors (Guruswami–Umans–Vadhan, etc.) already give \(k\,\mathrm{polylog}(N)\)? If not, identify the exact quantitative gap.
3. Main obstacle: the Welch bound forces either \(N\le m^2\) or small \(k\); beating it requires coherence-based techniques to fail, i.e., second-order/cumulants analysis (as in BDFKK). Any \(O(k\log N)\) construction must control all \(k\)-subsets' spectra using global structure, not pairwise coherence.
4. Consider studying *hardness of certifying RIP* (complexity of RIP verification) as an alternative angle — lower-bound evidence is itself publishable.

## Key references

- J. Bourgain, S. Dilworth, K. Ford, S. Konyagin, D. Kutzarova, "Explicit constructions of RIP matrices and related problems," *Duke Math. J.* 159 (2011) 145–185. First explicit RIP construction breaking the \(N \le m^2\) bottleneck using additive combinatorics; achieves \(m \approx k^{2-\epsilon}\) up to log factors. https://arxiv.org/abs/1008.0471
- D. G. Mixon, "Explicit Matrices with the Restricted Isometry Property: Breaking the Square-Root Bottleneck," arXiv:1403.3427. Survey clarifying the sqrt-bottleneck and refining the BDFKK parameter analysis. https://arxiv.org/abs/1403.3427
- E. Candès, J. Romberg, T. Tao, "Stable signal recovery from incomplete and inaccurate measurements," *Comm. Pure Appl. Math.* 59 (2006) 1207–1223. Proves random measurements + \(\ell_1\) minimization recover sparse signals; source of the \(m\sim k\log(N/k)\) benchmark. https://arxiv.org/abs/math/0503066
- M. Rudelson, R. Vershynin, "Sparse reconstruction by convex relaxation: statistical and geometric limits," 2006. Sharp analysis of random RIP matrices via eigenvalues of random submatrices. (verify exact venue) https://arxiv.org/abs/math/0603141

## Warnings

- Do not confuse "explicit" with "verifiable": even given a random matrix, certifying RIP is believed computationally hard, so a solution must prove RIP analytically, not check it numerically.
- The Welch bound (\(N \le O(m^2)\) when \(k \ge c\log N\)) kills all coherence-based approaches at optimal \(m\); any attack must bypass pairwise coherence.
- Watch parameter regimes: results are often stated for \(k \le N^\alpha\); a general solution must handle all \(k\).
- The census line "explicit constructions have broken some older barriers" refers specifically to the \(N\le m^2\) barrier, not to the row count — no explicit construction is within a constant factor of \(k\log(N/k)\).

---
*`ALGO-000058` · unverified*

## Acceptance guidance

1. **Full solve:** a deterministic algorithm running in poly\((mN)\) time outputting an order-\(k\) RIP matrix with fixed \(\delta\) and \(m \le C(\delta)\,k\log(N/k)\), for all \(N, k\) — plus a proof of the RIP property.
2. **Partial results of interest:** (a) explicit \(m = O(k^{1+\epsilon}\log N)\) for any fixed \(\epsilon>0\); (b) explicit \(m = k\,\mathrm{polylog}(N)\) (removing exponential-in-loglog losses); (c) a lower bound showing any *explicit* (or finitely descriptive) RIP family requires \(\omega(k\log(N/k))\) rows — this would be a striking "hardness of derandomization" theorem.
3. A referee would demand: rigorous RIP proof, explicit polynomial-time construction procedure (not merely existence), and clear parameter statement \((N,k,\delta)\mapsto m\).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/5b39f244-8372-442f-bc20-c3944b697039?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000058.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000058)
