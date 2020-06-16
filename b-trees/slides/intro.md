@snap[midpoint span-100]

# B-Trees

### Introduction

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

* **List** key concepts for our discussion of B-Trees
* **Recall** the details of the ordered dictionary interface

---

## Interface

Interface: **big ordered dictionary**

Same as our ordered dictionary from weeks 2 and 3

<p class="small">Maps keys to values, maintains sorted order</p>

Question: How can we handle more records than fit in memory?

Application: Database indexing

---

## Ordered Dictionary

**Records** are key-value pairs

@snap[small]
- Keys are fixed-size, like an integer, date or short string
- Values are references (e.g. location of a DB record on disk)
@snapend

**Supported Operations**

<ul class="small">
<li>Insert a new key-value pair in `\(O(log(n))\)` time</li>
<li>Lookup a value by key in `\(O(log(n))\)` time</li>
<li>Iterate through records in sorted order in `\(O(n)\)` time</li>
</ul>

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

## Memory Swapping

B-Trees are designed to store more records than fit in main memory

To give context, we'll start with a discussion of **memory swapping and paging**, and the way that the operating system manages memory and disk space

How can we leverage this knowledge to build an efficient data structure?

---

## Summary

**Application:** database indexing

**Interface:** big ordered dictionary

**Implementation:** B-Tree

**Additional Consideration:** large-scale memory management
