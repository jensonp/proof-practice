# 11. Language and String Facts over Σ\*

## Background

Before writing proofs about languages and Turing machines, you need the objects to be fully concrete.

- An **alphabet** Σ is any finite nonempty set of symbols. Example: Σ = `{0, 1}`.
- A **string** over Σ is a finite sequence of symbols from Σ. The **empty string** ε has length zero.
- Σ\* denotes the set of **all** finite strings over Σ, including ε.
- A **language** over Σ is any subset `L ⊆ Σ*`.

Proofs about languages are just set proofs (see `02-set-membership`) applied to subsets of Σ*. The only new element is that "elements" are now strings, not numbers.

---

## The Technique

All techniques from steps 1–10 apply directly. The most common patterns:

- To prove `L₁ ⊆ L₂`: take arbitrary string `w`, assume `w ∈ L₁`, derive `w ∈ L₂`.
- To prove `L₁ = L₂`: prove both `L₁ ⊆ L₂` and `L₂ ⊆ L₁`.
- To prove `L` is infinite: construct infinitely many distinct strings in `L`, or use contradiction.

---

## Key Definitions

- The **concatenation** of strings `x` and `y` is written `xy`. Its length is `|xy| = |x| + |y|`.
- The **reverse** of `w = a₁a₂...aₙ` is `wᴿ = aₙ...a₂a₁`.
- `Lᴿ = { wᴿ : w ∈ L }` is the **reverse language**.
- `L₁ · L₂ = { xy : x ∈ L₁, y ∈ L₂ }` is the **concatenation** of two languages.
- `L* = { w₁w₂...wₖ : k ≥ 0, each wᵢ ∈ L }` is the **Kleene star**. Note: ε ∈ L* always.

---

## Example Proofs

### Claim: For any language `L`, `ε ∈ L*`.

**Proof:**
By definition, `L* = { w₁w₂...wₖ : k ≥ 0, each wᵢ ∈ L }`.

Take `k = 0`. The concatenation of zero strings is the empty string `ε`. Since `k = 0` is a valid choice, `ε ∈ L*`. □

---

### Claim: If `L₁ ⊆ L₂`, then `L₁* ⊆ L₂*`.

**Proof:**
Assume `L₁ ⊆ L₂`. Let `w` be an arbitrary string and assume `w ∈ L₁*`.

By definition of Kleene star, `w = w₁w₂...wₖ` for some `k ≥ 0` where each `wᵢ ∈ L₁`.

Since `L₁ ⊆ L₂`, each `wᵢ ∈ L₂`.

Therefore `w = w₁w₂...wₖ` is a concatenation of strings from `L₂`, so `w ∈ L₂*` by definition.

Since `w` was arbitrary, `L₁* ⊆ L₂*`. □

---

### Claim: The language `L = { 0ⁿ : n ≥ 0 }` is infinite.

**Proof:**
For each `n ≥ 0`, let `wₙ` denote the string consisting of exactly `n` copies of `0`. Then `wₙ ∈ L` for all `n ≥ 0`.

If `n ≠ m`, then `|wₙ| = n ≠ m = |wₘ|`, so `wₙ ≠ wₘ`. Therefore the strings `w₀, w₁, w₂, ...` are pairwise distinct and all belong to `L`.

Since `L` contains infinitely many distinct elements, `L` is infinite. □

---

## What to Notice

- Proofs about languages are still set proofs. The variable `w` plays the role of `x` from step 2.
- We proved infiniteness by **constructing an infinite family of distinct witnesses** — combining steps 9 and 10.
- Length is a useful tool: two strings of different lengths are always different.

---

## Practice Problems

1. Prove: for any language `L`, `L ⊆ L*`.
2. Prove: `(L*)* = L*` for any language `L`.
3. Let `L = { w ∈ {0,1}* : w contains an equal number of 0s and 1s }`. Prove that `L` is infinite.
