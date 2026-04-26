# 19. Proving NP-Hardness via Polynomial-Time Reduction

## Background

A language `B` is **NP-hard** if every language in NP can be reduced to it in polynomial time:

```
B is NP-hard  ⟺  ∀A ∈ NP, A ≤_p B
```

You never prove NP-hardness by directly reducing every NP language to `B` (there are infinitely many). Instead you use **transitivity of reductions**:

> If `A ≤_p B` and `B ≤_p C`, then `A ≤_p C`.

So to prove `B` is NP-hard, it suffices to show `K ≤_p B` for any single language `K` that is **already known to be NP-hard**. The most common starting point is **3-SAT**.

---

## The Polynomial-Time Reduction (`≤_p`)

A **polynomial-time many-one reduction** from `A` to `B` is a function `f` computable in polynomial time such that:

```
w ∈ A  ⟺  f(w) ∈ B
```

This is identical in structure to the mapping reductions from steps 16–17, with one added requirement: **`f` must run in polynomial time** (not just be computable).

The four properties to verify are the same as step 16, with property (1) upgraded:

| # | Property | Requirement |
|---|---|---|
| 1 | **Poly-time computable** | `f` is computed by a TM running in polynomial time |
| 2 | **Total** | `f(w)` defined for all `w` |
| 3 | **Yes → Yes** | `w ∈ A` implies `f(w) ∈ B` |
| 4 | **No → No** | `w ∉ A` implies `f(w) ∉ B` |

---

## The Source: 3-SAT

**3-SAT** is the canonical NP-hard language. Cook-Levin theorem (not proved here, taken as established) says:

```
3-SAT = { <φ> : φ is a satisfiable 3-CNF Boolean formula }
```

A **3-CNF formula** is a conjunction (AND) of **clauses**, where each clause is a disjunction (OR) of exactly **3 literals** (a variable or its negation).

Example: `(x₁ ∨ ¬x₂ ∨ x₃) ∧ (¬x₁ ∨ x₂ ∨ x₄) ∧ (x₂ ∨ ¬x₃ ∨ ¬x₄)`

A formula is **satisfiable** if there exists a truth assignment to the variables that makes every clause true.

---

## Worked Example: 3-SAT ≤_p CLIQUE

This is one of the most instructive reductions in complexity theory. It converts a satisfiability question into a graph clique question.

### Claim: `CLIQUE` is NP-hard.

**Proof:** We show `3-SAT ≤_p CLIQUE`.

---

### Step 1 — Design the Reduction

Given a 3-CNF formula `φ` with `k` clauses, we construct a graph `G` and integer `k` such that:

```
φ is satisfiable  ⟺  G has a clique of size k
```

**The key idea:** Each clause contributes 3 nodes (one per literal). A clique of size `k` will pick exactly one literal per clause — a consistent truth assignment satisfying all clauses.

---

### Step 2 — Define `f`

**Input:** A 3-CNF formula `φ = C₁ ∧ C₂ ∧ ... ∧ Cₖ` where each clause `Cᵢ = (lᵢ₁ ∨ lᵢ₂ ∨ lᵢ₃)`.

**Construct graph `G = (V, E)`:**

- **Vertices:** For each clause `Cᵢ` and each literal `lᵢⱼ` in that clause, create a node `(i, j)`. Total: `3k` vertices.
- **Edges:** Add edge between `(i, j)` and `(i', j')` if and only if:
  1. They come from **different clauses**: `i ≠ i'`, AND
  2. Their literals are **not contradictory**: it is not the case that one is `x` and the other is `¬x` for the same variable.

**Output:** `f(φ) = ⟨G, k⟩`.

---

### Step 3 — Verify the Four Properties

**(1) Poly-time computable:**
Given `φ` with `k` clauses, we create `3k` vertices. For each pair of vertices `(i,j)` and `(i',j')` (there are `O(k²)` pairs), we check two conditions: `i ≠ i'` (constant time) and whether literals are contradictory (constant time per pair given parsed input). Total construction time: `O(k²)` which is polynomial in `|φ|`. ✓

**(2) Totality:**
For any input (well-formed or not), the construction produces a valid graph and integer. Malformed inputs produce a trivially empty or fixed graph. `f` is total. ✓

**(3) Yes → Yes:** Assume `φ` is satisfiable.

Let `A` be a satisfying assignment. For each clause `Cᵢ`, since `A` satisfies `Cᵢ`, at least one literal `lᵢⱼᵢ` in `Cᵢ` is true under `A`. Select one such literal per clause; call these selected nodes `s₁, s₂, ..., sₖ` (one from each clause).

**Claim:** `{s₁, ..., sₖ}` is a clique of size `k` in `G`.

