@snap[midpoint span-100]

# Tries

### Introduction

@snapend

---

## Learning Goals

By the end of this module, students will be able to...

- **Name** the interface and implementation we'll be studying this week
- **Define** the terms radix, string, prefix and suffix

---

## Interface

Interface: **prefix dictionary**

Maps a string code to a string word

New operation: find all words pairs matching a certain code **prefix**

Application: T9 dictionary

---

## Implementation

Data structure: **trie** (short for re-TRIE-val)

<p class="small">a.k.a. radix tree</p>

Tree optimized for working with strings

<p class="small">Non-binary tree - more than 2 children per node</p>

---

## String Vocab

Tries are all about strings!

Four important terms:

- Radix
- String
- Prefix
- Suffix

---

## Radix

A radix is an atomic primitive in an encoding scheme

<p class="small">A character in an alphabet</p>

- Binary: `0`, `1`
- Decimal: the digits `0` through `9`
- Hexadecimal: `0-9`, `A-F`
- Lowercase English: `a-z`
- Unicode: any printable symbol

---

## String

A string is a sequence of zero or more radixes

- Binary: `1101101`
- Decimal: `1991`
- Hexadecimal: `7880AE4D`
- Lowercase English: `academy`
- Unicode: `안녕하세요`

The **length** of a string is the number of radixes

---

## Prefix

Zero or more characters at the **beginning** of a string

Prefixes of `academy`:

<p class="small">'', 'a', 'ac', 'aca', 'acad', 'acade', 'academ', 'academy'</p>

Notes:

<ul class="small">
<li>The empty string is a prefix of every string</li>
<li>Every string is a prefix of itself</li>
</ul>

---

## Suffix

Zero or more characters at the **end** of a string

<p class="small">Opposite of a prefix</p>

Suffixes of `academy`:

<p class="small">'', 'y', 'my', 'emy', 'demy', 'ademy', 'cademy', 'academy'</p>

Notes:

<ul class="small">
<li>The empty string is a suffix of every string</li>
<li>Every string is a suffix of itself</li>
</ul>

---

## String Vocab

| Term   | Definition                       | Example                                                                                        |
| ------ | -------------------------------- | ---------------------------------------------------------------------------------------------- |
| Radix  | A letter in an alphabet          | 0 and 1 are the radixes of binary, the letters 'a'-'z' are the radixes of the English alphabet |
| String | A sequence of radixes            | 10110 in binary, 'dev' in English                                                              |
| Prefix | Radixes at the front of a string | '', 'd', 'de' and 'dev' are all prefixes of 'dev'                                              |
| Suffix | Radixes at the end of a string   | '', 'v', 'ev' and 'dev' are all suffixes of 'dev'                                              |
