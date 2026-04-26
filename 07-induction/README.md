# 7. Proof by Induction

## The Technique

**Mathematical induction** proves that a statement $P(n)$ holds for all natural numbers $n \geq n_0$.

The structure is:
1. **Base case:** Prove $P(n_0)$ directly.
2. **Inductive step:** Assume $P(k)$ holds for some arbitrary $k \geq n_0$ (the **inductive hypothesis**). Then prove $P(k+1)$ using that assumption.
3. **Conclusion:** By induction, $P(n)$ holds for all $n \geq n_0$.

**Why it works:** The base case establishes $n = n_0$. The inductive step says: given any $k$ that works, $k+1$ also works. So $n_0$ works, then $n_0+1$, then $n_0+2$, and so on.

## Example Proof

**Claim:** For all $n \geq 1$,

$$1 + 2 + \cdots + n = \frac{n(n+1)}{2}$$

**Proof by induction on $n$:**

**Base case $(n = 1)$:**
The left side is $1$. The right side is $\dfrac{1 \cdot 2}{2} = 1$. They are equal. ✓

**Inductive step:**
Assume the formula holds for some $k \geq 1$:

$$1 + 2 + \cdots + k = \frac{k(k+1)}{2} \tag{IH}$$

We want to show it holds for $k + 1$, i.e., that:

$$1 + 2 + \cdots + k + (k+1) = \frac{(k+1)(k+2)}{2}$$

Starting from the left side:

$$1 + 2 + \cdots + k + (k+1) = \frac{k(k+1)}{2} + (k+1) \quad \text{(by IH)}$$

$$= \frac{k(k+1)}{2} + \frac{2(k+1)}{2} = \frac{k(k+1) + 2(k+1)}{2} = \frac{(k+1)(k+2)}{2}$$

This is exactly the formula for $n = k+1$.

By induction, the formula holds for all $n \geq 1$. $\blacksquare$

## What to Notice

- The inductive hypothesis is **stated explicitly** and labeled (IH).
- In the inductive step, we **started from the left side** of the $k+1$ case and used (IH) as a substitution.
- We never said "obviously" or "it follows" — every algebraic step is written.

## Practice Problems

1. Prove by induction: $1^2 + 2^2 + \cdots + n^2 = \dfrac{n(n+1)(2n+1)}{6}$ for all $n \geq 1$.
2. Prove by induction: $2^0 + 2^1 + \cdots + 2^n = 2^{n+1} - 1$ for all $n \geq 0$.
3. Prove by induction: for all $n \geq 1$, $n^3 - n$ is divisible by $6$.
