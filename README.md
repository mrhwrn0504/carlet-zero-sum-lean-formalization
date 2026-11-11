# Carlet zero-sum subspaces — Lean 4 formalization

This is the **separate open-source release** of the machine-checked Carlet zero-sum subspace theorem, along with its Lean 4 source code, reproducibility scripts and bilingual mathematical papers (Chinese and English).

**Author:** Wang Quanzhi (王泉智) · **Toolchain:** Lean 4.33.0

## Statements / 定理

For a characteristic-two finite field (K) of cardinality (2^n), the formalization constructs a (k)-dimensional (mathbb F_2)-linear subspace (Esubseteq K) with

[
sum_{xin Esetminus{0}}x^{-1}=0
]

in the parity-sensitive ranges:

- Odd (n): (3le kle n-3).
- Even (n): (2le kle n-2).

The principal definitions and theorems are in `formalization/Carlet/Statement.lean`, `MainTheorem.lean`, `EvenDegree.lean` and `FullTheorem.lean`.

## Verified source snapshot

The implementation is imported from the exact audited commit
[`bd491a4a644f3f3da300658eb3da1cb6c7a6d62a`](https://github.com/mrhwrn0504/carlet-conjecture-proof-candidate/commit/bd491a4a644f3f3da300658eb3da1cb6c7a6d62a).
The original snapshot passed **both** GitHub Actions verifications:

- [Push CI run #42925672368](https://github.com/mrhwrn0504/carlet-conjecture-proof-candidate/actions/runs/42925672368)
- [Pull request CI run #42925679186](https://github.com/mrhwrn0504/carlet-conjecture-proof-candidate/actions/runs/42925679186)

Those runs compiled **188 AINTLIB modules and 274 Carlet modules**, audited **942 printed declarations**, verified source/OLean SHA-256 hashes, reported **zero Lean compiler warnings**, found no `sorryAx` dependency, and independently re-elaborated the final theorems. The theorem axiom dependencies are limited to `propext`, `Classical.choice` and `Quot.sound`.

This repository runs its **own clean CI**. Do not confuse the original snapshot's success with successful independent verification of a new release until this repository's workflow is green.

## Reproducibility / 复现

The complete pipeline is defined in `.github/workflows/full-carlet-theorem.yml`. With Lean 4.33.0, pinned mathlib, and the included vendored AINTLIB sources configured:

```bash
cd formalization
python3 -I build.py
python3 -I verify_build.py
python3 -I audit_final_theorem.py
```

The build reports are uploaded as GitHub Actions artifacts.

## Papers / 中英文论文

The editable papers and PDFs are in `paper/lean-formalization/`. They describe the verified energy-contraction and norm-one routes, **not** the separate, unfinished high-dimensional reciprocal-geometry/cohomology proof program.

## Prior work and scholarly attribution

Kaimin Cheng, *Counting zero-sum subspaces for the multiplicative inverse function*, [arXiv:2610.06445](https://arxiv.org/abs/2610.06445) (October 2026) already proved Carlet's existence conjecture and a quantitative counting result. The original existence theorem is **not claimed as a first proof here**. This repository's scope is the Lean formalization, its explicit constructions and auditable machine verification.

The V7 direct-elimination and trace-criterion modules are included, but general existence of a V7 trace witness is **not** claimed to be separately formalized; this does not block the audited main theorem.

## Licenses

Original Lean code: MIT (`LICENSE`). Manuscript materials: CC BY 4.0 (`paper/LICENSE.md`). Bundled AINTLIB material retains its own Apache-2.0 notices. See `CITATION.cff` for citation metadata.

> The publication import will populate the source tree and papers. An empty project at this point does not yet constitute a published proof.
