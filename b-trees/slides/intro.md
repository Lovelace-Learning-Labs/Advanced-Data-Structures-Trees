@snap[midpoint span-100]

# B-Trees

### Introduction

@snapend

---

## Learning Goals

By the end of this module, students will be able to...


---

## Interface

Interface: **big ordered dictionary**

Same as our ordered dictionary from weeks 2 and 3

<p class="small">Maps keys to values, maintains sorted order</p>

Question: How can we handle more records than fit in memory?

Application: Database indexing

---

## Implementation

Data structure: **B-tree**

<p class="small">"B" stands for many things!</p>

B-trees are...

<ul class="small">
<li>Ordered similar to a binary search tree</li>
<li>Non-binary (many children per node)</li>
<li>Optimized for working with secondary storage (disk drives)</li>
</ul>

---
