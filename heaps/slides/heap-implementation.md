@snap[midpoint span-100]

# Heap

### Implementation

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

* **Describe** the algorithm to insert a record into a max-heap
* **Describe** the algorithm to remove the highest-priority record from a max-heap

---

## Design Review

Store tree nodes as elements in an **array**

<p class="small">Parent is at `\(\left \lfloor{ \frac{i}{2} } \right \rfloor \)`, children are at `\(2 * i\)` and `\(2 * i + 1\)`</p>

Keep the tree **perfectly balanced**

<p class="small">Bottom layer fills left-to-right</p>

Maintain the **max-heap property**:

<p class="small">Every node has priority less than or equal to that of its parent</p>

---

## Insert Strategy

To keep the heap perfectly balanced, insert will always add a slot **at the end of the array**

![](heaps/images/heap-insert-plan.png)

Inserting the new record here might violate the **max-heap property**

---

## Float Up

Our newly inserted record might have a higher priority than its parent

Idea: "float" the record up the tree until we find the right spot

<p class="small">Repeatedly swap with the parent</p>

---

## Float Up

![](heaps/images/heap-float-up.png)

---

## Float Pseudocode

```ruby zoom-12
def float(i)
  # Note: i and p are indices (not records)
  p = parent(i)
  while inBounds(p) && priority(p) < priority(i)
    swap(i, p)

    i = p
    p = parent(i)
```

---

## Float Induction

**Question:** If the new record is larger than its parent, could it be smaller than its sibling?

![](heaps/images/heap-float-contradiction.png)

<p class="fragment">**No!**</p>

<p class="fragment small">By induction, we can assume that the heap was valid before we started</p>

---

## Remove-Max Strategy

We want to remove the element at the front

<p class="small">The root has the highest priority</p>

We want to remove the slot from the back

<p class="small">This keeps the tree balanced</p>

![](heaps/images/heap-remove-strategy.png)

<p class="small fragment">Idea: swap the root with the last element, reduce the count, then "sink" the new root down until the max-heap property holds</p>

---

## Sink Down

![](heaps/images/heap-sink.png)

---

## Sink Pseudocode

```ruby
def sink(i)
  # Note: i, l, r and max are all indices (not records)
  finished = false
  until finished
    l = left(i)
    r = right(i)

    max = i
    if inBounds(l) && priority(l) > priority(max)
      max = l
    if inBounds(r) && priority(r) > priority(max)
      max = r

    if max == i
      finished = true
    else
      swap(i, max)
      i = max
```

---

## Summary

To stay balanced, a heap must always **add and remove slots at the end** of the current storage

<p class="small">Even if the record to add or remove doesn't go at the end</p>

We described **float** and **sink** subroutines to help us

<ul class="small">
<li>**Insert:** add the record at the end, then "float" it up to the right spot by repeatedly swapping with its parent</li>
<li>**Remove-Max:** swap root with the last element, then "sink" the new root down to the right spot by repeatedly swapping with its largest child
</ul>