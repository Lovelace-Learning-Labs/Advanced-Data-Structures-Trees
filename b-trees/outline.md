B-tree rules / definitions

Leaf node: node with no children (different than RBT definition)
- No sentinels

Degree of a node is the number of children that node has (or could have)
- Number of key/value pairs is always one less than number of children
- You can think of keys as "separating" children
- Even for a leaf, which has no children, we talk about the degree

Nodes are sorted
- k/v pairs go from left to right, so node.keys[i] < node.keys[i+1] for 0 <= i < t-1
- For every key:
    - Every key in the subtree rooted at node.children[i] is less than node.keys[i]
    - Every key in the subtree rooted at node.children[i+1] is greater than than node.keys[i]
- What do these two rules tell you about children further to the left / right?
- How does this compare to the BST property?


B-Tree has a "minimum degree" t
- Every node (except the root) must have at least degree t
    - So at least t-1 k/v pairs
- Every node has at most degree 2t
    - So at most 2t-1 k/v pairs
- What is the minimum minimum degree?
    - 2! Otherwise you have 0 k/v pairs per node


Supplement: disk drives and paging
- [Data structures and secondary storage](http://staff.ustc.edu.cn/~csli/graduate/algorithms/book6/chap19.htm) from CLRS Intro to Algorithms, start up to (not including) 19.1

Additional Reading
- [Intro to disk drives](http://pages.cs.wisc.edu/~remzi/OSTEP/file-disks.pdf), start through 37.3 (can skip "some other details")
- [Intro to Virtual Memory and Paging](http://pages.cs.wisc.edu/~remzi/OSTEP/vm-paging.pdf)
- Comes from http://pages.cs.wisc.edu/~remzi/OSTEP/, from UW Madison