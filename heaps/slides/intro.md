@snap[midpoint span-100]

# Heaps

### Introduction

@snapend

---

## Overview

Interface: **priority queue**

<p class="small">Each record has a priority, records are removed in priority order</p>

<br>

Data structure: **heap**

<p class="small">Binary tree, but not a binary search tree</p>

<p class="small">Implemented using an array</p>

---

## Naming

"Heap" presents a naming collision!

<p class="fragment">**Heap data structure**: binary tree implemented using an array</p>

<p class="fragment">The **program heap**: unstructured memory where the JS interpreter stores our objects</p>

<p class="small fragment">The two have nothing to do with each other (the heap is not implemented using a heap)</p>

---

## Constraints

Heaps are a relatively straightforward data structure

<p class="small">So this week we'll add in a constraint!</p>

<div class="fragment">
<p>**No allocation** on the program heap allowed after initialization</p>
<p class="small">Could come up in operating systems (e.g. process scheduler), embedded systems</p>
</div>

---

## Heapsort

We'll look at an algorithm called **heapsort**

Heapsort takes an array of `\(n\)` records...

And, by turning it into a heap...

Sorts it in-place in `\(O(n*log(n))\)` time 

---

## Stack and Heap

Call stack and program heap

Last section is an optional deep-dive

Gives context to some of what we're talking about

---

## Summary

We will use the **heap** data structure to implement the **priority queue** interface

Constraint: our DS cannot allocate memory after initialization

We will finish with the **heapsort** algorithm

A heap data structure is different from the program heap, where objects are allocated
