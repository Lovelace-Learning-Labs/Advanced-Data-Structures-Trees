@snap[midpoint span-100]

# Priority Queue

### Interface

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

---

## Priority Queue

Records are pairs: element + priority

Operations: insert, remove max

<p class="small">Both `\(O(log(n))\)` for a p-queue with `\(n\)` records</p>

Has a fixed capacity, no allocation allowed after initialization

---

## Inspiration

Consider the data structures we've learned about so far. Can any of them implement the priority queue interface easily?

If not, what inspiration can we draw from those other data structures?

---

## Features

Red-black trees have `\(O(log(n))\)` insert and remove

<ul class="small">
<li>Records are sorted</li>
<li>Tree is balanced</li>
</ul>

Arrays are a good way to store a fixed number of elements

<p class="fragment">Idea: make a tree out of an array</p>

---

## 

---

## Summary

---

## Vocab