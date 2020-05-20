@snap[midpoint span-100]

# Priority Queue

### Interface

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Describe** the operations of the priority queue interface
- **List** the additional constraints we've added for this week
- **Differentiate** between queues and priority queues

---

## Problem

Operating system's process scheduler

<ul class="small">
<li>Each process has a **priority** (positive integer)</li>
<li>Only one process can run at a time</li>
<li>When one process is done, the next process to run should be the one with the highest priority</li>
<li>The system limits the number of processes to 1024</li>
</ul>

We'll call the DS that tracks waiting processes a **priority queue**

---

## Interface Questions

Pause the video and consider the following questions about our **priority queue** interface:

- What **type of records** are we storing?
- What **operations** do we need to support?
- What (if any) **ordering** do we maintain?
- What **use pattern** do we expect?

---

## Priority Queue

Records are pairs: element + priority

Operations:

<ul class="small">
<li>Insert a process with a given priority</li>
<li>Remove the highest-priority process from the queue</li>
</ul>

Ordered by priority

We expect **mixed** inserts and removes

Has a **fixed capacity**

<p class="small">Attempting to insert into a full queue results in an error</p>

---

## Constraint

The priority queue **cannot allocate memory** on the program heap

<p class="small">Stack variables are OK</p>

This is a typical constraint in operating systems problems

<ul class="small">
<li>Maybe the system has a fixed amount of kernel memory</li>
<li>Maybe allocation is too slow</li>
<li>What to do if allocation fails?</li>
</ul>

---

## Performance

Let `\(c\)` be the capacity of the priority queue, and `\(n\)` the number of records currently stored. Then we have

`\[
n \leq c = 1024
\]`

Insert and remove should each be `\(O(log(n))\)`

<p class="small">What does this imply about balance?</p>

The whole data structure should always take `\(O(c)\)` space

No operation should take more than constant space

---

## Queues and P-Queues

We've talked about queues already

How is a priority queue different from a regular queue?

<ul class="fragment">
<li>Each record has a priority</li>
<li>Insertion order doesn't matter</li>
<li>P-queue lacks support for ordered iteration, cancel</li>
<li>Performance constraints not at all the same</li>
</ul>

<p class="fragment">Though they solve a similar problem, they are very different</p>

---

## Summary

A **priority queue** associates a priority with each stored record

Records are removed from the queue in priority order

We have added two constraints:

<ul class="small">
<li>Fixed maximum capacity</li>
<li>No allocations after initialization</li>
</ul>