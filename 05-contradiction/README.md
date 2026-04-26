# 5. Proof by Contradiction

## The Technique

To prove a statement $P$ by contradiction:
1. **Assume $\lnot P$** (that $P$ is false).
2. Derive a **contradiction** — a statement of the form $X \land \lnot X$, which is always false.
3. Since the assumption $\lnot P$ led to something impossible, $\lnot P$ must be false. Therefore $P$ is true.

This technique is useful when $P$ is a universal negative ("no object has property $X$") or an irrationality claim, because these are hard to prove directly.

## Example Proof

**Claim:** $\sqrt{2}$ is irrational.

**Proof:**
Assume, for the sake of contradiction, that $\sqrt{2}$ is rational.

Then $\sqrt{2} = \dfrac{a}{b}$ for some integers $a$ and $b$ with $b \neq 0$, where $\gcd(a, b) = 1$ (the fraction is in lowest terms).

Squaring both sides:

$$2 = \frac{a^2}{b^2} \implies 2b^2 = a^2$$

This means $a^2$ is even. By the result from Proof 4 (if $n^2$ is even then $n$ is even), $a$ is even.

So $a = 2k$ for some integer $k$. Substituting:

$$2b^2 = (2k)^2 = 4k^2 \implies b^2 = 2k^2$$

This means $b^2$ is even, so $b$ is even.

But now both $a$ and $b$ are even, meaning $\gcd(a, b) \geq 2$. This **contradicts** our assumption that $\gcd(a, b) = 1$.

The assumption that $\sqrt{2}$ is rational leads to a contradiction. Therefore $\sqrt{2}$ is irrational. $\blacksquare$

## What to Notice

- We explicitly opened with: **"Assume, for the sake of contradiction..."**
- We tracked **what the contradiction is** at the end: $\gcd(a,b) = 1$ vs $\gcd(a,b) \geq 2$.
- We used a previously proven result (Proof 4) as a lemma — proofs build on each other.

## Practice Problems

1. Prove by contradiction: there is no largest even integer.
2. Prove by contradiction: if $n^2$ is divisible by $5$, then $n$ is divisible by $5$.
3. Prove by contradiction: $\sqrt{3}$ is irrational.
