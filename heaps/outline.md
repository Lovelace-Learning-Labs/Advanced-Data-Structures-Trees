Motivating problem

- Priority queue
  - Insert element with priority
  - Get element with highest priority

Additional concerns:
  - Heapsort
  - 

Max heap vs min heap
- Max heap for heapsort
- Min heap for p-queue (priority is the cost)

A heap vs the heap (similar to a stack vs the stack)

Why fixed size
- Memory allocation is "slow"
- Sometimes you can't allocate memory after setup (OS, embedded systems)
- Fast serialize / deserialize
- Want to keep everything in one memory page (what is a memory page)

Fixed size in JS is imaginary

Here's what we're doing in JS (give them the constructor), and what memory looks like

Here's what code would look like in C (Rust?) and what memory looks like

Discussion Qs:
- If several elements have the same priority, does the heap respect insertion order? If not, how would you make it so? Remember that you can't allocate memory on insert. Would this change the run time?
- If you reverse a max heap, do you get a min heap? Argue why or give a counterexample.


Open Questions:
- Custom comparator? It would be cool to talk about this (when will we have another chance) but I suspect we won't have time