# 20. Proving NP-Completeness — Combining Membership and Hardness

## Background

A language `B` is **NP-complete** if it satisfies both:

1. `B ∈ NP` — solutions can be verified in polynomial time (step 18).
2. `B` is **NP-hard** — every language in NP reduces to `B` in polynomial time (step 19).

NP-complete problems are the hardest problems in NP. If any NP-complete problem is in P, then P = NP — every problem whose solution can be checked quickly can also be *solved* quickly.

This step brings together everything from steps 14, 18, and 19 into a single complete proof. An NP-completeness proof always has **two clearly labeled parts**.

---

## The Structure of Every NP-Completeness Proof

```
Claim: B is NP-complete.
Proof:

Part 1 — NP membership:
  [From step 18: exhibit certificate, bound length,
   describe verifier, bound time, prove correctness]

Part 2 — NP-hardness:
  [From step 19: choose known NP-hard language K,
   define poly-time reduction f : K ≤_p B,
   verify all four properties]

Since B ∈ NP and B is NP-hard, B is NP-complete. □
```

Neither part alone is sufficient. A proof of NP membership says nothing about hardness. A proof of NP-hardness says nothing about membership (an NP-hard problem might not even be in NP — the halting problem is NP-hard but undecidable).

---

## Worked Example: VERTEX-COVER is NP-Complete

**Define:**
```
VERTEX-COVER = { ⟨G, k⟩ : G has a vertex cover of size ≤ k }
```

A **vertex cover** of graph `G` is a set `S` of vertices such that every edge in `G` has at least one endpoint in `S`.

### Claim: `VERTEX-COVER` is NP-complete.

---

## Part 1 — VERTEX-COVER ∈ NP

**Certificate:** A set `S` of at most `k` vertices claimed to be a vertex cover.

**Length bound:** `S` contains at most `k ≤ n` vertices (where `n = |⟨G, k⟩|`). Each vertex label is `O(log n)` bits. Total length: `O(n log n)` — polynomial. ✓

**Verifier `V(⟨G, k⟩, c)`:**
1. Check `|c| ≤ k` and every vertex in `c` exists in `G`. If not, reject.
2. For every edge `(u, v)` in `G`, check that `u ∈ c` or `v ∈ c`. If any edge is uncovered, reject.
3. Accept.

**Time analysis:**
- Step 1: `O(k)` ≤ `O(n)`.
- Step 2: `|E|` edges, each check is `O(k)` membership lookup — total `O(|E| · k) = O(n²)` with an adjacency list or sorted set.
- Step 3: `O(1)`.

Total: `O(n²)` — polynomial. ✓

**Correctness:**

*(⇒)* If `⟨G, k⟩ ∈ VERTEX-COVER`, a valid cover `S` of size `≤ k` exists. Use `S` as the certificate. `V` confirms size and checks every edge — all edges are covered, so `V` accepts.

*(⇐)* If `V` accepts with certificate `c`, then `c` is a set of at most `k` vertices covering every edge. By definition, `c` is a vertex cover of size `≤ k`, so `⟨G, k⟩ ∈ VERTEX-COVER`. ✓

**Therefore `VERTEX-COVER ∈ NP`.** □

---

## Part 2 — VERTEX-COVER is NP-Hard

We show `CLIQUE ≤_p VERTEX-COVER`. Since `CLIQUE` is NP-hard (step 19), this makes `VERTEX-COVER` NP-hard.

### The Key Lemma

> **Lemma:** Let `G` be a graph with `n` vertices and let `G̅` be its complement (edges exactly where `G` has none). Then `G` has a clique of size `k` if and only if `G̅` has a vertex cover of size `n - k`.

**Proof of Lemma:**

*(⇒)* Suppose `S` is a clique of size `k` in `G`. Let `T = V \ S` (the remaining `n - k` vertices). We claim `T` is a vertex cover of `G̅`.

Let `(u, v)` be any edge in `G̅`. By definition of complement, `(u, v)` is **not** an edge in `G`. Since `S` is a clique, every pair of vertices in `S` **is** connected in `G`. Therefore `u` and `v` cannot both be in `S` (otherwise `(u,v)` would be a `G`-edge). So at least one of `u, v` is in `T = V \ S`. Therefore `T` covers the edge `(u, v)`.

Since `(u, v)` was arbitrary, `T` covers all edges of `G̅`. `T` is a vertex cover of size `n - k`. ✓

*(⇐)* Suppose `T` is a vertex cover of size `n - k` in `G̅`. Let `S = V \ T` (size `k`). We claim `S` is a clique in `G`.

Let `u, v ∈ S` be any two distinct vertices in `S`. Since `S = V \ T`, neither `u` nor `v` is in `T`. Since `T` is a vertex cover of `G̅`, every edge of `G̅` has at least one endpoint in `T`. Since neither `u` nor `v` is in `T`, the edge `(u, v)` cannot be in `G̅`. By definition of complement, `(u, v)` must be in `G`.

Since `u, v` were arbitrary vertices in `S`, every pair in `S` is connected in `G`. So `S` is a clique of size `k` in `G`. ✓

This completes the proof of the lemma. □

---

### Define `f`

**On input `⟨G, k⟩`:** Output `⟨G̅, n - k⟩` where `G̅` is the complement of `G` and `n = |V(G)|`.

