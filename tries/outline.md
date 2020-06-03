# Tries

## Intro

Interface / DS

Trees optimized for strings

Multi-trees

## Interface

Motivating problem: T9 dictionary
- Slide with some examples

Interface: Prefix Dictionary

Records: codes + words (strings)
Ops: Insert, lookup by code, lookup by code prefix
Use pattern: preload, occasional inserts

Performance:
- Terms: n (record count), r (code alphabet size (10, 26, etc), aka number of radixes), c (length of current code), k (max code length), m (num matches)
- Insert - c
- Lookup - c
- Lookup prefix - c + m
- Space: n
- Startup time: fast (n * c)

Different codes
- T9
- Identity

Vocab
- prefix
- suffix
- radix

## Design + Impl

Other DS
- Sorted array: slow to construct, still log(n) lookup (we want c)
- Linked list: no random lookup
- Hash: fast lookup, but no searching by prefix
- RB Tree: Sill log(n), search by prefix is complex
- Heap: not relevant

Need something new

Idea: node represents a code prefix, children are all suffixes

How to organize?

One letter per link

How many children per node?

Radix count (r)

Node Structure:
- Store list of children in a hash
- Multiple words might have the same code, so we'll need to store a list of words at each node. List might be empty (for an interior node).

Insert / lookup / gather

## Analysis

Branching factor - number of radixes r

Height - length of maximum code

Number of nodes
- n <= r^h
- log_r(n) <= h

Time - insert code of length c
- Follow or create one node per radix
- O(c)

Time - lookup code of length c
- Look at one node per radix in the code
- O(c)

Time - lookup prefix of length c
- Follow one link per radix in prefix
- Gather words from subtree
- O(c + m)

Space - How many nodes?
- Really hard to express
- Lower bound is n (all words have the same code)
- Upper bound in terms of r + c: r^c
    - Not realistic, because real languages are sparse (not all word)
- Upper bound in terms of n + c: n * c
    - Not realistic, because lots of code overlap
- In practice, for English (10k words, average length X)
    - Identity: x nodes, x empty
    - T9: 

Vocab
- dense
- sparse

## Optimization

Idea: compress runs of nodes that contain no words

Since we're using JS objects to store child nodes, structure is similar (keys just have more than one letter)

Lookup is almost the same

Insert gets a little tricky
- Partial match -> need to "split" a link

## Qs

- Would it be a good idea to use an array to store a trie (like a heap)? Why or why not?
- How could you optimize a trie if the code for every word is that word?
    - We call the mapping from a word to itself the "identity" mapping.


## Additional Reading

https://blog.afterthedeadline.com/2010/01/29/how-i-trie-to-make-spelling-suggestions/