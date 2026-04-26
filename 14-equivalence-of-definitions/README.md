# 14. Equivalence of Two Definitions

## Background

In complexity theory, **NP** has two standard definitions:

- **Definition A (NTM-based):** A language `L` is in NP if there exists a nondeterministic Turing machine `N` that decides `L` in polynomial time — meaning every branch of `N` on any input of length `n` halts within `p(n)` steps for some polynomial `p`.

- **Definition B (Verifier-based):** A language `L` is in NP if there exists a deterministic polynomial-time Turing machine `V` (a verifier) and a polynomial `q` such that for every string `w`:
  - If `w ∈ L`, there exists a certificate `c` with `|c| ≤ q(|w|)` such that `V(w, c)` accepts.
  - If `w ∉ L`, then for all `c`, `V(w, c)` rejects.

Proving these definitions are equivalent is an **iff proof** (step 6), where each direction requires constructing a machine and verifying its polynomial time bound.

---

## The Technique

An equivalence of definitions proof has the form:

```
"Definition A" ⇔ "Definition B"

(⇒) Assume L satisfies Definition A.
     Construct an object satisfying Definition B.
     Verify correctness and time bound.

(⇐) Assume L satisfies Definition B.
     Construct an object satisfying Definition A.
     Verify correctness and time bound.
```

---

## Example Proof

### Claim: Definition A and Definition B for NP are equivalent.

**Proof:**

### (⇒) If `L ∈ NP` by Definition A, then `L ∈ NP` by Definition B.

Assume `N` is an NTM deciding `L` in polynomial time `p(n)`.

**Construction of verifier `V`:**
A certificate `c` for input `w` will encode the sequence of nondeterministic choices made along one accepting branch of `N` on `w`. Since `N` runs in `p(n)` steps, each branch has length at most `p(n)`, and at each step there are at most `b` choices (where `b` is the maximum branching factor of `N`, a constant). So `c` can be encoded as a string of length at most `p(n) · ⌈log b⌉`, which is polynomial in `n`.

Define `V(w, c)` as follows:
1. Simulate `N` on input `w`, following the choices encoded in `c` at each step.
2. If the simulation reaches `q_accept`, **accept**. Otherwise **reject**.

**Time bound:** `V` simulates `N` for at most `p(n)` steps, each step taking polynomial time. So `V` runs in polynomial time. □

**Correctness:**
- If `w ∈ L`: since `N` accepts `w`, there exists an accepting branch. Let `c` encode that branch's choices. Then `V(w, c)` simulates that branch and accepts.
- If `w ∉ L`: since `N` does not accept `w`, no branch reaches `q_accept`. For any `c`, `V(w, c)` follows the choices of `c` and never reaches `q_accept`, so it rejects. □

---

### (⇐) If `L ∈ NP` by Definition B, then `L ∈ NP` by Definition A.

Assume `V` is a polynomial-time verifier for `L` with certificate length bound `q(n)`.

**Construction of NTM `N`:**
Define `N` on input `w` (where `|w| = n`) as follows:
1. Nondeterministically write a string `c` of length at most `q(n)` on a second tape. (At each of `q(n)` steps, nondeterministically choose a symbol from Σ or stop.)
2. Run `V(w, c)` deterministically.
3. Accept if and only if `V(w, c)` accepts.

**Time bound:** Step 1 takes `q(n)` nondeterministic steps. Step 2 takes polynomial time in `|w| + |c| ≤ n + q(n)`, which is polynomial in `n`. So each branch of `N` runs in polynomial time. □

**Correctness:**
- If `w ∈ L`: by Definition B, there exists a certificate `c` with `|c| ≤ q(n)` such that `V(w, c)` accepts. The branch of `N` that writes exactly this `c` in step 1 will accept in step 3. So `N` accepts `w`.
- If `w ∉ L`: by Definition B, for all `c`, `V(w, c)` rejects. Every branch of `N` writes some `c` and runs `V(w, c)`, which rejects. So no branch of `N` accepts. So `N` does not accept `w`. □

Since both directions hold, the two definitions are equivalent. □

---

## What to Notice

- This is a large proof. It has **four sub-proofs**: construction + correctness + time for each direction.
- Each direction required **building an object** (a verifier or an NTM) and then **verifying two things**: correctness and polynomial time.
- The certificate in direction (⇒) is exactly the **sequence of nondeterministic choices** — this is the key insight connecting NTMs to verifiers.

---

## Practice Problems

1. In the (⇒) direction, why does the certificate `c` have polynomial length? Write this argument in one complete paragraph.
2. In the (⇐) direction, why does the NTM `N` halt on all branches? Give the halting argument explicitly.
3. Define co-NP informally. State and prove: `L ∈` co-NP if and only if `L̅ ∈` NP.
