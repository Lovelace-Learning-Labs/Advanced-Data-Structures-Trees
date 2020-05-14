@snap[midpoint span-100]

# Red-Black Tree Rules

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

* **Define** the terms red-black tree, black-depth and rebalance
* **Explain** how, by following a set of rules, red-black trees can keep themselves balanced as they grow
* **List** the red-black tree rules

---

## Balance - Review

A tree is **balanced** if no leaf is more than twice as deep as any other

Balance directly affects the height `\(h\)` of a tree of size `\(n\)`:

`\[ h = \begin{cases} O(log(n)) & \quad \text{for a balanced tree} \\ O(n) & \quad \text{for an unbalanced tree} \end{cases} \]`

For a BST, `insert`, `lookup` and `delete` are `\(O(h)\)` time, and `forEach` is `\(O(h)\)` space

---

# End Fixup 1

---

@snap[midpoint span-100]

# Red-Black Tree Rebalance

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

* **Define** the term induction
* **Describe** the algorithm to rebalance a red-black tree after inserting a node
* **Explain** why our rebalance algorithm will only ever encounter one rules violation