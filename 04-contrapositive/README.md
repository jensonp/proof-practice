# 4. Proof by Contrapositive

## The Technique

The **contrapositive** of $P \Rightarrow Q$ is $\lnot Q \Rightarrow \lnot P$. These two statements are **logically equivalent** — they are both true or both false at the same time.

Sometimes $Q$ is easier to negate and work with than $P$ is to assume. When the direct proof feels stuck, try the contrapositive:

1. Assume $\lnot Q$ (the negation of the conclusion).
2. Derive $\lnot P$ (the negation of the hypothesis).
3. Conclude $P \Rightarrow Q$.

**When to reach for it:** When the hypothesis $P$ is a negative or existential statement and $Q$ is a simpler positive statement. Negating $Q$ gives you something concrete to work with.

## Example Proof

**Claim:** If $n^2$ is even, then $n$ is even.

**Why contrapositive is easier here:** The hypothesis is about $n^2$, but we want to say something about $n$. It is easier to start from a fact about $n$ and derive one about $n^2$.

**Contrapositive form:** If $n$ is odd, then $n^2$ is odd.

**Proof (of the contrapositive):**
Assume $n$ is odd. Then by definition, $n = 2k + 1$ for some integer $k$.

$$n^2 = (2k+1)^2 = 4k^2 + 4k + 1 = 2(2k^2 + 2k) + 1$$

This is odd. Therefore, if $n$ is odd then $n^2$ is odd, which is the contrapositive of the original claim.

Since the contrapositive holds, the original claim holds: if $n^2$ is even then $n$ is even. $\blacksquare$

## What to Notice

- We proved the contrapositive, not the original. We must **state** this clearly.
- At the end we invoke logical equivalence to conclude the original.
- The proof we wrote is essentially the same as the one in Proof 3 — we are just reusing it at the right moment.

## Practice Problems

1. Prove by contrapositive: if $n^2$ is odd, then $n$ is odd.
2. Prove by contrapositive: if the product $ab$ is odd, then both $a$ and $b$ are odd.
3. Prove by contrapositive: if $n$ is not divisible by $3$, then $n^2$ is not divisible by $3$.
