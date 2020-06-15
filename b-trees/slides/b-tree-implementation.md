@snap[midpoint span-100]

# B-Trees

### Implementation and Analysis

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

## B-Tree Tuning



---


## Lookup

```ruby
def findIndex(node, key)
  # Or use binary search!
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


`\[
\text{lookup time} = O(log_2(t)) * O(log_t(n) ) \\
= O\left(log_2(t) * \frac{log_2(n)}{log_2(t)}\right) \\
= O(log(n))
\]`

<br>

Needs `\(O(t)\)` space to load one node at a time into memory

---

## Lookup Disk Access

Our algorithm uses a single pass to walk down the tree

The number of disk reads is the number of nodes visited, is the height of the tree

Keeping `\(t\)` large keeps this number small
