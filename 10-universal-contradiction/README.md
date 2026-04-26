# 10. Universal Statements by Contradiction

## The Technique

To prove $\forall x,\, P(x)$ by contradiction:
1. Assume $\lnot(\forall x,\, P(x))$, which equals $\exists x,\, \lnot P(x)$.
2. Let $x_0$ be the specific element for which $\lnot P(x_0)$ holds.
3. Derive a contradiction from the existence of $x_0$.
4. Conclude $\forall x,\, P(x)$.

This technique is especially useful for proving infiniteness or other "for all" claims where contradiction localizes the failure to one element.

## Example Proof

**Claim:** There are infinitely many prime numbers.

**Proof:**
Assume, for the sake of contradiction, that there are only finitely many primes. List them all:

$$p_1, p_2, p_3, \ldots, p_n$$

Construct the number:

$$N = p_1 \cdot p_2 \cdot p_3 \cdots p_n + 1$$

Consider two cases:

**Case 1: $N$ is prime.**
Then $N$ is a prime not in our list (since $N > p_i$ for every $i$). This contradicts the assumption that our list contains all primes.

**Case 2: $N$ is composite.**
Then $N$ has a prime factor $q$. Since every prime is in our list, $q = p_i$ for some $i$. But then $p_i$ divides both $N$ and $p_1 \cdot p_2 \cdots p_n$. So $p_i$ divides their difference:

$$N - p_1 \cdot p_2 \cdots p_n = 1$$

A prime dividing $1$ is impossible, since all primes are $\geq 2$.

Both cases lead to contradictions. Therefore there are infinitely many primes. $\blacksquare$

## What to Notice

- We negated $\forall$ to get $\exists$: "finitely many" is the concrete form of the assumption.
- We **constructed an object** ($N$) designed to cause a contradiction — this is the creative step.
- We handled **all cases** of the object we constructed. Leaving a case unchecked makes the proof incomplete.
- The contradiction was specific: a prime divides $1$, which is impossible.

## Practice Problems

1. Prove by contradiction: there is no largest integer.
2. Prove by contradiction: there are infinitely many even numbers.
3. Prove by contradiction: the set of all strings over $\{0, 1\}$ is infinite.
