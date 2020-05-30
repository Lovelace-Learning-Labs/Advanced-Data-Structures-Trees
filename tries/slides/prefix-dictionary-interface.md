@snap[midpoint span-100]

# Prefix Dictionary

### Interface

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Define** the terms radix, string, prefix, suffix
- **Describe** how a T9 keyboard works
- **List** the important features of the prefix dictionary interface

---

@snap[north-west span-60]
## T9 Dictionary

Method for quick input on phones without a full keyboard

<p class="small">One button press per letter, system give a list of matching words</p>

<p class="small">Supports autocomplete</p>

We need a data structure to store the code for each word

We'll call it a **prefix dictionary**

@snapend

@snap[east span-40]
![](tries/images/t9-keyboard.png)
@snapend

---

@snap[north-west span-60]
## T9 Codes

What would the T9 codes be for...

- ada
- developers
- academy
- bat
- cat
@snapend

@snap[east span-40]
![](tries/images/t9-keyboard.png)
@snapend

---

@snap[north-west span-60]
## T9 Codes

What would the T9 codes be for...

- ada: `232`
- developers: `3383567377`
- academy: `2223369`
- bat: `228`
- cat: `228`

<p class="small">"bat" and "cat" share a code</p>

<p class="small fragment">Typing out `2` `2` would show "bat", "cat" and "academy" in the list of words (among many others)</p>
@snapend

@snap[east span-40]
![](tries/images/t9-keyboard.png)
@snapend

---

## Lowercase Codes

Digits are hard to read!

In these lessons, to make things easier to read, we will use `toLowerCase` as our code scheme

- `academy`: `academy`
- `ACADEMY`: `academy`
- `AcAdEmY`: `academy`

We will also assume only English letters

---

## Interface Questions

Pause the video and consider the following questions about our **prefix dictionary** interface:

- What **type of records** are we storing?
- What **operations** do we need to support?
- What (if any) **ordering** do we maintain?
- What **use pattern** do we expect?

---

## Prefix Dictionary

**Records** are pairs: word (lowercase English) + code (decimal numbers)

<p class="small">Code can be generated from the word</p>

**Operations:**

<ul class="small">
<li>Add a new word</li>
<li>Lookup a word by code</li>
<li>Get a list of all words where the code matches a given prefix</li>
</ul>

**Order** doesn't matter as long as you can search by prefix

**Workflow:** Build once, read many times

<p class="small">Occasionally the user may add a new word</p>

---

## Performance

Goals:

- Fast lookup - order `\(O(c)\)` for a code of length `\(c\)`
- Minimal space (linear with a good constant)
- Slow insert is OK

---

## Summary

We need a data structure to track associations between **codes** and **words**, both strings

Key operation: Lookup words by **code prefix**

Goals: fast lookup, minimal storage space
