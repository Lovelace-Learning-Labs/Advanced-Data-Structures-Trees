@snap[midpoint span-100]

# Heap

### Implementation

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

* **Explain** how to build a heap from an unsorted list
* **Demonstrate** how to turn a max-heap into a sorted array
* **Express** the time and space complexity of heapsort in big-O notation

---

## Heapsort

We can use a heap to sort an array of `\(n\)` records in `\(O(n*log(n))\)` time

<p class="small">Basic idea: `\(n\)` inserts at `\(O(log(n))\)` each, then `\(n\)` removes also at `\(O(log(n))\)`</p>

<p class="small">We could do this with a red-black tree too!</p>

The advantage of heapsort is that it's in-place!

---

## Building the Heap

Observation: an array of size 1 is a valid heap

Idea: build up subtrees iteratively by merging heaps

<p class="small">Sinking the subtree root if needed</p>

Similar to mergesort

---

## Building the Heap

![](heaps/images/heapsort-build-heap.png)

---

## Build Heap Pseudocode

```ruby
def buildheap(array)
  midpoint = Math.floor(array.length / 2)
  for i = midpoint down to 1
    sink(i)
```

---


Sum from i = 1 to log_2(n) of:

n / 2^i * i

---

## Summary