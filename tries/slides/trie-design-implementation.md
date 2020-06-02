@snap[midpoint span-100]

# Trie

### Design and Implementation

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Identify** features of other data structures relevant to implementing a prefix dictionary
- **Describe** the structure of a trie
- **Explain** how the lookup and insert operations work on a trie

---

## Prefix Dictionary

We need a data structure to track associations between **codes** and **words**, both strings

Key operation: Lookup words by **code prefix**

Goals:

- Fast lookup (`\(O(c + m)\)` time for a code of length `\(c\)` resulting in `\(m\)` matches)
- Minimal storage space

---

## Inspiration

Consider the data structures we've learned about so far

Can any of them implement the prefix dictionary interface easily?

If not, what inspiration can we draw from those other data structures?

---

## Tree Inspiration

Lookup in a BST takes one step for each "decision point"

<p class="small">i.e. compare target key to current node, go left or right</p>

What if we could make one decision per code radix?

<p class="small">We would have a tree of radixes - a **radix tree**</p>

Each node would need to have many children...

---

## Naming

This data structure is known as both a **radix tree** and a **trie**

<p class="small">These are the same thing</p>

**Radix tree:** tree where each branch represents a radix

**Trie:** tree optimized for reTRIEval

<p class="small">Pronounced like "try"</p>

In this class we'll call them **tries**

---

## Wide Nodes

Idea: a tree with more than two children per node

<p class="small">Instead of `left` and `right`, each child represents one radix in our code alphabet</p>

![](tries/images/trie-node.png)

<p class="small">Tries are **sparse**, so from here on we'll only show filled links</p>

In JavaScript, we can use an object to store children

---

@snap[north-west span-65]

## Links Make Codes

To lookup a code, iterate through its radixes, following a link every time

```ruby
def lookup(code)
  node = root
  for radix in code
    node = node.children[radix]
    return [] if node is undefined
  return node.words
```

@snapend

@snap[east span-30]
![](tries/images/trie-links.png)
@snapend

---

@snap[north-west span-65]
## Storing Words

Multiple words may have the same code

Each node keeps an **array** of matching words

<p class="small">Inner nodes with no matching words contain an empty array</p>

@snapend

@snap[east span-30]
![](tries/images/trie-multiple-words.png)
@snapend

---

## Lookup by Prefix

Each prefix corresponds to a sub-trie

Follow links to find the sub-trie (similar to lookup)

Iterate through all nodes in the subtree to gather matches (similar to BST.forEach)

---

## Lookup by Prefix

![](tries/images/trie-lookup-prefix.png)

---

@snap[north-west span-65]

## Insert

Similar to lookup, but create missing nodes

```ruby
def insert(word)
  code = buildCode(word)
  node = root

  for radix in code
    if node.children[radix] is undefined
      node.children[radix] = new TrieNode()
    node = node.children[radix]

  node.words.push(word)
```

@snapend

@snap[east span-30]
![](tries/images/trie-insert.png)
@snapend

---

## Summary

- In a trie, each node has one child for each radix in our code alphabet
- Each node stores a list of words matching that code
- To lookup by code, walk down the trie one radix at a time
    - Lookup by prefix: lookup, then gather all matches in the subtree
    - Insert: lookup but create missing nodes

