@snap[midpoint span-100]

# Memory Swapping

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Compare** main memory (RAM) with secondary memory (disk)
- **Explain** why memory is organized into pages
- **Describe** the technique of swapping memory to disk

---

## Memory Primer

B-trees are optimized for working with disk drives

An understanding of key memory concepts will help our discussion

- Main memory (RAM)
- Secondary memory (disk)
- Memory paging
- Memory swapping

---

@snap[north-west span-70]

## Main Memory

Powered silicon chips called **RAM** (Random Access Memory)

<p class="small">All memory access takes about the same time</p>

**Volatile**

<p class="small">Data goes away after a reboot, crash or power failure</p>

Fast but expensive

<ul class="small">
<li>Typical access speed is 100 nanoseconds</li>
<li>In 2020, $100 buys about 32GB of RAM</li>
</ul>
@snapend

@snap[east span-30]
![](b-trees/images/ram.jpg)
@snapend

---

## Secondary Memory

@snap[south-west span-70]

External storage like hard drives, SSDs or tape drives, collectively called **disk**

<p class="small">Typically supports **sequential** access - much faster to read data close together than far apart</p>

**Non-volatile** (a.k.a. persistent)

<p class="small">Data is saved long-term, even through power loss</p>

Slow but cheap

<ul class="small">
<li>Typical access speed is 10 milliseconds</li>
<li>In 2020, $100 buys about 4TB of disk</li>
</ul>

@snapend

@snap[east span-30]
![](b-trees/images/hard-drive.jpg)
@snapend

---

## RAM vs Disk

| Category       | Main Memory | Secondary Memory | Difference |
| -------------- | ----------- | ---------------- | ---------- |
| Hardware       | RAM chips   | Disk, SSD, tape  |            |
| $100 buys...   | 32 GB       | 4 TB             | 100x       |
| Latency        | 100 ns      | 10 ms            | 100,000x   |
| Persistent     | No          | Yes              |            |
| Access pattern | Random      | Sequential       |            |

<br>

Main memory (RAM) is the default

<p class="small">All the programs we've written in this class have used main memory exclusively for storage</p>

---

## Memory Pages

Disk access is **sequential**

<ul class="small">
<li>**Seek** (find the right spot) is slow (milliseconds)</li>
<li>**Transfer** (read or write the data) is fast (microseconds)</li>
</ul>

To minimize seek time, we want to read/write big chunks of data, called **pages**

<p class="small">Pages have a fixed size - 2, 4 or 8 KB is common</p>

Performance is best if you read / write an entire page at a time

---

## Swapping Memory

Main memory is expensive, so we'll have less of it

What if our program needs to store a **lot** of data?

<p class="small">e.g. a big database</p>

Idea: use RAM as a **cache** for disk

<ul class="small">
<li>Data lives on disk, organized in pages</li>
<li>Before working with data, load its page into main memory</li>
<li>If a page hasn't been used in a while, send it back to disk</li>
</ul>

This strategy is called **swapping** memory

---

## Swapping Data Structure

How can we design a data structure to perform well with swapping?

Such a data structure would need to answer many questions:

- How do you know in which page your data lives?
- How do you take advantage of the large size of a page?
- How do you minimize the number of disk reads per operation?
- How do you balance processor speed against disk access time?

These questions will be our focus this week

---

## Memory in JavaScript

JavaScript doesn't give us visibility into memory

- How big is main memory?
- How big is a page?
- How is memory laid out?
- What page does this object live on?

If you were implementing a database, you would use a systems language like C, C++ or Rust

These ideas give context to our discussion, but we won't be able to see the mechanics or measure the benefits in JS

---

## Summary

**Secondary memory** (disk) is 100x cheaper but 100,000x slower than **main memory** (RAM)

<p class="small">Most computers have way more disk space than RAM</p>

Memory is organized into fixed-size **pages** of a few KB each

<p class="small">To boost performance, secondary memory is always read / written in page</p>

**Swapping** pages of main memory out to disk lets us pretend we have extra memory available