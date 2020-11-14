---
date: 2020-11-14T15:44
tags: [recursion, history, primitive-recursion, recursion-schemes]
---

The first work completely dedicated to recursive definability was produced by
Thoralf Skolem in 1923:

> The foundations of elementary arithmetic established by the recursive mode of
> thought, without the use of apparent variables ranging over infinite domains.

It was the first piece of work that gave an informal definition of primitive
recursion and linked recursion to effective computability.

What stands out the most is what Skolem called "recursive mode of thought",
which can be laid out like a recipe:

i. The natural numbers are defined recursively
ii. Previously proven statements can be substituted in expressions --
    functional programmers know this as [[referential-transparency]].
iii. All definitions of functions and relations on numbers are given by
    recursion.
iv. Functional assertions must be proven by induction.

This formula sounds and awful lot like recursion-schemes but specialised to
natural numbers.