Take any two nodes `sᵢ = (i, jᵢ)` and `sᵢ’ = (i', jᵢ’)` with `i ≠ i'`.
- They come from different clauses: condition 1 for edges is satisfied.
- Their literals are both true under `A`. No variable can be both true and false simultaneously, so one cannot be `x` and the other `¬x`. Condition 2 for edges is satisfied.

Therefore every pair `(sᵢ, sᵢ’)` is connected by an edge. The `k` selected nodes form a clique of size `k`. So `⟨G, k⟩ ∈ CLIQUE`. ✓

**(4) No → No:** Assume `φ` is not satisfiable. We show `G` has no clique of size `k`.

Suppose for contradiction that `S = {(i₁,j₁), ..., (iₖ,jₖ)}` is a clique of size `k` in `G`.

Since edges only connect nodes from **different clauses**, and we have exactly `k` nodes and `k` clauses, the pigeonhole principle forces exactly one node per clause in `S` (if two nodes came from the same clause, they share index `i` and would not be connected — but then we'd need `k` nodes from fewer than `k` clause-groups, impossible with no intra-clause edges).

So `S` picks one literal per clause. Define truth assignment `A` as follows: for each node `(i, jᵢ)` in `S`, set the variable of `lᵢⱼᶢ` to make `lᵢⱼᶢ` true.

This assignment is **consistent** because every pair of nodes in `S` is connected by an edge, meaning no two literals in `S` are contradictory. So no variable is set to both true and false.

Since every clause has its selected literal set to true, `A` satisfies every clause. So `A` satisfies `φ` — contradicting the assumption that `φ` is not satisfiable.

Therefore no clique of size `k` exists. `⟨G, k⟩ ∉ CLIQUE`. ✓

---

### Conclusion

All four properties hold. Therefore `3-SAT ≤_p CLIQUE`.

Since `3-SAT` is NP-hard and `3-SAT ≤_p CLIQUE`, `CLIQUE` is NP-hard. □

---

## What to Notice

- **The graph encodes the structure of the formula.** Vertices are literals, edges encode compatibility. This is the typical pattern: translate the combinatorial structure of one problem into the structure of another.
- **Yes→Yes** constructed a clique from a satisfying assignment — the assignment told us which nodes to pick.
- **No→No** worked by contradiction: a clique would imply a satisfying assignment, contradicting unsatisfiability. This reverse direction (clique → assignment) is as important as the forward direction.
- **Pigeonhole** was the key lemma in No→No: `k` nodes from `k` groups with no intra-group edges forces exactly one node per group.
- The reduction runs in **polynomial time** — `O(k²)` — because we only iterate over pairs of vertices, not over all possible assignments.

---

## The Reduction Chain So Far

NP-hardness proofs build a chain. Each arrow is a polynomial-time reduction:

```
All NP languages
      ↓  (Cook-Levin)
    3-SAT
      ↓  (this step)
    CLIQUE
      ↓  (step 20 and beyond)
  VERTEX-COVER, HAM-PATH, SUBSET-SUM, ...
```

Once `CLIQUE` is NP-hard, you can prove other problems NP-hard by reducing from `CLIQUE` (or from any NP-hard problem). You never need to go back to `3-SAT` directly.

---

## Practice Problems

1. **Trace the reduction on a small instance.** Let `φ = (x₁ ∨ ¬x₂ ∨ x₃) ∧ (¬x₁ ∨ x₂ ∨ x₃) ∧ (x₁ ∨ x₂ ∨ ¬x₃)`.
   - (a) Construct the graph `G` produced by `f(φ)`. List all vertices and all edges.
   - (b) Find a satisfying assignment for `φ` and identify the corresponding clique of size 3 in `G`.
   - (c) Verify that the clique nodes are pairwise connected in `G`.

2. **3-SAT ≤_p INDEPENDENT-SET.** Define:
   ```
   INDEPENDENT-SET = { ⟨G, k⟩ : G has an independent set of size k }
   ```
   An **independent set** is a set of vertices with no edges between them. Prove `3-SAT ≤_p INDEPENDENT-SET` by defining `f` and verifying all four properties.
   - *Hint: the construction is nearly identical to CLIQUE — flip which pairs of nodes get edges.*

3. **CLIQUE ≤_p INDEPENDENT-SET.** Prove `CLIQUE ≤_p INDEPENDENT-SET` directly using the complement graph.
   - Define `f(⟨G, k⟩) = ⟨G̅, k⟩` where `G̅` is the complement of `G` (same vertices, edges exactly where `G` has none).
   - Verify all four properties and argue polynomial-time computability.
   - What does this tell you about the hardness of INDEPENDENT-SET?
