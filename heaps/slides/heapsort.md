@snap[midpoint span-100]

# Heapsort

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Explain** how to build a heap from an unsorted list
- **Demonstrate** how to turn a max-heap into a sorted array
- **Express** the time and space complexity of heapsort in big-O notation
- **Compare** heapsort to other sorting algorithms

---

## Heapsort

We can use a heap to sort an array of `\(n\)` records in `\(O(n*log(n))\)` time

<p class="small">Basic idea: `\(n\)` inserts at `\(O(log(n))\)` each, then `\(n\)` removes also at `\(O(log(n))\)`</p>

<p class="small">Turns out we can do a little better at building the tree</p>

<p class="small">We could do this with a red-black tree too!</p>

The advantage of heapsort is that it's in-place!

<p class="small">Red-black tree sort would not be in-place</p>

---

## Building the Heap

Observation: an array of size 1 is a valid heap

Idea: build up subtrees iteratively by merging heaps

<p class="small">Sinking the subtree root if needed</p>

Similar idea to mergesort

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

`sink(i)` assumes that `left(i)` and `right(i)` are both valid heaps, and combines them into one big heap

---

## Build Heap Complexity

For an array of size `\(n\)`

**Space** is constant

<br>

**Time** has a clear **upper bound**: `\(O(n*log(n))\)`

<p class="small">`sink` is `\(O(log(n))\)`, we do `\(O(n)\)` of them</p>

Turns out we can do better!

---

## Build Heap Runtime

How many swaps to sink the root a subtree of height `\(h\)`?

<div class="fragment">`\[O(h)\]`</div>

<p class="fragment">How many subtrees of height `\(h\)`?</p>

<div class="fragment">`\[\left \lceil{ \frac{n}{2^h} } \right \rceil \]`</div>

<p class="fragment">What's the height of the biggest subtree?</p>

<div class="fragment">`\[\left \lfloor{ log(n) } \right \rfloor \]`</div>

---

## Build Heap Runtime

`\[ \displaystyle\sum_{h=0}^{\left \lfloor{ log(n) } \right \rfloor} \left \lceil{ \frac{n}{2^h} } \right \rceil * O(h) \]`

`\[ =O\left(n*\displaystyle\sum_{h=0}^{\left \lfloor{ log(n) } \right \rfloor} \frac{h}{2^h} \right) \]`

`\[ =O\left(n*2 \right) \]`

`\[ =O\left(n \right) \]`

@snap[south span-100 small]
I do not expect you to reproduce this math
@snapend

---

## Build Heap Runtime

Building a heap from an unordered array of size `\(n\)` takes `\(O(n)\)` time

<p class="small">Not `\(O(n*log(n))\)`</p>

<p class="small">That's a surprising and powerful result!</p>

---

## Sorting the Heap

Idea: call `removeMax` `\(n\)` times

`removeMax` procedure:

<ol class="small">
<li>Swap first and last records</li>
<li>Reduce count</li>
<li>Sink the new root</li>
</ol>

Leave the removed element at the end of the array

---

## Sorting the Heap

![](heaps/images/heapsort-remove.png)

---

## Sort Pseudocode

```ruby
def heapsort(array)
  buildheap(array)
  for i = array.length down to 1
    array[i] = removeMax(array)
```

Note: this assumes that the array has an empty slot at index 0

<p class="small">This week's lab matches this assumption</p>

---

## Sort Complexity

For an array of size `\(n\)`

**Space** is constant

<br>

**Time** is `\(O(n*log(n))\)`

<p class="small">No opportunity for fancy math this time</p>

---

## Heapsort

Build a heap from an unordered array: `\(O(n)\)`

Sort the heap using `removeMax`: `\(O(n*log(n))\)`

**Total time complexity:** `\(O(n*log(n))\)`

<p class="small">This is true in all cases (no pathological inputs)</p>

In-place (constant space)

Unstable (doesn't preserve order)

---

## Sort Comparison

Heapsort vs Quicksort vs Mergesort

| Sort | Best              | Average           | Worst             | In place? | Stable? |
| --------- | ----------------- | ----------------- | ----------------- | --------- | ------- |
| Heap  | `\(O(n*log(n))\)` | `\(O(n*log(n))\)` | `\(O(n*log(n))\)` | ✅        | ❌      |
| Quick | `\(O(n)\)`        | `\(O(n*log(n))\)` | `\(O(n^2)\)`      | ✅        | ❌      |
| Merge | `\(O(n*log(n))\)` | `\(O(n*log(n))\)` | `\(O(n*log(n))\)` | ❌        | ✅      |

<br>



---

## System Sort

In practice, **Quicksort beats Heapsort** on most input

<p class="small">Comes down to number of swaps - writes are more expensive than reads!</p>

<ul class="small">
<li>Quicksort makes a minimal number of swaps</li>
<li>Heapsort does a lot of swapping (think about all those sinks)</li>
</ul>

<div class="fragment">
<p>`Array.sort` is always **Quicksort**</p>

<p class="small">Possibly falls back to Heapsort on bad input</p>

<p>Both are **in-place** and **unstable**</p>
</div>

---

## Summary

Heapsort is a pretty good sorting algorithm

<ul class="small">
<li>Build a heap from an unordered array: `\(O(n)\)` (woah!)</li>
<li>Sort the heap using `removeMax`: `\(O(n*log(n))\)`</li>
<li>**Total time complexity:** `\(O(n*log(n))\)`</li>
<li>In-place, unstable</li>
</ul>

Quicksort does better on most inputs, but heapsort is a good fallback
