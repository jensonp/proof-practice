# 12. Closure Properties of Decidable Languages

## Background

A language `L` is **decidable** if there exists a Turing machine `M` that halts on every input and accepts exactly the strings in `L`.

A **closure property** says: if language(s) with property `P` are combined in some way, the result also has property `P`. For decidable languages, the standard operations are union, intersection, complement, and concatenation.

Proving a closure property requires **constructing a new machine** from the given machines. The proof has two parts:
1. **Describe the construction:** What does the new machine do, step by step?
2. **Verify correctness:** Show the constructed machine actually decides the target language.

This is a new kind of proof. You are not just manipulating symbols — you are building an object and then proving it has a property.

---

## The Technique

Template for a closure proof:

```
Let L₁ and L₂ be decidable languages.
Let M₁ decide L₁ and M₂ decide L₂.   [using the hypothesis]
Construct machine M as follows: ...
Claim: M decides L₁ [operation] L₂.
Proof of correctness:
  (⇒) If w ∈ L₁ [op] L₂, then M accepts w.
  (⇐) If w ∉ L₁ [op] L₂, then M rejects w.
  M halts on every input because ...
```

---

## Example Proof

### Claim: If `L₁` and `L₂` are decidable, then `L₁ ∪ L₂` is decidable.

**Proof:**

Let `M₁` be a decider for `L₁` and `M₂` be a decider for `L₂`. Both halt on every input.

**Construction:** Define machine `M` that on input `w`:
1. Run `M₁` on `w`. If `M₁` accepts, **accept**.
2. Run `M₂` on `w`. If `M₂` accepts, **accept**.
3. **Reject**.

**Claim:** `M` decides `L₁ ∪ L₂`.

**Correctness:**

**(⇒) If `w ∈ L₁ ∪ L₂`, then `M` accepts `w`.**

Assume `w ∈ L₁ ∪ L₂`. By definition of union, `w ∈ L₁` or `w ∈ L₂`.
- If `w ∈ L₁`: since `M₁` decides `L₁`, `M₁` accepts `w`. So `M` accepts at step 1.
- If `w ∈ L₂`: since `M₂` decides `L₂`, `M₂` accepts `w`. So `M` accepts at step 2.

In either case `M` accepts. □

**(⇐) If `w ∉ L₁ ∪ L₂`, then `M` rejects `w`.**

Assume `w ∉ L₁ ∪ L₂`. Then `w ∉ L₁` and `w ∉ L₂`.
- Since `M₁` decides `L₁` and `w ∉ L₁`, `M₁` rejects `w`. So `M` does not accept at step 1.
- Since `M₂` decides `L₂` and `w ∉ L₂`, `M₂` rejects `w`. So `M` does not accept at step 2.
- `M` reaches step 3 and rejects. □

**Halting:** `M₁` halts on every input (it is a decider). `M₂` halts on every input. `M` runs `M₁` then `M₂` sequentially, and halts regardless of outcome. Therefore `M` halts on every input. □

Since `M` accepts exactly `L₁ ∪ L₂` and halts on all inputs, `M` decides `L₁ ∪ L₂`. □

---

## What to Notice

- The construction is **explicit** — we described every step the machine takes.
- Correctness was a **biconditional** (step 6): we proved both directions separately.
- We separately argued **halting** — this is mandatory for deciders and easy to forget.

---

## Practice Problems

1. Prove: if `L₁` and `L₂` are decidable, then `L₁ ∩ L₂` is decidable.
2. Prove: if `L` is decidable, then its complement `L̅ = Σ* \ L` is decidable.
3. Prove: if `L₁` and `L₂` are decidable, then `L₁ \ L₂ = { w : w ∈ L₁ and w ∉ L₂ }` is decidable.
