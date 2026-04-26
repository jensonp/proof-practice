# 17. Proving a Specific Problem is Undecidable via Reduction

## Background

Step 16 established the **template** for a reduction proof and the four properties every reduction must satisfy. Step 17 applies that template to a concrete, non-trivial target language.

The goal here is not just to mechanically fill in the template — it is to develop the skill of **designing** the right reduction function `f`. That design step is the creative core of undecidability proofs, and it follows a repeatable strategy:

> **Design principle:** Given a known-undecidable language `A` and a target language `B`, ask: "What does membership in `B` require? Can I encode membership in `A` as a question about `B`?"

The most common source language is `A_TM`. The most common encoding strategy is: construct a machine `M'` whose behavior on some canonical input encodes whether `M` accepts `w`.

---

## Worked Target: `REGULAR_TM`

This is one of the canonical examples from computability theory.

**Define:**
```
REGULAR_TM = { <M> : L(M) is a regular language }
```

This is the set of encodings of Turing machines whose accepted language happens to be regular. We will prove it is undecidable.

---

## Claim: `REGULAR_TM` is undecidable.

**Proof:** We show `A_TM ≤_m REGULAR_TM`.

---

### Step 1 — Design the Reduction

We need a computable function `f` such that:
```
<M, w> ∈ A_TM  ⟺  f(<M, w>) ∈ REGULAR_TM
```

That is: `f(<M, w>)` should be the encoding of some machine whose language is regular **exactly when** `M` accepts `w`.

**The key idea:** Build a machine `M'` whose language switches between two languages depending on whether `M` accepts `w`:
- If `M` accepts `w`: make `L(M') = Σ*` (all strings — a regular language).
- If `M` does not accept `w`: make `L(M') = { 0ⁿ1ⁿ : n ≥ 0 }` (a non-regular language).

This works because `Σ*` is regular and `{ 0ⁿ1ⁿ }` is not, so membership in `REGULAR_TM` tracks exactly whether `M` accepts `w`.

---

### Step 2 — Define `f`

**Define `f`:** On input `<M, w>`, output `<M'>` where `M'` is defined as follows:

> `M'` on input `x`:
> 1. If `x` is of the form `0ⁿ1ⁿ` for some `n ≥ 0`, **accept**.
> 2. Otherwise, run `M` on `w` (ignoring `x` from this point).
> 3. If `M` accepts `w`, **accept**.
> 4. If `M` rejects `w`, **reject**.

Note: `M'` always accepts strings of the form `0ⁿ1ⁿ`, and additionally accepts all other strings if `M` accepts `w`.

---

### Step 3 — Verify the Four Properties

**(1) Computability:**
The function `f` takes `<M, w>` and outputs the description of `M'`. The description of `M'` is a finite object that can be written down from `<M>` and `w` by a Turing machine that never runs `M` — it only reads `M`'s description and incorporates it into `M'`'s transition table. This construction always terminates. So `f` is computable. ✓

**(2) Totality:**
For every input string (well-formed or not), `f` produces a valid machine description `<M'>`. On malformed inputs, define `f` to output the description of a fixed machine that immediately rejects everything (whose language is ∅, which is regular — so it is not in `REGULAR_TM`, consistent with the No→No direction). `f` is total. ✓

**(3) Yes → Yes:** Assume `<M, w> ∈ A_TM`, i.e., `M` accepts `w`.

We must show `f(<M, w>) = <M'> ∈ REGULAR_TM`, i.e., `L(M')` is regular.

Claim: when `M` accepts `w`, `L(M') = Σ*`.

Proof of claim: Let `x` be any string.
- If `x = 0ⁿ1ⁿ`: `M'` accepts at step 1.
- If `x` is anything else: `M'` runs `M` on `w` at step 2. Since `M` accepts `w` (by assumption), `M'` accepts at step 3.

So `M'` accepts every string. Therefore `L(M') = Σ*`.

Since `Σ*` is regular (it is accepted by a one-state DFA that accepts on every symbol), `<M'> ∈ REGULAR_TM`. ✓

**(4) No → No:** Assume `<M, w> ∉ A_TM`, i.e., `M` does not accept `w`.

