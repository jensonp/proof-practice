# 13. Simulation Arguments

## Background

A **simulation argument** proves that one computational model is at least as powerful as another, or that two models are equivalent. The proof has a fixed structure:

1. **Given:** A machine of type A.
2. **Construct:** A machine of type B that simulates A.
3. **Verify:** The constructed machine of type B accepts exactly the same inputs as A.

Simulation proofs appear throughout computability and complexity theory. The key discipline is: you must describe the simulating machine **concretely enough** that its behavior is unambiguous, and then prove correctness formally.

---

## The Technique

The most important simulation in this course: every DTM is a special case of an NTM.

Recall:
- A **DTM** has transition function `δ_D : Q × Γ → Q × Γ × {L,R}` (at most one move per state-symbol pair).
- An **NTM** has transition function `δ_N : Q × Γ → P(Q × Γ × {L,R})` (a set of possible moves).

---

## Example Proof

### Claim: Every deterministic Turing machine is a special case of a nondeterministic Turing machine.

Formally: if `L` is decided by a DTM, then `L` is decided by an NTM.

**Proof:**

Let `M = (Q, Σ, Γ, δ_D, q₀, q_accept, q_reject)` be a DTM that decides `L`.

**Construction:** Define NTM `N = (Q, Σ, Γ, δ_N, q₀, q_accept, q_reject)` where for every `q ∈ Q` and `a ∈ Γ`:

```
δ_N(q, a) = { δ_D(q, a) }    if δ_D(q, a) is defined
δ_N(q, a) = ∅                if δ_D(q, a) is undefined
```

In words: `N` has the same states, alphabets, and start/halt states as `M`. Its transition function wraps each deterministic move in a singleton set.

**Correctness:**

**(⇒) If `M` accepts `w`, then `N` accepts `w`.**

Since `M` accepts `w`, there is a computation of `M` on `w` that reaches `q_accept`. This computation is a finite sequence of configurations `C₀, C₁, ..., Cₖ` where `C₀` is the start configuration on `w` and `Cₖ` has state `q_accept`.

Each step `Cᵢ → Cᵢ₊₁` follows `δ_D`. By construction, `δ_D(q, a) = (r, b, D)` implies `(r, b, D) ∈ δ_N(q, a)`. So every step of `M`'s computation is a legal step of `N`.

Therefore the same sequence `C₀, C₁, ..., Cₖ` is a valid computation branch of `N` that reaches `q_accept`. So `N` accepts `w`. □

**(⇐) If `N` accepts `w`, then `M` accepts `w`.**

Since `N` accepts `w`, some computation branch of `N` on `w` reaches `q_accept`. Let this branch be `C₀, C₁, ..., Cₖ`.

Each step `Cᵢ → Cᵢ₊₁` uses some `(r, b, D) ∈ δ_N(q, a)`. By construction, `δ_N(q, a)` contains at most one element (namely `δ_D(q, a)`). So the only possible move is `δ_D(q, a)`.

Therefore `C₀, C₁, ..., Cₖ` is also a valid computation of `M`, and it reaches `q_accept`. So `M` accepts `w`. □

**Halting:** `M` halts on every input. By the argument above, `N`'s only branch on any input follows `M`'s unique computation. Since `M` halts, this branch halts. Therefore `N` halts on every input (all branches halt). So `N` is a decider. □

Since `N` accepts exactly the strings `M` accepts and halts on all inputs, `N` decides `L`. □

---

## What to Notice

- We gave a **concrete construction**: we defined `δ_N` precisely in terms of `δ_D`.
- We proved **both directions** of correctness as a biconditional (step 6).
- We proved **halting** separately — it is not automatic.
- We reused the structure of the original machine's computation rather than re-deriving everything.

---

## Practice Problems

1. Prove: an NTM with at most one transition per state-symbol pair is equivalent to a DTM.
2. Prove: a two-tape DTM can be simulated by a single-tape DTM. *(Describe the encoding and verify acceptance equivalence.)*
3. Prove: if a language is decided by a DTM, then it is also recognized by a DTM. *(Hint: a decider is already a recognizer.)*
