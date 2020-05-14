# Discussion Questions

## Binary Search Trees

Please read through these before class, and come prepared to have a meaningful discussion with your peers

For each question we'll discuss in small groups, then as a big group

## General

1. Introduce yourself to your group!
1. What questions or comments do you have after watching the video lectures?
1. How could you use a BST to sort a list of numbers? What are the time and space complexities of this operation?
1. Do all binary trees of size `n` have the same number of leaves (empty children)? Make a convincing argument or find a counter-example.
1. Show that if a node in a BST has two children, then its successor (the node with the next key, in order) has no left child and its predecessor has no right child
1. What would it look like to augment our BST with a custom comparison function, that is, relying on a user-defined order instead of a natural one?
    - Does this change the time or space complexity of our operations?
1. How would you check _equivalence_ for two BSTs?
    - Analyze the time and space complexity
    - Is it possible for two BSTs with different internal structures to be equivalent?
1. How would we need to adjust our tree interface and implementation to permit repeat keys?
1. How would you _serialize_ and _deserialize_ a BST?
    - What are the time and space complexities of these operations?
1. Work with your group to design a non-recursive version of `forEach`...
    - Using a stack
    - Without using a stack (hint: the solution involves comparing nodes)
    - Analyze the time and space complexity of each design
