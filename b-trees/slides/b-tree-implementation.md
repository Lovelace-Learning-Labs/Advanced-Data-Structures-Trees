@snap[midpoint span-100]

# B-Trees

### Implementation and Analysis

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

* **Implement** the B-Tree lookup and insert algorithms
* **State** the runtime of those algorithms using big-O notation
* **Describe** how the insert algorithm keeps a B-Tree balanced

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

## B-Tree Tuning

The minimum degree `\(t\)` has a big impact on its structure

- Large `\(t\)` `->` more records per node `->` fewer nodes
- Large `\(t\)` `->` more children per node `->` shorter tree
- If `\(t\)` is too big our tree starts to act like an array

Idea: select `\(t\)` so that the **max size of a node** (`\(d=2t\)`) is as close to the **size of a page** as possible without going over

<p class="small">Typical values of `\(t\)` are between 10 and 100</p>

---

## Lookup

Similar to BST lookup

Walk down the tree, selecting the "correct" child of each node on the path

<p class="small">Search through keys to find the right index</p>

When you find the key you're looking for or run out of nodes, you're done

---

## Lookup

```ruby
def findIndex(node, key)
  # Or use binary search! Our analysis will assume this.
  i = 0
  while i < node.keys.length and node.keys[i] < key
    i += 1
  return i

def lookup(key)
  node = root

  while true
    i = findIndex(node, key)

    if i < node.keys.length and node.keys[i] == key
      return node.values[i]
    elsif node.isLeaf
      return undefined
    else
      node = node.children[i]
```

---

## Lookup Analysis

Number of nodes inspected: `\(O(log_t(n))\)`

Work per node: `\(O(log_2(t))\)`

`\[ \text{lookup time} = O(log_2(t)) * O(log_t(n) ) \\ = O\left(log_2(t) * \frac{log_2(n)}{log_2(t)}\right) \\ = O(log(n)) \]`

<br>

Needs `\(O(t)\)` space to load one node at a time into memory

---

## Lookup Disk Access

Our algorithm uses a single pass to walk down the tree

The number of disk reads is the number of nodes visited, is the height of the tree

Keeping `\(t\)` large keeps this number small

---

## Insert

**Idea:** Walk down the tree to the correct leaf, insert the key and values into the middle of the array

```ruby
def insert(key, value)
  node = root
  while true
    index = findIndex(node, key)

    if node.isLeaf
      node.keys.insertAt(index, key)
      node.values.insertAt(index, value)
      break

    else
      child = node.children[index]
      if child.degree == 2 * t
        # Uh oh, child is full
      node = child
```

---

## Insert

**Problem:** What if the leaf node is full (`\(d=2t\)`)?

@snap[fragment]

<p class="small">Split the full node into two half-full nodes (`\(d=t\)`), promote the center key to the parent, then insert on the left or right side as appropriate</p>

What if the parent is also full?
@snapend

@snap[fragment small]
We don't want to backtrack, that will require extra disk access

Split as you walk down the tree, whenever you find a full node
@snapend

---

@snap[midpoint span-100]
`splitChild(parent, 2)`

![](b-trees/images/btree-split-child.png)
@snapend

---

## Insert Revised

```ruby
def insert(key, value)
  if root.degree == 2 * t
    newRoot = new Node(isLeaf: false, children: [root])
    splitChild(newRoot, 0)
    root = newRoot

  node = root
  while true
    index = findIndex(node, key)
    if node.isLeaf
      # as before
    else
      child = node.children[index]
      if child.degree == 2 * t
        splitChild(node, index)
        if key > node.keys[index]
          child = node.children[index + 1]

      node = child
```

---

## Record Flow

Insert always adds a record to a leaf

The only way for records to move up the tree is when a full node splits

When the root is full, the algorithm splits it and adds a new layer to the tree

---

## Insert Analysis

Splitting a node takes `\(O(t)\)` time

<p class="small">Copy `\(O(t)\)` records from child to sibling</p>

Insert looks at `\(O(log(n))\)` nodes

<p class="small">In the worst case it must split all of them</p>

Insert takes `\(O(t*log(n))\)` time

<br>

Space is `\(O(t)\)`

---

## Insert Disk Access

Because we split nodes preemptively, our algorithm avoids backtracking

The number of disk reads is the number of nodes visited, is linear in the height of the tree

Similar to lookup

---

## Insert and Balance

Does our insert algorithm keep the B-Tree **balanced**?

<p class="small">Requirement: every leaf has the same depth</p>

@snap[fragment]
**Yes!**

Adding a record to a non-empty node doesn't change its depth

Splitting a node keeps its children at the same depth

When we split the root, the depth of every node increases by one
@snapend

---

## Summary

Lookup is similar to BST lookup

Insert is more complicated because we split full nodes

<p class="small">We split preemptively to avoid backtracking</p>

Insert keeps the B-Tree balanced

| Operation | Time              | Space      | Disk Accesses             |
| --------- | ----------------- | ---------- | ------------------------- |
| Lookup    | `\(O(log(n))\)`   | `\(O(t)\)` | `\(O(log(n))\)` (minimal) |
| Insert    | `\(O(t*log(n))\)` | `\(O(t)\)` | `\(O(log(n))\)` (minimal) |

Iterate (implementation and analysis) is up to you!
