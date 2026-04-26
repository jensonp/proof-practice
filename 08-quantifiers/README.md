# 8. Quantifiers — $\forall$ and $\exists$ Explicitly

## The Technique

Many proof errors come from misreading quantifiers. Before proving anything involving $\forall$ or $\exists$, **translate the statement into plain English and back.** This makes the proof structure visible.

| Statement | Proof strategy |
|---|---|
| $\forall x,\, P(x)$ | Take arbitrary $x$, prove $P(x)$ |
| $\exists x,\, P(x)$ | Exhibit a specific $x$ and verify $P(x)$ |
| $\lnot (\forall x,\, P(x)) = \exists x,\, \lnot P(x)$ | Find one counterexample |
| $\lnot (\exists x,\, P(x)) = \forall x,\, \lnot P(x)$ | Take arbitrary $x$, show $\lnot P(x)$ |

**Negating quantifiers:**
- The negation of $\forall x,\, P(x)$ is $\exists x,\, \lnot P(x)$.
- The negation of $\exists x,\, P(x)$ is $\forall x,\, \lnot P(x)$.

This is the most common source of errors in proof by contradiction — **always negate the statement carefully** before starting.

## Example Proof 1

**Claim:** $A \subseteq B$ if and only if $\forall x,\, (x \in A \Rightarrow x \in B)$.

**Proof:**

$(\Rightarrow)$ Assume $A \subseteq B$. Let $x$ be arbitrary. Assume $x \in A$. By definition of $A \subseteq B$, we have $x \in B$. Since $x$ was arbitrary, $\forall x,\, (x \in A \Rightarrow x \in B)$. $\blacksquare$

$(\Leftarrow)$ Assume $\forall x,\, (x \in A \Rightarrow x \in B)$. Let $x$ be arbitrary and assume $x \in A$. Instantiating the universal with this $x$, we get $x \in B$. So $A \subseteq B$. $\blacksquare$

## Example Proof 2

**Claim:** There is no integer that is both even and odd.

**Translation:** $\lnot(\exists n,\; n \text{ is even} \land n \text{ is odd})$, which equals $\forall n,\; \lnot(n \text{ is even} \land n \text{ is odd})$.

**Proof:**
Let $n$ be an arbitrary integer. Suppose for contradiction that $n$ is both even and odd.

Then $n = 2j$ and $n = 2k + 1$ for some integers $j$, $k$. So:

$$2j = 2k + 1 \implies 2(j - k) = 1$$

This means $1$ is even (since $1 = 2(j-k)$), which contradicts the fact that $1$ is odd. Contradiction.

Since $n$ was arbitrary, no integer is both even and odd. $\blacksquare$

## Practice Problems

1. Prove: $\forall n \in \mathbb{Z},\; n^2 \geq 0$.
2. Prove: $\lnot(\exists n \in \mathbb{Z},\; n^2 < 0)$.
3. Prove: $A = B$ if and only if $A \subseteq B$ and $B \subseteq A$. *(Write out the full quantifier translation for $A = B$ first.)*
