@snap[midpoint span-100]

# B-Trees

### Tuning

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

---

## B-Tree Design

The **degree** `\(d\)` of a non-leaf node is its number of children

<p class="small">A node with `\(d\)` children stores `\(d-1\)` key-value pairs</p>

A B-Tree has **min degree** `\(t\)` and **max degree** `\(2t\)`

The **B-Tree property** is similar to the BST property

<ul class="small">
<li>All keys under `node.children[i] < node.keys[i]`</li>
<li>All keys under `node.children[i+1] > node.keys[i]`</li>
</ul>

All **leaf nodes** have the same **depth**

<p class="small">For a B-tree with `\(n\)` records, the height `\(h = O(log(n))\)`</p>

---

## B-Tree Design

![](b-trees/images/btree-full.png)

---

## Tuning

The minimum degree `\(t\)` has a big impact on the structure of a B-Tree

How can we select `\(t\)` to optimize performance?

---

## Width and Height

Wider nodes (i.e. larger values of `\(t\)`) means more nodes per tree layer, so the tree is shorter

Wide nodes contain more records, so you need fewer nodes overall

![](b-trees/images/btree-degree-comparison.png)

---

## Tree Heights

Assuming `\(d = t\)` for all nodes

| prop | records&nbsp;&nbsp;&nbsp;   | `\(t=2\)` | `\(t=11\)`  | `\(t=101\)` | `\(t=1001\)` |
| -------- | --------- | --------------- | ----------- | ----------- | ------------ |
| nodes    | 1 million | 1 million       | 100,000     | 10,000      | 1000         |
| height   | 1 million | 20              | 6           | 3           | 2            |
| nodes    | 1 billion | 1 billion       | 100,000,000 | 10,000,000  | 1,000,000    |
| height   | 1 billion | 30              | 9           | 5           | 3            |

<br>

`\(t\)` determines the _base_ of our logarithm

<p class="small">Bigger bases grow slower (by a constant factor)</p>

---

## Max `t`

If large values of `\(t\)` correspond to shallow trees, shouldn't we set `\(t\)` to something huge?

@snap[fragment]
No!

@math
<p>If `\(t > n\)`, our tree becomes an array</p>
@mathend

We'll start to lose the benefits of trees

Remember that memory comes in pages...
@snapend

---

## Choosing `t`

**Goal:** minimize the number of pages read on a walk from the root to a leaf

---

## Choosing `t`

**Goal:** minimize the number of pages read on a walk from the root to a leaf

**Idea:** get the max size of a node (`\(d=2t\)`) as close to the size of a page as possible without going over

<ul class="small">
<li>Each node requires exactly one disk read</li>
<li>We get the most possible info out of that read</li>
<li>Keeping `\(t\)` big minimizes the height of the tree</li>
</ul>

Workflow: read a page, figure out which page to read next, repeat

---

## Choosing `t` - Example

These values are typical for database indexing

<ul class="small">
<li>**Page size:** 4096 bytes (4KB)</li>
<li>**Key:** 4-byte integer</li>
<li>**Value:** 8-byte reference</li>
<li>**Child:** 8-byte reference</li>
<li>**Node overhead:** 4-byte integer to track current degree</li>
</ul>

`\[
4096 = 4 + 2t * 8 + (2t-1) * (4 + 8) \\
= 28t - 8 \\
t = 146
\]`

<p class="small">To store one million records, a B-Tree with `\(t=146\)` uses 6,900 nodes and has a max height of 3 (in the worst case)</p>

---

## Summary

The minimum degree `\(t\)` has a big impact on a B-Tree's structure and performance

Our goal is to select `\(t\)` to **minimize the number of pages read on a walk from the root to a leaf**

Idea: select `\(t\)` so that the **max size of a node** (`\(d=2t\)`) is as close to the **size of a page** as possible without going over

