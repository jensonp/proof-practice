# 3. Direct Proof of an Implication

## The Technique

An **implication** has the form: **If $P$, then $Q$** (written $P \Rightarrow Q$).

To prove it directly:
1. **Assume $P$** is true.
2. Using $P$ and any other facts you know, derive **$Q$**.
3. Conclude $P \Rightarrow Q$.

You do not need to verify what happens when $P$ is false. The implication $P \Rightarrow Q$ is automatically true whenever $P$ is false — a fact called **vacuous truth**. Your only job is the case when $P$ holds.

## Example Proof 1

**Claim:** If $n$ is even, then $n^2$ is even.

**Proof:**
Assume $n$ is even. By definition, there exists an integer $k$ such that $n = 2k$.

Then:

$$n^2 = (2k)^2 = 4k^2 = 2(2k^2)$$

Let $m = 2k^2$. Since $k$ is an integer, $m$ is an integer. Therefore $n^2 = 2m$, so $n^2$ is even by definition. $\blacksquare$

## Example Proof 2

**Claim:** If $n$ is odd, then $n^2$ is odd.

**Proof:**
Assume $n$ is odd. Then there exists an integer $k$ such that $n = 2k + 1$.

$$n^2 = (2k+1)^2 = 4k^2 + 4k + 1 = 2(2k^2 + 2k) + 1$$

Let $m = 2k^2 + 2k$. Since $k$ is an integer, $m$ is an integer. Therefore $n^2 = 2m + 1$, so $n^2$ is odd. $\blacksquare$

## What to Notice

- The proof opens by **assuming the hypothesis**.
- All algebra is shown explicitly and each result is named.
- The proof closes by **restating the conclusion** in the language of the definition.

## Practice Problems

1. Prove: if $n$ is divisible by $3$, then $n^2$ is divisible by $9$.
2. Prove: if $n$ and $m$ are odd, then $nm$ is odd.
3. Prove: if $n^2 + n$ is odd, then $n$ is even. *(Hint: factor first.)*
