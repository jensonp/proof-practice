# Proof Practice

A progressive guide to writing mathematical proofs — built for someone with zero proof-writing experience. Each level introduces one new technique. Complete them in order.

---

## Table of Contents

1. [Direct Calculation — Arithmetic Identities](#1-direct-calculation--arithmetic-identities)
2. [Set Membership — Chasing Definitions](#2-set-membership--chasing-definitions)
3. [Direct Proof of an Implication](#3-direct-proof-of-an-implication)
4. [Proof by Contrapositive](#4-proof-by-contrapositive)
5. [Proof by Contradiction](#5-proof-by-contradiction)
6. [Biconditionals — Proving ↔](#6-biconditionals--proving-)
7. [Proof by Induction](#7-proof-by-induction)
8. [Quantifiers — ∀ and ∃ Explicitly](#8-quantifiers----and--explicitly)
9. [Existential Proofs by Construction](#9-existential-proofs-by-construction)
10. [Universal Statements by Contradiction](#10-universal-statements-by-contradiction)

---

## What a Proof Is

A proof is a **finite sequence of justified steps** that starts from things you are allowed to assume (axioms, definitions, hypotheses) and ends at the statement you want to show is true. Every single step must follow from the previous ones by a rule you can name.

A proof is **not** an explanation of why something feels right. It is not a calculation that "gets close." It is not an argument from examples. It is a chain of logic with no missing links.

---

## 1. Direct Calculation — Arithmetic Identities

### The Technique

The simplest proofs apply definitions directly, one step at a time. You do not need creativity. You need to know what the symbols mean and apply them.

**Goal:** Get comfortable with the idea that "prove" means "write down every step, with a reason."

### Key Definitions

- An integer `n` is **even** if there exists an integer `k` such that `n = 2k`.
- An integer `n` is **odd** if there exists an integer `k` such that `n = 2k + 1`.
- `n + 0 = n` for all integers — this is an axiom of integer arithmetic.

### Example Proof

**Claim:** For all integers `n`, `n + 0 = n`.

**Proof:**
This follows directly from the additive identity axiom of the integers, which states that for every element `n` in the set of integers, there exists an element `0` such that `n + 0 = n`. Applying this axiom with the element `n` gives the result. □

---

**Claim:** If `n` is even and `m` is even, then `n + m` is even.

**Proof:**
Assume `n` is even and `m` is even.

By definition of even, there exists an integer `j` such that `n = 2j`.
By definition of even, there exists an integer `k` such that `m = 2k`.

Then:
```
n + m = 2j + 2k    (substituting definitions)
      = 2(j + k)   (factoring out 2)
```

Let `p = j + k`. Since `j` and `k` are integers, `p` is an integer.
Therefore `n + m = 2p`, which means `n + m` is even by definition. □

### What to Notice

- Every step is justified ("by definition of even", "factoring").
- We **named** the witness: `p = j + k`. We did not just say "some integer exists".
- The box □ marks the end of the proof.

### Practice Problems

1. Prove: if `n` is odd and `m` is odd, then `n + m` is even.
2. Prove: if `n` is even, then `n² = 4k²` for some integer `k`.
3. Prove: `0 · n = 0` for all integers `n`, using the distributive law `(a + b) · c = ac + bc` and the identity `0 + 0 = 0`.

---

## 2. Set Membership — Chasing Definitions

### The Technique

Most set proofs follow one pattern: **take an arbitrary element and chase what the definitions say about it.**

To prove `A ⊆ B`, you:
1. Take an arbitrary element `x` and assume `x ∈ A`.
2. Using only the definition of `A`, derive that `x ∈ B`.
3. Conclude `A ⊆ B`.

The word **arbitrary** is important. You cannot pick a specific element (like `x = 5`). You pick an element about which you know nothing except that it satisfies the hypothesis.

### Key Definitions

- `A ⊆ B` means: for all `x`, if `x ∈ A` then `x ∈ B`.
- `A ∩ B = { x : x ∈ A and x ∈ B }`
- `A ∪ B = { x : x ∈ A or x ∈ B }`

### Example Proof

**Claim:** For any sets `A` and `B`, `A ∩ B ⊆ A`.

**Proof:**
Let `x` be an arbitrary element. Assume `x ∈ A ∩ B`.

By definition of intersection, `x ∈ A ∩ B` means `x ∈ A` **and** `x ∈ B`.

In particular, `x ∈ A`.

Since `x` was arbitrary and we showed `x ∈ A ∩ B` implies `x ∈ A`, we conclude `A ∩ B ⊆ A`. □

---

**Claim:** For any sets `A`, `B`, `C`, if `A ⊆ B` and `B ⊆ C`, then `A ⊆ C`.

**Proof:**
Assume `A ⊆ B` and `B ⊆ C`. Let `x` be arbitrary and assume `x ∈ A`.

Since `A ⊆ B`, by definition of subset, `x ∈ B`.
Since `B ⊆ C`, by definition of subset, `x ∈ C`.

Since `x` was arbitrary, `A ⊆ C`. □

### What to Notice

- "Let `x` be arbitrary" opens the proof. It is a ritual. Always write it.
- We never assumed anything about `x` except what the hypothesis gives us.
- The conclusion closes the quantifier: "since `x` was arbitrary."

### Practice Problems

1. Prove: `A ⊆ A ∪ B` for any sets `A` and `B`.
2. Prove: if `A ⊆ B`, then `A ∩ C ⊆ B ∩ C`.
3. Prove: `A ∩ B = B ∩ A`. *(Hint: prove both `A ∩ B ⊆ B ∩ A` and `B ∩ A ⊆ A ∩ B`.)*

---

## 3. Direct Proof of an Implication

### The Technique

An **implication** has the form: **If P, then Q** (written `P → Q`).

To prove it directly:
1. **Assume P** is true.
2. Using P and any other facts you know, derive **Q**.
3. Conclude `P → Q`.

You do not need to verify what happens when P is false. The implication `P → Q` is automatically true whenever P is false — a fact called **vacuous truth**. Your only job is the case when P holds.

### Example Proof

**Claim:** If `n` is even, then `n²` is even.

**Proof:**
Assume `n` is even.

By definition, there exists an integer `k` such that `n = 2k`.

Then:
```
n² = (2k)²
   = 4k²
   = 2(2k²)
```

Let `m = 2k²`. Since `k` is an integer, `m` is an integer.
Therefore `n² = 2m`, so `n²` is even by definition. □

---

**Claim:** If `n` is odd, then `n²` is odd.

**Proof:**
Assume `n` is odd. Then there exists an integer `k` such that `n = 2k + 1`.

```
n² = (2k + 1)²
   = 4k² + 4k + 1
   = 2(2k² + 2k) + 1
```

Let `m = 2k² + 2k`. Since `k` is an integer, `m` is an integer.
Therefore `n² = 2m + 1`, so `n²` is odd. □

### What to Notice

- The proof opens by **assuming the hypothesis**.
- All algebra is shown explicitly and each result is named.
- The proof closes by **restating the conclusion** in the language of the definition.

### Practice Problems

1. Prove: if `n` is divisible by 3, then `n²` is divisible by 9.
2. Prove: if `n` and `m` are odd, then `nm` is odd.
3. Prove: if `n² + n` is odd, then `n` is even. *(Hint: factor first.)*

---

## 4. Proof by Contrapositive

### The Technique

The **contrapositive** of `P → Q` is `¬Q → ¬P`. These two statements are **logically equivalent** — they are both true or both false at the same time.

Sometimes Q is easier to negate and work with than P is to assume. When the direct proof feels stuck, try the contrapositive:

1. Assume `¬Q` (the negation of the conclusion).
2. Derive `¬P` (the negation of the hypothesis).
3. Conclude `P → Q`.

**When to reach for it:** When the hypothesis P is a negative or existential statement and Q is a simpler positive statement. Negating Q gives you something concrete to work with.

### Example Proof

**Claim:** If `n²` is even, then `n` is even.

**Why contrapositive is easier here:** The hypothesis is about `n²`, but we want to say something about `n`. It is easier to start from a fact about `n` and derive one about `n²`.

**Contrapositive form:** If `n` is odd, then `n²` is odd.

**Proof (of the contrapositive):**
Assume `n` is odd. Then by definition, `n = 2k + 1` for some integer `k`.

```
n² = (2k + 1)² = 4k² + 4k + 1 = 2(2k² + 2k) + 1
```

This is odd. Therefore, if `n` is odd then `n²` is odd, which is the contrapositive of the original claim.

Since the contrapositive holds, the original claim holds: if `n²` is even then `n` is even. □

### What to Notice

- We proved the contrapositive, not the original. We must **state** this clearly.
- At the end we invoke logical equivalence to conclude the original.
- The proof we wrote is essentially the same as the one in Section 3 — we are just reusing it at the right moment.

### Practice Problems

1. Prove by contrapositive: if `n²` is odd, then `n` is odd.
2. Prove by contrapositive: if the product `ab` is odd, then both `a` and `b` are odd.
3. Prove by contrapositive: if `n` is not divisible by 3, then `n²` is not divisible by 3.

---

## 5. Proof by Contradiction

### The Technique

To prove a statement `P` by contradiction:
1. **Assume `¬P`** (that P is false).
2. Derive a **contradiction** — a statement of the form `X and ¬X`, which is always false.
3. Since the assumption `¬P` led to something impossible, `¬P` must be false. Therefore `P` is true.

This technique is useful when P is a universal negative ("no object has property X") or an irrationality claim, because these are hard to prove directly.

### Example Proof

**Claim:** √2 is irrational.

**Proof:**
Assume, for the sake of contradiction, that √2 is rational.

Then √2 = a/b for some integers `a` and `b` with `b ≠ 0`, and where `a/b` is in **lowest terms** (i.e., `gcd(a, b) = 1`).

Squaring both sides:
```
2 = a²/b²
2b² = a²
```

This means `a²` is even. By the result from Section 4 (if `n²` is even then `n` is even), `a` is even.

So `a = 2k` for some integer `k`. Substituting:
```
2b² = (2k)² = 4k²
b² = 2k²
```

This means `b²` is even, so `b` is even.

But now both `a` and `b` are even, meaning `gcd(a, b) ≥ 2`. This **contradicts** our assumption that `a/b` was in lowest terms (`gcd(a, b) = 1`).

The assumption that √2 is rational leads to a contradiction. Therefore √2 is irrational. □

### What to Notice

- We explicitly opened with: **"Assume, for the sake of contradiction..."**
- We tracked **what the contradiction is** at the end: `gcd(a,b) = 1` vs `gcd(a,b) ≥ 2`.
- We used a previously proven result (Section 4) as a lemma — proofs build on each other.

### Practice Problems

1. Prove by contradiction: there is no largest even integer.
2. Prove by contradiction: if `n²` is divisible by 5, then `n` is divisible by 5.
3. Prove by contradiction: √3 is irrational.

---

## 6. Biconditionals — Proving ↔

### The Technique

A **biconditional** `P ↔ Q` ("P if and only if Q") means both:
- `P → Q` (the forward direction), and
- `Q → P` (the backward direction).

A biconditional proof is always **two separate proofs**. Write them explicitly as **(⇒)** and **(⇐)**, or **(→)** and **(←)**.

**Common mistake:** Treating `P ↔ Q` as one thing to prove in one go. It is always two implications. Prove each one independently.

### Example Proof

**Claim:** For any integer `n`, `n` is even if and only if `n²` is even.

**Proof:**

**(⇒) If `n` is even, then `n²` is even.**

Assume `n` is even. Then `n = 2k` for some integer `k`. So `n² = 4k² = 2(2k²)`, which is even. □

**(⇐) If `n²` is even, then `n` is even.**

We prove the contrapositive: if `n` is odd, then `n²` is odd.

Assume `n` is odd. Then `n = 2k + 1` for some integer `k`. So:
```
n² = (2k+1)² = 4k² + 4k + 1 = 2(2k² + 2k) + 1
```
which is odd. □

Since both directions hold, `n` is even if and only if `n²` is even. □

### What to Notice

- We labeled each direction **(⇒)** and **(⇐)** explicitly.
- The two directions used **different techniques** — direct proof for one, contrapositive for the other. That is fine.
- The final sentence closes the biconditional by stating that both directions hold.

### Practice Problems

1. Prove: for integers `n` and `m`, `n + m` is even if and only if `n` and `m` have the same parity (both even or both odd).
2. Prove: `A ⊆ B` if and only if `A ∩ B = A`.
3. Prove: `A ⊆ B` if and only if `A ∪ B = B`.

---

## 7. Proof by Induction

### The Technique

**Mathematical induction** proves that a statement `P(n)` holds for all natural numbers `n ≥ n₀`.

The structure is:
1. **Base case:** Prove `P(n₀)` directly.
2. **Inductive step:** Assume `P(k)` holds for some arbitrary `k ≥ n₀` (**inductive hypothesis**). Then prove `P(k+1)` using that assumption.
3. **Conclusion:** By induction, `P(n)` holds for all `n ≥ n₀`.

**Why it works:** The base case gets `n = n₀`. The inductive step says: given any `k` that works, `k+1` also works. So `n₀` works, then `n₀+1`, then `n₀+2`, and so on — covering every natural number.

### Example Proof

**Claim:** For all `n ≥ 1`, the sum of the first `n` natural numbers equals `n(n+1)/2`.

Formally: `1 + 2 + ... + n = n(n+1)/2`.

**Proof by induction on `n`:**

**Base case (n = 1):**
The left side is just `1`. The right side is `1 · 2 / 2 = 1`. They are equal. ✓

**Inductive step:**
Assume the formula holds for some `k ≥ 1`:
```
1 + 2 + ... + k = k(k+1)/2    [inductive hypothesis]
```

We want to show it holds for `k + 1`, i.e., that:
```
1 + 2 + ... + k + (k+1) = (k+1)(k+2)/2
```

Starting from the left side:
```
1 + 2 + ... + k + (k+1)
  = [1 + 2 + ... + k] + (k+1)      (grouping)
  = k(k+1)/2 + (k+1)               (inductive hypothesis)
  = k(k+1)/2 + 2(k+1)/2            (common denominator)
  = [k(k+1) + 2(k+1)] / 2
  = (k+1)(k+2) / 2                 (factoring k+1)
```

This is exactly `(k+1)(k+2)/2`, which is the formula for `n = k+1`.

By induction, the formula holds for all `n ≥ 1`. □

### What to Notice

- The inductive hypothesis is **stated explicitly** with a label.
- In the inductive step, we **started from the left side** of the `k+1` case and used the inductive hypothesis as a substitution.
- We never said "obviously" or "it follows" — every algebraic step was written.

### Practice Problems

1. Prove by induction: `1² + 2² + ... + n² = n(n+1)(2n+1)/6` for all `n ≥ 1`.
2. Prove by induction: `2⁰ + 2¹ + ... + 2ⁿ = 2ⁿ⁺¹ - 1` for all `n ≥ 0`.
3. Prove by induction: for all `n ≥ 1`, `n³ - n` is divisible by 6.

---

## 8. Quantifiers — ∀ and ∃ Explicitly

### The Technique

Many proof errors come from misreading quantifiers. Before proving anything involving ∀ or ∃, **translate the statement into plain English and back.** This makes the proof structure visible.

| Statement | Proof strategy |
|---|---|
| `∀x, P(x)` | Take arbitrary `x`, prove `P(x)` |
| `∃x, P(x)` | Exhibit a specific `x` and verify `P(x)` |
| `¬(∀x, P(x))` = `∃x, ¬P(x)` | Find one counterexample |
| `¬(∃x, P(x))` = `∀x, ¬P(x)` | Take arbitrary `x`, show `¬P(x)` |

**Negating quantifiers:**
- The negation of "for all x, P(x)" is "there exists x such that ¬P(x)".
- The negation of "there exists x such that P(x)" is "for all x, ¬P(x)".

This is the most common source of errors in proof by contradiction — **always negate the statement carefully** before starting.

### Example Proof

**Claim:** `A ⊆ B` if and only if `∀x, (x ∈ A → x ∈ B)`.

This is essentially a definition restatement, but walking through it carefully locks in the quantifier structure.

**Proof:**

**(⇒)** Assume `A ⊆ B`. Let `x` be arbitrary. Assume `x ∈ A`. By definition of `A ⊆ B`, `x ∈ B`. Since `x` was arbitrary, `∀x, (x ∈ A → x ∈ B)`. □

**(⇐)** Assume `∀x, (x ∈ A → x ∈ B)`. We want to show `A ⊆ B`, i.e., every element of `A` is in `B`. Let `x` be arbitrary and assume `x ∈ A`. By our assumption (instantiating the universal with this `x`), `x ∈ B`. So `A ⊆ B`. □

---

**Claim:** There is no integer that is both even and odd.

**Translation:** `¬(∃n, n is even ∧ n is odd)` = `∀n, ¬(n is even ∧ n is odd)`.

**Proof:**
Let `n` be an arbitrary integer. Suppose for contradiction that `n` is both even and odd.

Then `n = 2j` and `n = 2k + 1` for some integers `j`, `k`.
```
2j = 2k + 1
2j - 2k = 1
2(j - k) = 1
```

This means `1` is even (since `1 = 2(j-k)`), which contradicts the fact that `1` is odd. Contradiction.

Since `n` was arbitrary, no integer is both even and odd. □

### Practice Problems

1. Prove: `∀n ∈ ℤ, n² ≥ 0`.
2. Prove: `¬(∃n ∈ ℤ, n² < 0)`.
3. Prove: `A = B` if and only if `A ⊆ B` and `B ⊆ A`. *(Write out the full quantifier translation for A = B first.)*

---

## 9. Existential Proofs by Construction

### The Technique

To prove `∃x, P(x)`, you only need to **exhibit one specific `x`** and verify that it satisfies `P`. You do not need to explain how you found it. You do not need to show it is the only one. One witness is enough.

This is sometimes called a **constructive proof** or a **proof by example** (in the existential sense — not a proof that a universal statement holds by checking one case, which would be invalid).

**The trap to avoid:** Confusing an existential proof with a universal one. If you prove `∃x, P(x)` by showing `P(7)` holds, that is valid. But if you want to prove `∀x, P(x)` and only show `P(7)`, that is invalid.

### Example Proof

**Claim:** There exists a prime number greater than 100.

**Proof:**
Consider `n = 101`. We claim `101` is prime.

A number is prime if it is greater than 1 and has no positive divisors other than 1 and itself. The primes up to `√101 < 11` are: 2, 3, 5, 7.

- `101 / 2 = 50.5` — not an integer.
- `101 / 3 = 33.67...` — not an integer.
- `101 / 5 = 20.2` — not an integer.
- `101 / 7 = 14.43...` — not an integer.

Since `101` has no prime divisors ≤ √101, it is prime. Since `101 > 100`, we have exhibited a prime greater than 100. □

---

**Claim:** There exists an irrational number `x` such that `xˣ` is rational.

**Proof:**
This is a famous nonconstructive existence argument, but we present a constructive version.

Let `x = √2`. We know √2 is irrational (from Section 5). Then:
```
(√2)² = 2
```
which is rational. So `x = √2` is an irrational number with `xˣ` rational (taking the exponent to be 2 here).

More precisely: `(√2)^(√2·√2) = (√2)^2 = 2`. Thus the irrational base √2 raised to the power 2 (which equals √2 · √2) gives a rational number. □

### What to Notice

- We stated the witness (`n = 101`, `x = √2`) immediately and then verified the property.
- We did not need to explain how we found the witness.
- Verification was explicit — we checked every necessary condition.

### Practice Problems

1. Prove: there exists an integer `n` such that `n² = 2n`.
2. Prove: there exist irrational numbers `a` and `b` such that `a + b` is rational.
3. Prove: there exist integers `a`, `b`, `c` (not all zero) such that `a² + b² = c²`. *(Pythagorean triple.)*

---

## 10. Universal Statements by Contradiction

### The Technique

To prove `∀x, P(x)` by contradiction:
1. Assume `¬(∀x, P(x))`, which equals `∃x, ¬P(x)`.
2. Let `x₀` be the specific element for which `¬P(x₀)` holds.
3. Derive a contradiction from the existence of `x₀`.
4. Conclude `∀x, P(x)`.

This technique is especially useful for proving infiniteness or other "for all" claims where a direct approach would require handling every element, but contradiction localizes the failure to one element.

### Example Proof

**Claim:** There are infinitely many prime numbers.

**Proof:**
Assume, for the sake of contradiction, that there are only finitely many primes. List them all:
```
p₁, p₂, p₃, ..., pₙ
```

Construct the number:
```
N = p₁ · p₂ · p₃ · ... · pₙ + 1
```

Consider two cases:

**Case 1: `N` is prime.**
Then `N` is a prime not in our list (since `N > pᵢ` for every `i`). This contradicts the assumption that our list contains all primes.

**Case 2: `N` is composite.**
Then `N` has a prime factor `q`. Since every prime is in our list, `q = pᵢ` for some `i`. But then `pᵢ` divides both `N` and `p₁ · p₂ · ... · pₙ`. So `pᵢ` divides their difference:
```
N - (p₁ · p₂ · ... · pₙ) = 1
```
A prime dividing `1` is impossible, since all primes are ≥ 2.

Both cases lead to contradictions. Therefore the assumption that there are finitely many primes is false. There are infinitely many primes. □

### What to Notice

- We negated `∀` to get `∃`: "finitely many" is the concrete form of the assumption.
- We **constructed an object** (`N`) designed to cause a contradiction — this is the creative step.
- We handled **all cases** of the object we constructed. Leaving a case unchecked makes the proof incomplete.
- The contradiction was specific: a prime divides 1, which is impossible.

### Practice Problems

1. Prove by contradiction: there is no largest integer.
2. Prove by contradiction: there are infinitely many even numbers. *(Simple, but good practice with the template.)*
3. Prove by contradiction: the set of all strings over `{0, 1}` is infinite.

---

## Summary of Techniques

| # | Technique | Open with | Useful when |
|---|---|---|---|
| 1 | Direct calculation | Apply definitions step by step | Simple arithmetic/algebraic facts |
| 2 | Set membership | "Let x be arbitrary, assume x ∈ A" | Proving A ⊆ B |
| 3 | Direct implication | "Assume P" | P → Q, P is a positive/constructive condition |
| 4 | Contrapositive | "Assume ¬Q" | P → Q, ¬Q is simpler to work with |
| 5 | Contradiction | "Assume ¬P, for contradiction" | Irrationality, impossibility |
| 6 | Biconditional | Prove (⇒) then (⇐) separately | P ↔ Q, always two proofs |
| 7 | Induction | Base case, then inductive step | Statements about all n ≥ n₀ |
| 8 | Quantifier manipulation | Translate ∀/∃ to English first | Before any proof involving quantifiers |
| 9 | Construction | Exhibit the witness, verify it | Proving ∃x, P(x) |
| 10 | Universal by contradiction | Negate ∀ to get ∃, derive contradiction | Infiniteness, universal negatives |

---

## What Comes Next (Steps 11–20)

Once the above are comfortable, the next levels introduce:

- **11.** Language/set facts over Σ* — applying the above to formal language theory
- **12.** Closure properties — proving decidable/recognizable languages are closed under operations
- **13.** Simulation arguments — constructing one machine from another and verifying correctness
- **14.** Equivalence of definitions — NTM-based NP equals verifier-based NP
- **15.** Diagonalization — the halting problem
- **16–20.** Reductions, NP membership, NP-hardness, NP-completeness
