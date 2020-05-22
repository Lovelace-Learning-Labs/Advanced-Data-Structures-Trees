@snap[midpoint span-100]

# Heap

### Design

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

---

## Design Review

Store tree nodes as elements in an **array**

<p class="small">Parent is at `\(\left \lfloor{ \frac{i}{2} } \right \rfloor \)`, children are at `\(2 * i\)` and `\(2 * i + 1\)`</p>

Keep the tree **perfectly balanced**

<p class="small">Bottom layer fills left-to-right</p>

Maintain the **max-heap property**:

<p class="small">Every node has priority less than or equal to that of its parent</p>

In the next module, we'll show how to implement insert and remove to satisfy these two properties

---

## Summary

---

## Vocab