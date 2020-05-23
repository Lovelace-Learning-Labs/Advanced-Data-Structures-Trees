@snap[midpoint span-100]

# Heap

### Design

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

* **Identify** features of other data structures relevant to implementing priority queues
* **Describe** how to lay out the nodes of a tree in an array
* **Recite** the max-heap property

---

## Priority Queue

Records are pairs: element + priority

Operations: insert, remove max

<p class="small">Both `\(O(log(n))\)` for a p-queue with `\(n\)` records</p>

Fixed capacity, no allocation after initialization

---

## Inspiration

Consider the data structures we've learned about so far

Can any of them implement the priority queue interface easily?

If not, what inspiration can we draw from those other data structures?

---

## Features

Red-black trees have `\(O(log(n))\)` insert and remove

<ul class="small">
<li>Records are sorted</li>
<li>Tree is balanced</li>
</ul>

Arrays are a good way to store a fixed number of elements

<p class="fragment">Idea: make a binary tree out of an array</p>

---

## Aspects of Design

Idea: make a binary tree out of an array

We will talk about

- Layout
- Balance
- Max-heap property

---

## Array Tree

Root goes at index 1

For a record at index `\(i\)`

<ul class="small">
<li>Parent is at index `\(\left \lfloor{ \frac{i}{2} } \right \rfloor \)`</li>
<li>Left child is at index `\(2 * i\)`</li>
<li>Right child is at index `\(2 * i + 1\)`</li>
</ul>

![](heaps/images/heap-layout.png)

<em class="small">Note: these are indices, not priorities</em>

---

## Links

Let's consider the node at index 4. What index do its parent and children have?

![](heaps/images/heap-layout-node-4.png)

- Parent: `\(\left \lfloor{ \frac{i}{2} } \right \rfloor = 2\)`
- Left child: `\(2 * i = 8\)`
- Right child: `\(2 * i + 1 = 9\)`

---

## Arrays and Trees

We can view this data structure as either a tree or an array

@snap[south span-60]
![](heaps/images/heap-to-tree.png)
@snapend

---

## Perfect Balance

To avoid gaps, the tree must be perfectly balanced

<p class="small">Except for the bottom layer, which fills from left to right</p>

@snap[south span-80]
![](heaps/images/heap-to-tree-unbalance.png)
@snapend

---

## Max-Heap Property

The BST property is too strict

<p class="small">Since we don't support ordered iteration or random lookup / remove, we don't really need it</p>

<p class="small fragment">**Perfect balance** is more important than **perfect order**</p>

<div class="fragment">
<p>**Max-heap property**: every node has priority less than or equal to that of its parent</p>

<p class="small">That means the root has the highest priority</p>
</div>

<p class="small fragment">The heap diagrams we've seen so far showed indices, not priorities!</p>

---

## Max-Heap Example

@snap[south span-70]
![](heaps/images/heap-example.png)
@snapend

---

## Design Summary

Store tree nodes as elements in an **array**

<p class="small">Parent is at `\(\left \lfloor{ \frac{i}{2} } \right \rfloor \)`, children are at `\(2 * i\)` and `\(2 * i + 1\)`</p>

Keep the tree **perfectly balanced**

<p class="small">Bottom layer fills left-to-right</p>

Maintain the **max-heap property**:

<p class="small">Every node has priority less than or equal to that of its parent</p>

In the next module, we'll show how to implement insert and remove to satisfy these two properties
