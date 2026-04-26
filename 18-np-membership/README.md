# 18. Proving NP Membership — Exhibit a Certificate, Bound Verification Time

## Background

Recall from step 14 that a language `L` is in **NP** if and only if there exists a polynomial-time verifier `V` and a polynomial `q` such that:

```
w ∈ L  ⟺  ∃c with |c| ≤ q(|w|) such that V(w, c) accepts
```

To prove `L ∈ NP` you do **not** need to find a fast algorithm that solves `L`. You only need to show that a proposed solution can be *checked* quickly. This is a much easier bar.

Proving NP membership is one half of proving NP-completeness (the other half, NP-hardness, is step 19).

---

## The Two Things to Show

Every NP membership proof must establish exactly two things:

| # | What to show | How to prove it |
|---|---|---|
| 1 | **Certificate exists and has polynomial length** | Describe what the certificate `c` is; argue `|c| ≤ q(|w|)` for some polynomial `q` |
| 2 | **Verification runs in polynomial time** | Describe what the verifier `V(w, c)` does; argue every step runs in time polynomial in `|w|` |

> **Common mistake:** Describing a certificate but not bounding its length, or describing verification steps without arguing their time complexity. Both omissions make the proof incomplete.

---

## The Technique

NP membership proof template:

```
Claim: L ∈ NP.
Proof:

Certificate: [Describe what c is for a yes-instance w ∈ L]
Length bound: [Argue |c| ≤ p(|w|) for some polynomial p]

Verifier V(w, c):
  [Describe every check V performs, step by step]

Time analysis:
  [Bound the running time of each step in terms of |w|]
  Total: O(p(|w|)^k) for some constants — polynomial in |w|.

Correctness:
  (⇒) If w ∈ L, the described certificate exists and V accepts.
  (⇐) If V accepts with certificate c, then w ∈ L.

Therefore L ∈ NP. □
```

---

## Example Proof 1: CLIQUE

**Define:**
```
CLIQUE = { ⟨G, k⟩ : G is an undirected graph containing a clique of size k }
```

A **clique** of size `k` in graph `G` is a set of `k` vertices such that every pair of vertices in the set is connected by an edge.

### Claim: `CLIQUE ∈ NP`.

**Proof:**

**Certificate:** Given `⟨G, k⟩ ∈ CLIQUE`, the certificate `c` is the set of `k` vertices that form the clique. Represent `c` as a list of `k` vertex labels.

**Length bound:** The graph `G` has at most `n` vertices (where `n = |⟨G, k⟩|`). Each vertex label requires at most `O(log n)` bits. A list of `k ≤ n` labels has length at most `k · O(log n) = O(n log n)`, which is polynomial in `n`. ✓

**Verifier `V(⟨G, k⟩, c)`:**
1. Check that `c` is a list of exactly `k` distinct vertices of `G`. If not, reject.
2. For every pair of vertices `u, v` in `c`, check that the edge `(u, v)` exists in `G`. If any pair is missing an edge, reject.
3. Accept.

**Time analysis:**
- Step 1: Parsing `c` and checking `k` distinctness takes `O(k²)` time — at most `O(n²)`.
- Step 2: There are `C(k, 2) ≤ k²/2` pairs. For each pair, checking edge existence in an adjacency matrix takes `O(1)`, or `O(n)` in an adjacency list. Total: `O(k² · n) = O(n³)`.
- Step 3: `O(1)`.

Total time: `O(n³)`, which is polynomial in `|⟨G, k⟩|`. ✓

**Correctness:**

*(⇒)* If `⟨G, k⟩ ∈ CLIQUE`, there exists a set `S` of `k` vertices forming a clique. Use `S` as the certificate. `V` checks `k` vertices, finds all edges present, and accepts.

*(⇐)* If `V(⟨G, k⟩, c)` accepts, then `c` is a list of `k` distinct vertices of `G` and every pair is connected by an edge. By definition, those vertices form a clique of size `k` in `G`. So `⟨G, k⟩ ∈ CLIQUE`. ✓

Therefore `CLIQUE ∈ NP`. □

---

## Example Proof 2: SUBSET-SUM

**Define:**
```
SUBSET-SUM = { ⟨S, t⟩ : S is a multiset of integers and some subset of S sums to t }
```

### Claim: `SUBSET-SUM ∈ NP`.

**Proof:**

**Certificate:** A subset `T ⊆ S` that sums to `t`.

**Length bound:** `T` contains at most `|S|` integers, each of which fits in `O(log(max value))` bits — at most `O(n)` bits per element where `n = |⟨S, t⟩|`. Total length of `T` is `O(n²)` at most — polynomial. ✓

**Verifier `V(⟨S, t⟩, c)`:**
1. Check that every element of `c` appears in `S` with correct multiplicity. If not, reject.
2. Compute the sum of all elements in `c`.
3. If the sum equals `t`, accept. Otherwise reject.

**Time analysis:**
- Step 1: `O(n²)` — matching each element of `c` against `S`.
- Step 2: `O(n)` additions, each on integers of `O(n)` bits: `O(n²)`.
- Step 3: `O(n)` comparison.

Total: `O(n²)`, polynomial. ✓

**Correctness:**

*(⇒)* If `⟨S, t⟩ ∈ SUBSET-SUM`, a subset `T` summing to `t` exists. Use `T` as the certificate. `V` confirms it is a valid subset, computes its sum, and accepts.

*(⇐)* If `V` accepts, then `c` is a valid subset of `S` and its sum equals `t`. So `⟨S, t⟩ ∈ SUBSET-SUM`. ✓

Therefore `SUBSET-SUM ∈ NP`. □

---

## What to Notice

- In both proofs, the certificate is the **solution itself** — the clique, the subset. This is the typical pattern: for combinatorial problems, the certificate is the witnessing object.
- The verifier **does not search** for a solution. It only checks one candidate. Searching would take exponential time; checking takes polynomial time.
- Correctness is a biconditional (step 6). The *(⇒)* direction says a certificate exists when `w ∈ L`. The *(⇐)* direction says acceptance implies `w ∈ L`. Both are required.
- The length bound is easy to overlook but essential. A certificate of exponential length would require exponential time just to read — the whole proof would collapse.

---

## Relationship to P

If `L ∈ P`, then `L ∈ NP`. The certificate can be the empty string, and the verifier just runs the polynomial-time algorithm for `L` directly on `w`. So `P ⊆ NP`. Whether `P = NP` — whether every NP problem has a polynomial-time algorithm — is the most famous open problem in computer science.

---

## Practice Problems

1. **VERTEX-COVER.** Define:
   ```
   VERTEX-COVER = { ⟨G, k⟩ : G has a vertex cover of size k }
   ```
   A **vertex cover** is a set `S` of vertices such that every edge in `G` has at least one endpoint in `S`. Prove `VERTEX-COVER ∈ NP`. Define the certificate, bound its length, describe the verifier, analyze its running time, and prove correctness in both directions.

2. **HAMILTONIAN-PATH.** Define:
   ```
   HAM-PATH = { ⟨G, s, t⟩ : G has a Hamiltonian path from s to t }
   ```
   A **Hamiltonian path** visits every vertex exactly once. Prove `HAM-PATH ∈ NP`.

3. **Certificate length matters.** Suppose someone proposes the following certificate for CLIQUE: "the list of all edges in the clique." Show that this certificate is also valid (polynomial length, checkable in polynomial time), and explain why both certificates are equally acceptable for the purpose of proving NP membership.