We must show `f(<M, w>) = <M'> ∉ REGULAR_TM`, i.e., `L(M')` is not regular.

Claim: when `M` does not accept `w`, `L(M') = { 0ⁿ1ⁿ : n ≥ 0 }`.

Proof of claim: Let `x` be any string.
- If `x = 0ⁿ1ⁿ`: `M'` accepts at step 1. So `0ⁿ1ⁿ ∈ L(M')`.
- If `x` is not of the form `0ⁿ1ⁿ`: `M'` skips step 1 and runs `M` on `w` at step 2. Since `M` does not accept `w` (by assumption), `M` either rejects or loops.
  - If `M` rejects `w`: `M'` reaches step 4 and rejects `x`.
  - If `M` loops on `w`: `M'` loops at step 2 and never accepts `x`.
  In either case, `x ∉ L(M')`.

So `L(M') = { 0ⁿ1ⁿ : n ≥ 0 }`.

By the pumping lemma for regular languages, `{ 0ⁿ1ⁿ : n ≥ 0 }` is not regular. Therefore `<M'> ∉ REGULAR_TM`. ✓

---

### Conclusion

All four properties hold. Therefore `A_TM ≤_m REGULAR_TM`.

Since `A_TM` is undecidable and `A_TM ≤_m REGULAR_TM`, `REGULAR_TM` is undecidable. □

---

## What to Notice

- **The machine `M'` never runs `M` on its own input `x`.** It runs `M` on the fixed string `w` that was baked in at reduction time. `x` only affects whether step 1 fires.
- **The language of `M'` switches based on whether `M` accepts `w`.** The two possible languages (`Σ*` and `{0ⁿ1ⁿ}`) were chosen deliberately: one is in `REGULAR_TM`, the other is not.
- **The No→No case needed two sub-cases** (reject vs. loop) for what `M` does on `w`. Both must be addressed.
- **We invoked the pumping lemma** as a prior result to justify that `{0ⁿ1ⁿ}` is not regular. In a full proof, you either cite this result or prove it inline.
- This proof structure — building `M'` with a "switch" based on whether `M` accepts `w` — appears in nearly every `A_TM`-reduction to a language property. Learn to recognize and reuse it.

---

## Rice's Theorem (Why This Pattern Generalizes)

The proof above is an instance of a much more powerful result:

> **Rice's Theorem:** Let `P` be any non-trivial property of Turing-recognizable languages (i.e., `P` is true for some TMs and false for others). Then `{ <M> : L(M) has property P }` is undecidable.

**Non-trivial** means: `P` is not always true and not always false. For example:
- `REGULAR_TM` — non-trivial ✓ (some TMs compute regular languages, some don't)
- `EMPTY_TM` — non-trivial ✓
- "L(M) is a language" — trivial ✗ (always true, so it's trivially decidable)

Rice's Theorem means you do not need to construct a custom reduction for every language property — they are **all** undecidable. The proof of Rice's Theorem is itself a reduction from `A_TM` using exactly the switch-machine technique from this step.

---

## Practice Problems

1. **`EMPTY_TM`.** Prove that `EMPTY_TM = { <M> : L(M) = ∅ }` is undecidable by reducing from `A_TM`. Define `f` explicitly and verify all four properties.
   - *Hint: construct `M'` so that `L(M') = ∅` when `M` does not accept `w`, and `L(M') = {w}` (or Σ*) when `M` does accept `w`.*

2. **`EQ_TM`.** Let `EQ_TM = { <M₁, M₂> : L(M₁) = L(M₂) }`. Prove `EQ_TM` is undecidable by reducing from `EMPTY_TM`.
   - *Hint: reduce by fixing one machine to always reject, and mapping `<M>` to `<M, M_reject>`.*

3. **Apply Rice's Theorem.** For each language below, state whether Rice's Theorem immediately implies it is undecidable. If yes, identify the language property `P` and confirm it is non-trivial. If no, explain why not.
   - (a) `{ <M> : M accepts the string "hello" }`
   - (b) `{ <M> : M has exactly 5 states }`
   - (c) `{ <M> : L(M) contains at least one palindrome }`
