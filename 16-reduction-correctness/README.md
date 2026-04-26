# 16. Reduction Correctness — Four Things to Verify

## Background

A **reduction** from language `A` to language `B` is a computable function `f : Σ* → Σ*` such that for every string `w`:

```
w ∈ A  ⟺  f(w) ∈ B
```

This is written `A ≤_m B` ("A is mapping-reducible to B").

Reductions are the primary tool for proving a language is undecidable or unrecognizable. The logic works like this:

- If `A ≤_m B` and `B` is decidable, then `A` is decidable.
- Equivalently (contrapositive): if `A ≤_m B` and `A` is **undecidable**, then `B` is **undecidable**.

So to prove `B` is undecidable, you take a known-undecidable language `A` (like `A_TM`), define a reduction `f` from `A` to `B`, and prove it is correct. The undecidability of `B` follows.

---

## The Four Things to Verify

Every reduction proof must verify exactly four properties of the function `f`. Missing any one makes the proof invalid.

| # | Property | What it means | How to prove it |
|---|---|---|---|
| 1 | **Computable** | `f` can be computed by a Turing machine that halts on all inputs | Describe the TM that computes `f` explicitly |
| 2 | **Total** | `f(w)` is defined for every `w ∈ Σ*` | Show the TM computing `f` halts on all inputs |
| 3 | **Yes → Yes** | If `w ∈ A`, then `f(w) ∈ B` | Assume `w ∈ A`; derive `f(w) ∈ B` |
| 4 | **No → No** | If `w ∉ A`, then `f(w) ∉ B` | Assume `w ∉ A`; derive `f(w) ∉ B` |

Properties 3 and 4 together establish the biconditional `w ∈ A ⟺ f(w) ∈ B`. Properties 1 and 2 together establish that `f` is a valid computable function.

> **Common mistake:** Many students prove Yes→Yes and No→No but forget to argue computability and totality. A reduction where `f` loops on some inputs is not a valid mapping reduction — it does not transfer decidability.

---

## The Technique

Reduction proof template:

```
Theorem: B is undecidable.
Proof: We show A_TM ≤_m B.

Define f as follows. On input w:
  [Describe what the TM computing f does on w]
  Output: [the string f(w)]

Verify the four properties:

(1) Computability: [argue the TM computing f halts on all inputs]
(2) Totality:      [confirm f(w) is defined for every w]
(3) Yes → Yes:     Assume w ∈ A_TM. Show f(w) ∈ B.
(4) No  → No:      Assume w ∉ A_TM. Show f(w) ∉ B.

Since A_TM ≤_m B and A_TM is undecidable, B is undecidable. □
```

---

## Example Proof

### Setup

Let:
- `A_TM = { ⟨M, w⟩ : M accepts w }` — known undecidable (step 15).
- `HALT = { ⟨M, w⟩ : M halts on w }` — we will show this is undecidable.

### Claim: `HALT` is undecidable.

**Proof:** We show `A_TM ≤_m HALT`.

**Define `f`:** On input `⟨M, w⟩` (treating any malformed input as a fixed string that is trivially not in HALT):

Construct and output the description `⟨M', w⟩` where `M'` is a new machine defined as:

> `M'` on input `x`:
> 1. Run `M` on `x`.
> 2. If `M` accepts, **accept**.
> 3. If `M` rejects, **loop forever**.

So `f(⟨M, w⟩) = ⟨M', w⟩`.

---

**Verify the four properties:**

**(1) Computability:**
`f` is computed by a Turing machine that, given `⟨M, w⟩`, constructs the description of `M'` (by writing the finite description of `M'`'s transitions based on `M`'s transitions) and outputs `⟨M', w⟩`. This construction is purely syntactic — it does not run `M`. The TM computing `f` always halts after writing the output. So `f` is computable. □

**(2) Totality:**
The construction above outputs a valid string `⟨M', w⟩` for every input `⟨M, w⟩`. Even on malformed inputs, we can define `f` to output a fixed string like `⟨M_reject, ε⟩` (a machine that immediately rejects) which is not in HALT. So `f` is total. □

**(3) Yes → Yes:** Assume `⟨M, w⟩ ∈ A_TM`, i.e., `M` accepts `w`.

We need to show `f(⟨M, w⟩) = ⟨M', w⟩ ∈ HALT`, i.e., `M'` halts on `w`.

By assumption, `M` accepts `w`. By the construction of `M'`: `M'` runs `M` on `w`; since `M` accepts `w`, `M'` reaches step 2 and accepts. Accepting is a halting state. Therefore `M'` halts on `w`, so `⟨M', w⟩ ∈ HALT`. □

**(4) No → No:** Assume `⟨M, w⟩ ∉ A_TM`, i.e., `M` does not accept `w`.

We need to show `f(⟨M, w⟩) = ⟨M', w⟩ ∉ HALT`, i.e., `M'` does not halt on `w`.

Since `M` does not accept `w`, either:
- `M` rejects `w`: then `M'` reaches step 3 and loops forever. `M'` does not halt.
- `M` loops on `w`: then `M'` loops at step 1. `M'` does not halt.

In both cases, `M'` does not halt on `w`, so `⟨M', w⟩ ∉ HALT`. □

---

Since all four properties hold, `A_TM ≤_m HALT`.

Since `A_TM` is undecidable and `A_TM ≤_m HALT`, `HALT` is undecidable. □

---

## What to Notice

- The function `f` **constructs a new machine description** — it does not run any machine. This is a critical pattern: reductions build objects, they do not simulate.
- The machine `M'` was designed so that **halting corresponds exactly to accepting** in `M`. This is why the reduction works: HALT asks "does it halt?" and `M'` halts iff `M` accepts.
- The No→No case required **two sub-cases** (reject vs. loop). Both must be handled.
- Properties 1 and 2 are often short but must be stated explicitly.

---

## Why the Order Yes→Yes / No→No (Not ⟺ Directly)

You could write the biconditional `w ∈ A ⟺ f(w) ∈ B` as a single iff and prove it directly. But splitting into Yes→Yes and No→No forces you to:
- Handle each direction with its own logic.
- Notice when one direction is harder (often No→No requires case analysis).
- Avoid accidentally using circular reasoning.

For a reduction proof, always write the two directions separately.

---

## Practice Problems

1. **Verify computability carefully.** In the example above, the TM computing `f` constructs `⟨M'⟩` from `⟨M⟩` without running `M`. Explain in your own words why constructing a machine description is always computable, while simulating a machine might not be.

2. **New reduction.** Let `EMPTY_TM = { ⟨M⟩ : L(M) = ∅ }` (the language of TMs that accept nothing). Prove `A_TM ≤_m OVERLINE(EMPTY_TM)` — that is, reduce `A_TM` to the complement of `EMPTY_TM`. Define `f`, then verify all four properties.

3. **Spot the gap.** A student writes the following reduction and claims it proves `B` is undecidable:
   > "On input `⟨M, w⟩`, simulate `M` on `w`. If `M` accepts, output a string in `B`. If `M` rejects, output a string not in `B`."
   Identify which of the four properties this reduction fails to establish, and explain why.
