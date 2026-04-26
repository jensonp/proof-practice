# 15. Diagonalization — The Halting Problem

## Background

Diagonalization is the proof technique used to show that certain problems are **undecidable** — no Turing machine can solve them, no matter how much time or space it uses.

The core idea: assume a machine `M` solves the problem. Construct a new machine `D` that uses `M` as a subroutine. Feed `D` its own description as input. Show that `M` existing causes `D` to contradict itself — `D` accepts if and only if it rejects. This is impossible, so `M` cannot exist.

The name "diagonalization" comes from Cantor's diagonal argument: the constructed object `D` is designed to differ from every machine at exactly the point where the machine is asked about itself.

---

## Key Definitions

- `<M>` denotes the **encoding** of machine `M` as a string over `{0,1}`. Every Turing machine can be encoded as a finite binary string.
- The **halting problem** is the language `HALT = { <M, w> : M halts on input w }`.
- The **acceptance problem** is `A_TM = { <M, w> : M accepts w }`.
- A language is **undecidable** if no Turing machine decides it.

---

## The Technique

Diagonalization proof template:

```
Assume, for contradiction, that machine H decides the target language.
Construct machine D using H as a subroutine.
Run D on input <D> (D's own description).
Show: D accepts <D> ⇔ D rejects <D>.
This is a contradiction. Therefore H cannot exist.
```

---

## Example Proof

### Claim: `A_TM = { <M, w> : M accepts w }` is undecidable.

**Proof:**

Assume, for the sake of contradiction, that `A_TM` is decidable. Let `H` be a decider for `A_TM`. Then `H` halts on every input and:
- `H` accepts `<M, w>` if `M` accepts `w`.
- `H` rejects `<M, w>` if `M` does not accept `w`.

**Construction of `D`:** Define machine `D` that on input `<M>` (the encoding of a Turing machine `M`):
1. Run `H` on input `<M, <M>>`. (Ask: does machine `M` accept its own description?)
2. If `H` **accepts**, then **reject**.
3. If `H` **rejects**, then **accept**.

`D` is a valid Turing machine because `H` is assumed to exist and halt on all inputs, so step 1 always terminates.

**The diagonal contradiction:** Run `D` on its own description `<D>`.

`D` executes step 1: run `H` on `<D, <D>>`. Since `H` decides `A_TM`, `H` accepts `<D, <D>>` if and only if `D` accepts `<D>`.

Now trace the two cases:

**Case 1:** Suppose `D` accepts `<D>`.
Then `H` accepts `<D, <D>>` (since `H` is correct about `D` accepting `<D>`).
Then by step 2 of `D`'s construction, `D` **rejects** `<D>`. Contradiction.

**Case 2:** Suppose `D` does not accept `<D>`.
Then `H` rejects `<D, <D>>` (since `H` is correct about `D` not accepting `<D>`).
Then by step 3 of `D`'s construction, `D` **accepts** `<D>`. Contradiction.

Both cases are impossible. The assumption that `H` exists leads to a contradiction. Therefore `A_TM` is undecidable. □

---

## What to Notice

- The proof is a **proof by contradiction** (step 5) at the outer level.
- The contradiction is not a numerical impossibility — it is a **logical impossibility**: `D` accepts `<D>` if and only if it does not.
- The machine `D` is designed specifically to **invert** whatever `H` says. This is the diagonal.
- We never said anything about what `D` does on inputs other than `<D>`. Only the self-referential case matters.
- The proof assumes that a Turing machine **can be encoded as a string** and **can receive its own encoding as input**. Both are true and are taken as established here.

---

## Connection to Previous Steps

| Step | Technique used in this proof |
|---|---|
| 5 | Outer structure is proof by contradiction |
| 8 | Negating the acceptance condition carefully |
| 12 | Constructing a machine explicitly |
| 13 | Using one machine (`H`) as a subroutine inside another (`D`) |

---

## Practice Problems

1. Prove: `HALT = { <M, w> : M halts on w }` is undecidable. *(Reduce from `A_TM`: assume `HALT` is decidable, build a decider for `A_TM`, derive a contradiction.)*
2. Explain in one paragraph why the construction of `D` in the proof above would fail if `H` were only a recognizer (might loop) rather than a decider.
3. State the claim "the complement of `A_TM` is not Turing-recognizable" and outline the proof. *(Hint: use the fact that if both `A_TM` and its complement were recognizable, `A_TM` would be decidable.)*
