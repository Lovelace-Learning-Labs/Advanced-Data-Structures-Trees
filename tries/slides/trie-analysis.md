@snap[midpoint span-100]

# Trie

### Analysis

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Name** the terms that affect trie performance
- **Describe** the time and space complexity of trie operations using big-O notation

---

@snap[north-west span-60]

## Trie Design

Each node has one child for each radix in our code alphabet

Each node stores a list of words matching that code

To lookup by code, walk down the trie one radix at a time

<ul class="small">
<li>Lookup by prefix: lookup, then gather all matches in the subtree</li>
<li>Insert: lookup but create missing nodes</li>
</ul>
@snapend

@snap[east span-30]
![](tries/images/trie-links.png)
@snapend

---

## Terms

What is important for analyzing tries?

| Term         | Meaning                                            |
| ------------ | -------------------------------------------------- |
| `\(n\)`      | Number of words (not nodes) in the trie            |
| `\(k\)`      | Average length of a code in the trie, typically ~5 |
| `\(max(k)\)` | Max length of a code in the trie, typically ~20    |
| `\(c\)`      | Length of the code being inserted or looked up     |
| `\(m\)`      | Number of words matching a code or prefix          |
| `\(r\)`      | Number of radixes in code alphabet                 |

<br class="small">

<p>We will treat `\(k\)` and `\(max(k)\)` like constants</p>

---

## Lookup by Code

```ruby
def lookupCode(code)
  node = root
  for radix in code
    node = node.children[radix]
    return [] if node is undefined
  return node.words
```

What is the time complexity of looking up a code of length `\(c\)` in a trie containing `\(n\)` words?

<ul class="fragment">
<li>We inspect at most `\(c\)` nodes</li>
<li>Inspecting a node is `\(O(1)\)`</li>
<li>`lookupCode` is `\(O(c)\)`</li>
<li>Space is constant</li>
</ul>

---

## Lookup by Prefix

Similar to lookup

<p class="small">Once you find a matching node iterate through its subtrie to collect all `\(m\)` matching words</p>

How many nodes in the subtrie?

`\[\text{subtrie size} \leq m*(max(k)-c) = O(m)\]`

<ul class="fragment">
<li>Finding the node is `\(O(c)\)`</li>
<li>Iterating through the subtrie takes `\(O(m)\)` time</li>
<li>Lookup by prefix is `\(O(c + m)\)`</li>
<li>Space is `\(O(m)\)` (output array)</li>
</ul>

---

## Insert

Walk down a path of length `\(c\)`, creating missing nodes as you go

Insert is `\(O(c)\)` time

Allocates up to `\(O(c)\)` space

<p class="small">Assumes code generation is `\(\leq O(c)\)`</p>

---

## Trie Space

Difficult to express because codes overlap

| Type  | Bound              | Description                    |
| ----- | ------------------ | ------------------------------ |
| Lower | `\(n\)`            | space to store `\(n\)` words   |
| Upper | `\(r^{ max(k) }\)` | number of possible codes       |
| Upper | `\(n*k\)`          | node count if no codes overlap |

<br>

Since `\(k\)` is typically a small constant, we can say a trie takes `\(O(n)\)` space

---

## Summary

`\(c\)` is code length, `\(m\)` is number of matches

| Operation      | Time           | Space      |
| -------------- | -------------- | ---------- |
| Lookup code    | `\(O(c)\)`     | constant   |
| Lookup prefix  | `\(O(c + m)\)` | `\(O(m)\)` |
| Insert one     | `\(O(c)\)`     | `\(O(c)\)` |
| Insert `\(n\)` | `\(O(n * c)\)` | `\(O(n)\)` |

<br>

Key takeaway: trie time complexity is **independent of the number of records**
