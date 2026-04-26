# 1. Direct Calculation — Arithmetic Identities

## The Technique

The simplest proofs apply definitions directly, one step at a time. You do not need creativity. You need to know what the symbols mean and apply them.

**Goal:** Get comfortable with the idea that "prove" means "write down every step, with a reason."

## Key Definitions

- An integer $n$ is **even** if there exists an integer $k$ such that $n = 2k$.
- An integer $n$ is **odd** if there exists an integer $k$ such that $n = 2k + 1$.
- $n + 0 = n$ for all integers — this is an axiom of integer arithmetic.

## Example Proof 1

**Claim:** For all integers $n$, $n + 0 = n$.

**Proof:**
This follows directly from the additive identity axiom of the integers, which states that for every element $n$ in the set of integers, there exists an element $0$ such that $n + 0 = n$. Applying this axiom with the element $n$ gives the result. $\blacksquare$

## Example Proof 2

**Claim:** If $n$ is even and $m$ is even, then $n + m$ is even.

**Proof:**
Assume $n$ is even and $m$ is even.

By definition of even, there exists an integer $j$ such that $n = 2j$.
By definition of even, there exists an integer $k$ such that $m = 2k$.

Then:

$$n + m = 2j + 2k = 2(j + k)$$

Let $p = j + k$. Since $j$ and $k$ are integers, $p$ is an integer. Therefore $n + m = 2p$, which means $n + m$ is even by definition. $\blacksquare$

## What to Notice

- Every step is justified ("by definition of even", "factoring").
- We **named** the witness: $p = j + k$. We did not just say "some integer exists".
- The box $\blacksquare$ marks the end of the proof.

## Practice Problems

1. Prove: if $n$ is odd and $m$ is odd, then $n + m$ is even.
2. Prove: if $n$ is even, then $n^2 = 4k^2$ for some integer $k$.
3. Prove: $0 \cdot n = 0$ for all integers $n$, using the distributive law $(a + b) \cdot c = ac + bc$ and the identity $0 + 0 = 0$.