### Verify the Four Properties

**(1) Poly-time computable:**
Given `G` with `n` vertices and `m` edges, construct `G̅` by iterating over all `C(n,2)` pairs of vertices and including exactly those pairs **not** in `G`. This takes `O(n²)` time — polynomial in `|⟨G, k⟩|`. ✓

**(2) Totality:**
`f` produces a valid output for every input. Malformed inputs map to a trivially small fixed instance. ✓

**(3) Yes → Yes:** Assume `⟨G, k⟩ ∈ CLIQUE`, i.e., `G` has a clique of size `k`.

By the lemma (⇒), `G̅` has a vertex cover of size `n - k`. So `⟨G̅, n-k⟩ ∈ VERTEX-COVER`. ✓

**(4) No → No:** Assume `⟨G, k⟩ ∉ CLIQUE`, i.e., `G` has no clique of size `k`.

By the contrapositive of the lemma (⇐): if `G̅` had a vertex cover of size `n - k`, then `G` would have a clique of size `k` — a contradiction. Therefore `G̅` has no vertex cover of size `n - k`. So `⟨G̅, n-k⟩ ∉ VERTEX-COVER`. ✓

**Therefore `CLIQUE ≤_p VERTEX-COVER`, and `VERTEX-COVER` is NP-hard.** □

---

### Conclusion

Since `VERTEX-COVER ∈ NP` (Part 1) and `VERTEX-COVER` is NP-hard (Part 2), `VERTEX-COVER` is NP-complete. □

---

## What to Notice

- **The lemma did the heavy lifting.** The actual reduction function `f` is just one line — take the complement and flip `k` to `n - k`. The hard part was proving the lemma that makes Yes→Yes and No→No obvious once you have it. In complex proofs, isolating the key structural insight as a named lemma keeps the proof readable.
- **No→No used the contrapositive of the lemma**, not the lemma directly. Recognize when contrapositive is cleaner (step 4).
- **The complement graph is a common bridge** between clique-style and cover-style problems. `G` has a clique ⟺ `G̅` has an independent set ⟺ `G̅`'s complement (`G`) has a vertex cover. These relationships form a web you can exploit.
- **Two-part structure is mandatory.** Label Part 1 and Part 2 explicitly in every NP-completeness proof. Examiners and reviewers look for this structure.

---

## The Complete NP-Completeness Proof Checklist

Before declaring a proof complete, verify every item:

**Part 1 — NP Membership**
- [ ] Certificate described concretely
- [ ] Certificate length bounded by a polynomial in `|w|`
- [ ] Verifier described step by step
- [ ] Each step's time bounded; total is polynomial
- [ ] Correctness (⇒): if `w ∈ L`, the certificate exists and `V` accepts
- [ ] Correctness (⇐): if `V` accepts, then `w ∈ L`

**Part 2 — NP-Hardness**
- [ ] Source language is known NP-hard (cite the result)
- [ ] Reduction function `f` described explicitly
- [ ] `f` runs in polynomial time (argued, not assumed)
- [ ] `f` is total
- [ ] Yes→Yes proved
- [ ] No→No proved
- [ ] Conclusion: source is NP-hard and reduces to target, so target is NP-hard

**Final line**
- [ ] "Since [B] ∈ NP and [B] is NP-hard, [B] is NP-complete."

---

## Full Reduction Landscape (Steps 15–20)

```
        A_TM (undecidable — step 15)
           |
        HALT (undecidable — step 16)
           |
     REGULAR_TM (undecidable — step 17)

  -------- decidability boundary --------

        3-SAT (NP-complete — Cook-Levin)
           |
        CLIQUE (NP-complete — step 19)
           |
    VERTEX-COVER (NP-complete — step 20)
    INDEPENDENT-SET (NP-complete — practice)
    HAM-PATH, SUBSET-SUM, ... (NP-complete)
           |
          P?
    (open: does P = NP?)
```

---

## Practice Problems

1. **INDEPENDENT-SET is NP-complete.** Define:
   ```
   INDEPENDENT-SET = { ⟨G, k⟩ : G has an independent set of size k }
   ```
   Prove NP-completeness in two parts:
   - Part 1: Prove `INDEPENDENT-SET ∈ NP`. Describe the certificate and verifier.
   - Part 2: Prove NP-hardness by reducing `CLIQUE ≤_p INDEPENDENT-SET` using the complement graph. (Same lemma structure as this step.)

2. **HAM-PATH is NP-complete (membership only).** Define:
   ```
   HAM-PATH = { ⟨G, s, t⟩ : G has a Hamiltonian path from s to t }
   ```
   Prove `HAM-PATH ∈ NP`. You do not need to prove hardness — focus on getting Part 1 exactly right: certificate, length, verifier, time, correctness in both directions.

3. **Hardness without a lemma.** For `CLIQUE ≤_p VERTEX-COVER`, the proof used a clean structural lemma. But the Yes→Yes and No→No directions could also have been proved directly without naming the lemma.
   - Rewrite the Yes→Yes direction without citing the lemma — prove it from first principles.
   - Rewrite the No→No direction without citing the lemma — use contradiction directly.
   - Compare the two versions. Which is cleaner and why?
