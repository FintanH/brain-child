---
date: 2020-11-14T15:51
tags: [functional-programming, expressions, haskell]
---

Referential transparency is a phrase that often correlates with functional
programming. It's the ability to substitute the result of an expression into a
larger expression without changing any meaning. This is a little bit wordy, so
let's look at an example.

## Example

```hs
x :: Int
x = 1

incr :: Int -> Int
incr y = y + x
```

In this simple example, referential transparency says that we can replace `x` in
the expression `y + x` with its value `1`, resulting in the expression `y + 1`.

This thought tool is extremely useful for when we want to reason about our
programs, i.e. substitute expressions for their values, in our heads.

```hs
plusTwo :: Int -> Int
plusTwo y = incr (incr y)
```

In this example, we can even substitute expressions for another expression --
and not a value. This would mean that we could also define `plusTwo` as:

```hs
plusTwo :: Int -> Int
plusTwo y = (y + x) + x
```
