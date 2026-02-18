---
name: dsa-challenge
description: Get a deep, mind-expanding coding challenge on data structures and algorithms. Includes theory, real-world applications, academic papers, and a hands-on problem. Use when you want to practice DSA or learn something new.
argument-hint: [topic]
allowed-tools: WebSearch, WebFetch
---

# DSA Challenge

Generate a rich, mind-expanding coding challenge centered on data structures and algorithms.

## Arguments

- `$ARGUMENTS` - (Optional) A specific topic or area of interest (e.g., "trees", "graphs", "hashing", "concurrent data structures"). If not provided, pick a random deep topic.

## Steps

### 1. Pick a Topic

If the user provided a topic in `$ARGUMENTS`, use it as a starting point but go deeper into a specific sub-area that's non-obvious and thought-provoking.

If no topic is provided, pick one at random from a diverse pool. Rotate through categories to avoid repetition — don't always pick the "popular" ones. Draw from areas like:

- Persistent data structures (fat nodes, path copying)
- Probabilistic data structures (Bloom filters, Count-Min Sketch, HyperLogLog, skip lists)
- Self-balancing trees (red-black, AVL, splay, treaps, scapegoat trees)
- Graph algorithms (flow networks, planarity testing, spectral methods, expander graphs)
- Succinct / compressed data structures (wavelet trees, FM-index, rank/select)
- Concurrent & lock-free data structures (lock-free queues, hazard pointers, epoch-based reclamation)
- Cache-oblivious data structures (van Emde Boas layout, cache-oblivious B-trees)
- Spatial data structures (R-trees, k-d trees, locality-sensitive hashing)
- String algorithms & data structures (suffix arrays, suffix automata, Aho-Corasick, BWT)
- Amortized / online algorithms (splay tree amortized analysis, competitive analysis)
- Randomized algorithms (treaps, randomized incremental construction, random sampling)
- External memory / streaming algorithms (external merge sort, reservoir sampling, streaming median)
- Algebraic data structures (monoids in segment trees, tropical semirings, Fenwick trees)

Pick something that will genuinely expand the user's thinking.

### 2. Search for Academic Context

Use WebSearch to find:
- The original academic paper or seminal reference for the chosen data structure/algorithm
- A recent paper or blog post showing a modern application or improvement
- Any relevant survey papers

Search queries should be specific, e.g.:
- `"<data structure name>" original paper site:arxiv.org OR site:dl.acm.org`
- `"<data structure name>" applications real-world`
- `"<data structure name>" tutorial explanation`

Use WebFetch on promising results to extract key insights, definitions, and complexity bounds.

### 3. Present the Challenge

Structure the output in this exact format:

---

**DSA Challenge: [Title]**

**The Data Structure / Algorithm**
- What it is, in 2-3 clear sentences. Define it formally but accessibly.
- Key properties and invariants.
- Time and space complexity for core operations (insert, delete, query, etc.) presented in a small table.

**Theoretical Foundation**
- Who invented it, when, and why.
- The core insight or "aha moment" behind the design.
- Link to the original paper with a 1-2 sentence summary of its contribution.
- Link to a modern paper or resource that extends or applies it.

**Where It's Actually Used**
- 2-3 concrete real-world systems or products that use this (e.g., "Redis uses HyperLogLog for cardinality estimation", "Google's Bigtable uses Bloom filters to avoid unnecessary disk reads").
- Why it's chosen over alternatives in those systems — what tradeoff makes it win.

**The Problem**

Present a coding problem that requires understanding and implementing the data structure or algorithm. The problem should:
- Have a clear problem statement with input/output format
- Include 2-3 examples (input -> expected output)
- Have constraints that make a naive approach infeasible (forcing the use of the target data structure)
- Include a follow-up / bonus that pushes deeper (e.g., "now make it persistent", "now handle concurrent access", "now optimize for cache performance")

**Hints** (collapsed — tell the user to ask if they want hints)
- Do NOT show hints by default. Just mention: "Ask me for hints if you get stuck — I have 3 levels of hints ready."
- Internally, prepare 3 levels:
  - Level 1: A conceptual nudge (which data structure family to consider)
  - Level 2: The specific approach and key operations needed
  - Level 3: Pseudocode outline

**Further Reading**
- 2-3 links to papers, blog posts, or visualizations for deeper exploration.

---

### 4. Tone and Style

- Be genuinely enthusiastic about the elegance of the topic. These are beautiful ideas.
- Don't dumb it down, but do make it accessible. Assume the reader is a strong programmer who may not have seen this specific topic.
- Use precise terminology but always explain it inline.
- Make the problem feel like a real engineering challenge, not a textbook exercise.
