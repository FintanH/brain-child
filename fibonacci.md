---
date: 2020-11-14T14:43
tags: [recursion, history]
---

The Fibonacci sequence is a recursive function that across early and often when
first exploring recursive functions. It is apocryphally claimed to be invented
by Leonardo Fibonacci, a 12th century Italian mathematician. Keith Devlin says
that it was found in ancient Sanskrit texts in his book "Finding Fibonacci: The
Quest to Rediscover the Forgotten Mathematical Genius Who Changed the World".

We can, however, see the sequence in "Liber Abaci", where Fibonacci poses it as
a solution to the problem of rabbit populations. The problem goes: "We have a
male and female rabbit. After a month, they reproduce another male and female
rabbit. After another month, those rabbits reproduce and out comes another male
and female rabbit. This continues on. How many rabbits would we have after a
year?" The answer is the same as as if we plug the value 12 into the Fibonacci
function. But what is this function?

```hs fib 1 = 1 fib 2 = 1 fib n = fib (n - 1) + fib (n - 2) ```

If we write these out as a sequence we get: `1, 1, 2, 3, 5, 8, 13, 21, 34, 55,
89, 144, ...`. The 12th value in that sequence is `144`.

The sequence shows up with
[applications](https://en.wikipedia.org/wiki/Fibonacci_number#Applications) in
mathematics, music, and nature. In a way it's a sequence of beauty that the
universe bestowed upon us.
