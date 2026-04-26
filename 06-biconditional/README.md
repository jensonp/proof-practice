# 6. Biconditionals — Proving $\Leftrightarrow$

## The Technique

A **biconditional** $P \Leftrightarrow Q$ ("$P$ if and only if $Q$") means both:
- $P \Rightarrow Q$ (the forward direction), and
- $Q \Rightarrow P$ (the backward direction).

A biconditional proof is always **two separate proofs**. Write them explicitly as $(\Rightarrow)$ and $(\Leftarrow)$.

**Common mistake:** Treating $P \Leftrightarrow Q$ as one thing to prove in one go. It is always two implications. Prove each one independently.

## Example Proof

**Claim:** For any integer $n$, $n$ is even if and only if $n^2$ is even.

**Proof:**

**$(\Rightarrow)$ If $n$ is even, then $n^2$ is even.**

Assume $n$ is even. Then $n = 2k$ for some integer $k$. So:

$$n^2 = (2k)^2 = 4k^2 = 2(2k^2)$$

which is even. $\blacksquare$

**$(\Leftarrow)$ If $n^2$ is even, then $n$ is even.**

We prove the contrapositive: if $n$ is odd, then $n^2$ is odd.

Assume $n$ is odd. Then $n = 2k + 1$ for some integer $k$. So:

$$n^2 = (2k+1)^2 = 4k^2 + 4k + 1 = 2(2k^2 + 2k) + 1$$

which is odd. $\blacksquare$

Since both directions hold, $n$ is even if and only if $n^2$ is even. $\blacksquare$

## What to Notice

- We labeled each direction $(\Rightarrow)$ and $(\Leftarrow)$ explicitly.
- The two directions used **different techniques** — direct proof for one, contrapositive for the other. That is fine.
- The final sentence closes the biconditional by stating that both directions hold.

## Practice Problems

1. Prove: for integers $n$ and $m$, $n + m$ is even if and only if $n$ and $m$ have the same parity.
2. Prove: $A \subseteq B$ if and only if $A \cap B = A$.
3. Prove: $A \subseteq B$ if and only if $A \cup B = B$.
