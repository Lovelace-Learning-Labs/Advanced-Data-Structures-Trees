@snap[midpoint span-100]

# B-Trees

### Design

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

---

## Big Ordered Dictionary

Records are key-value pairs

Operations: insert, lookup by key, iterate

Can store more records than fit in main memory

Performance goal: minimize **number of disk accesses**

<p class="small">Processor time for lookup and insert should still be `\(O(log(n))\)`</p>

---

## Inspiration

Consider the data structures we've learned about so far

Can any of them implement the big ordered dictionary interface easily?

If not, what inspiration can we draw from those other data structures?

---

## Features

Balanced, sorted trees have `\(O(log(n))\)` insert and lookup

None of the DS we've studied address disk accesses

<br>

<div class="fragment">
<p>Tries have wide nodes - maybe we can expand that to the size of a page?</p>

<p class="small">How to keep track of which child is which?</p>
</div>

---

## B-Tree Terms

`\(d\)` - degree of a node

<p class="small">The number of children that node has</p>

`\(t\)` - minimum degree of a tree

<p class="small">The minimum number of children any node (except the root) may have</p>

`\(2t\)` - maximum degree of a tree

<p class="small">The max number of children any node may have, always twice the min degree</p>

`\[t \leq d \leq 2t\]`

---

## B-Tree Nodes

3 parallel arrays: `\(d\)` `children`, `\(d-1\)` `keys` / `values`

Keys "separate" children

![](b-trees/images/btree-node.png)

---

## Leaf Nodes

A leaf node contains only keys/values, no children

<p class="small">The bottom layer of the tree</p>

We still say the node has `\(d-1\)` keys

<br>

This is different than the definition we used for red-black trees!

---

## B-Tree Property

<p class="small">Let `node` be any non-leaf node. Then for each index `\(0 \leq i \lt d-1\)`...</p>

<ul class="small">
<li>All keys in the subtree at `node.children[i]` are less than `node.keys[i]`</li>
<li>All keys in the subtree at `node.children[i+1]` are greater than `node.keys[i]`</li>
</ul>

![](b-trees/images/btree-node.png)

---

## B-Tree Logic

<ul class="small">
<li>All keys under `node.children[i] < node.keys[i]`</li>
<li>All keys under `node.children[i+1] > node.keys[i]`</li>
</ul>

<br>

What does this tell us about the relationship between...

<ul class="small">
<li>`node.keys[i]` and keys to the left or right?</li>
<li>`node.keys[i]` and keys in `node`'s left or right sibling?</li>
<li>`node.keys[i]` and keys in children of `node.children[i]` or `node.children[i+1]`?</li>
</ul>

---

## B-Tree Logic

<ul class="small">
<li>All keys under `node.children[i] < node.keys[i]`</li>
<li>All keys under `node.children[i+1] > node.keys[i]`</li>
</ul>

<br>

We can conclude...

<ul class="small">
<li>Keys within a node are sorted left to right</li>
<li>All keys in a node's left sibling come before all keys in that node, and all keys in the right sibling come after</li>
<li>Keys in grandchildren "follow the pattern"</li>
</ul>

---

## B-Tree Property

Here is a B-Tree containing integers between 1 and 41

![](b-trees/images/btree-full.png)

<!-- https://www.codeproject.com/Articles/1158559/B-Tree-Another-Implementation-By-Java -->

- What is the minimum degree?
- Does it follow the B-Tree Property?

---

## B-Trees and BSTs

Compare the **B-Tree property**

<p class="small">Let `node` be any non-leaf node. Then for each index `\(0 \leq i \lt d-1\)`...</p>

<ul class="small">
<li>All keys under `node.children[i] < node.keys[i]`</li>
<li>All keys under `node.children[i+1] > node.keys[i]`</li>
</ul>

With the **BST property**

<p class="small">For every node...
<ul class="small">
<li>All nodes under `node.left` have a key less than that node's key</li>
<li>All nodes under `node.right` have a greater key</li>
</ul>

<p class="fragment">A B-Tree with minimum degree `\(t=1\)` is a BST!</p>

---

## Leaf Keys

A leaf has keys and values but no children!

<p class="small">B-Tree property doesn't make sense</p>

Keys in a leaf are sorted from smallest to largest

<p class="small">Does this "follow the pattern"?</p>

---

## Leaf Depths

Every leaf in a B-Tree must have the same depth

<ul class="small">
<li>What does this tell us about balance?</li>
<li>What can we conclude about the height `\(h\)` of a B-Tree with `\(n\)` records?</li>
</ul>

<p class="fragment">`\[h = O(log(n))\]`</p>

<br>
<p class="fragment">How does this compare to the red-black tree rules?</p>

---

## B-Tree Leaves

Consider the leaves in our B-Tree

![](b-trees/images/btree-full.png)

<!-- https://www.codeproject.com/Articles/1158559/B-Tree-Another-Implementation-By-Java -->

- Are leaf keys in sorted order?
- Are the leaves all at the same depth?

