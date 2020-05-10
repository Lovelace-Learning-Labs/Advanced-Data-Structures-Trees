@snap[midpoint]

# Binary Search Trees

### Design

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Define** the terms linear search, binary search, binary search tree, root, parent, child, ancestor, descendant, subtree
- **Explain** why previously studied data structures aren't sufficient to implement a fast ordered dictionary
- **Use** binary search to find an element in a sorted array on `\(log(n)\)` time
- **Describe** the structure of a binary search tree

---

## Is It Easy?

Think about the data structures we've seen so far

<ul class="small">
<li>Array</li>
<li>Linked list</li>
<li>Hash</li>
</ul>

Can we use any of these to solve the problem without inventing something?

If not, what can we learn from them?

---

## Arrays

Could store elements in **insertion order**

<p class="small">Insert is `\(O(1)\)`, but lookup is `\(O(n)\)` and iterate is `\(O(n*log(n))\)`</p>

<br>

<div class="fragment">
<p>Could store elements in **sorted order**</p>

<p class="small">Lookup is `\(O(log(n))\)` via binary search, iterate is `\(O(n)\)`</p>
<p class="small">Insert is `\(O(n)\)` - need to search for the right spot, move following records to make a hole</p>
</div>

---

## Linked Lists

Once we know where to put it, adding a node is `\(O(1)\)`

Lookup by key is always `\(O(n)\)`

Linked lists really only work for stacks and queues

Maybe we can take some of the principles and apply them elsewhere...

---

## Hash

Insert and lookup are constant!

Iterate is `\(O(n*log(n))\)` - need to sort first

Not too useful - we have to make too many tradeoffs to get constant access

---

## Learn from Experience

Records must be **stored in sorted order**

<ul class="small">
<li>Otherwise iterate requires an `\(O(n*log(n))\)` sort</li>
<li>Lets us use **binary search** for `\(O(log(n))\)` lookups</li>
</ul>

<div class="fragment">
<p>Maybe we could **store records in nodes**</p>
<ul class="small">
<li>Similar to a linked list</li>
<li>Insert could be an `\(O(log(n))\)` lookup plus an `\(O(1)\)` node add</li>
<li>Lookup and delete are similarly `\(O(log(n))\)`</li>
</ul>
</div>

<p class="fragment">Plan: a **linked** data structure that supports **binary search**</p>

---

## Search Review

The core idea of binary search is essential to understanding trees, so let's review it before going further

---

## Linear Search

Imagine we have a sorted array of integers, and we want to check whether it contains the value `42`. How do we find out?

**Linear search**: start on the left, look at values one by one until you find your target or run out of array.

![](binary-trees/images/array-linear-search.png)

What is the time complexity of linear search? `\(O(n)\)`

---

## Binary Search

If our array is sorted, we can do better!

![](binary-trees/images/array-binary-search.png)

Binary search is `\(O(log(n))\)`

`\(log_2(n)\)`: how many times can you cut `\(n\)` in half?

---

## Binary Search

We can think of binary search as following a "path" through the data

![](binary-trees/images/array-to-bst.png)

<p class="small">Go right, then left, then right</p>

---

## Binary Search Tree

If we turn each potential "decision point" in the path into a node, we have a **binary search tree**

![](binary-trees/images/bst-transformed.png)

---

![wide](binary-trees/images/TreeVocabulary.png)

@snap[south span-100]
We will use a slightly different definition of **leaf**
@snapend

---

## Subtrees

A subtree consists of a node an all its descendants

<p class="small">Every subtree is itself a binary search tree</p>

<p class="small">That means **recursion** will be a useful tool</p>

A node's **left subtree** is the subtree **rooted** at the node's **left child**

<p class="small">Its "right subtree" is rooted at its right child</p>

**Question**: can a node's left and right subtrees ever share a node?

---

## BST Property

For every node...

All nodes in the node's left subtree have a key less than that node's key

All nodes in the right subtree have a greater key

@snap[south span-100]
![](binary-trees/images/bst-transformed.png)
@snapend

---

## Balance

A tree (or subtree) is **balanced** if it has close to the same number of descendants on its left as on its right

<p class="small">As we'll see, balance is key for performance</p>

We'll give a more rigorous definition of balance later

---

## BST Visualizer

https://www.cs.usfca.edu/~galles/visualization/BST.html

---

## Summary

Previously studied data structures aren't a good fit for the ordered dictionary interface

A **binary search tree** takes the idea behind binary search and turns it into a **linked** data structure

<p class="small">Linked data structures usually support fast random insert and delete</p>

Each node stores a key-value pair, and has links to up to two child nodes, `left` and `right`

For every node, all keys in the left subtree are less than its key, and all keys in the right subtree are greater

---

## Vocab 1

| Term               | Definition                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------- |
| Linear search      | Search by scanning through a list left to right, takes `\(O(n)\)` time for a list of size `\(n\)` |
| Binary search      | Splitting a list in half repeatedly, takes `\(O(log(n))\)` time for a list of size `\(n\)`        |
| Tree               | A linked data structure where each node links to two or more child nodes                          |
| Binary search tree | A tree organized to promote binary search                                                         |

---

## Vocab 2

| Term       | Definition                                             |
| ---------- | ------------------------------------------------------ |
| Root       | The top-most node in a tree                            |
| Parent     | The node directly above a given node                   |
| Ancestor   | Any node on the path between a given node and the root |
| Child      | A node directly below a given node                     |
| Descendant | Any of a node's children, its children's children, etc |
| Subtree    | A node and all its descendants                         |
