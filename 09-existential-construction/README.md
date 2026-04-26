# 9. Existential Proofs by Construction

## The Technique

To prove $\exists x,\, P(x)$, you only need to **exhibit one specific $x$** and verify that it satisfies $P$. You do not need to explain how you found it. You do not need to show it is unique. One witness is enough.

This is sometimes called a **constructive proof**.

**The trap to avoid:** Confusing an existential proof with a universal one. If you prove $\exists x,\, P(x)$ by showing $P(7)$ holds, that is valid. But if you want to prove $\forall x,\, P(x)$ and only show $P(7)$, that is invalid.

## Example Proof 1

**Claim:** There exists a prime number greater than $100$.

**Proof:**
Consider $n = 101$. We claim $101$ is prime.

A number is prime if it is greater than $1$ and has no positive divisors other than $1$ and itself. It suffices to check all primes $p \leq \sqrt{101} < 11$, which are $2, 3, 5, 7$.

- $101 / 2 = 50.5$ — not an integer.
- $101 / 3 \approx 33.67$ — not an integer.
- $101 / 5 = 20.2$ — not an integer.
- $101 / 7 \approx 14.43$ — not an integer.

Since $101$ has no prime divisors $\leq \sqrt{101}$, it is prime. Since $101 > 100$, we have exhibited a prime greater than $100$. $\blacksquare$

## Example Proof 2

**Claim:** There exists an irrational number $x$ such that $x^2$ is rational.

**Proof:**
Let $x = \sqrt{2}$. We know $\sqrt{2}$ is irrational (Proof 5). Then:

$$x^2 = (\sqrt{2})^2 = 2$$

which is rational. So $x = \sqrt{2}$ is an irrational number whose square is rational. $\blacksquare$

## What to Notice

- We stated the witness ($n = 101$, $x = \sqrt{2}$) immediately and then verified the property.
- We did not need to explain how we found the witness.
- Verification was explicit — we checked every necessary condition.

## Practice Problems

1. Prove: there exists an integer $n$ such that $n^2 = 2n$.
2. Prove: there exist irrational numbers $a$ and $b$ such that $a + b$ is rational.
3. Prove: there exist integers $a$, $b$, $c$ (not all zero) such that $a^2 + b^2 = c^2$.
