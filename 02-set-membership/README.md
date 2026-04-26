# 2. Set Membership — Chasing Definitions

## The Technique

Most set proofs follow one pattern: **take an arbitrary element and chase what the definitions say about it.**

To prove $A \subseteq B$, you:
1. Take an arbitrary element $x$ and assume $x \in A$.
2. Using only the definition of $A$, derive that $x \in B$.
3. Conclude $A \subseteq B$.

The word **arbitrary** is important. You cannot pick a specific element (like $x = 5$). You pick an element about which you know nothing except that it satisfies the hypothesis.

## Key Definitions

- $A \subseteq B$ means: for all $x$, if $x \in A$ then $x \in B$.
- $A \cap B = \{ x : x \in A \text{ and } x \in B \}$
- $A \cup B = \{ x : x \in A \text{ or } x \in B \}$

## Example Proof 1

**Claim:** For any sets $A$ and $B$, $A \cap B \subseteq A$.

**Proof:**
Let $x$ be an arbitrary element. Assume $x \in A \cap B$.

By definition of intersection, $x \in A \cap B$ means $x \in A$ **and** $x \in B$.

In particular, $x \in A$.

Since $x$ was arbitrary and we showed $x \in A \cap B$ implies $x \in A$, we conclude $A \cap B \subseteq A$. $\blacksquare$

## Example Proof 2

**Claim:** For any sets $A$, $B$, $C$, if $A \subseteq B$ and $B \subseteq C$, then $A \subseteq C$.

**Proof:**
Assume $A \subseteq B$ and $B \subseteq C$. Let $x$ be arbitrary and assume $x \in A$.

Since $A \subseteq B$, by definition of subset, $x \in B$.
Since $B \subseteq C$, by definition of subset, $x \in C$.

Since $x$ was arbitrary, $A \subseteq C$. $\blacksquare$

## What to Notice

- "Let $x$ be arbitrary" opens the proof. It is a ritual. Always write it.
- We never assumed anything about $x$ except what the hypothesis gives us.
- The conclusion closes the quantifier: "since $x$ was arbitrary."

## Practice Problems

1. Prove: $A \subseteq A \cup B$ for any sets $A$ and $B$.
2. Prove: if $A \subseteq B$, then $A \cap C \subseteq B \cap C$.
3. Prove: $A \cap B = B \cap A$. *(Hint: prove both $A \cap B \subseteq B \cap A$ and $B \cap A \subseteq A \cap B$.)*
