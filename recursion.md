---
date: 2020-11-14T14:13
---

# Recursion

**Recursion** -- in its basic form -- can be quite daunting for some people at
first. As functional programmers, it can be a birth by fire as we must begin to
think recursively to achieve what other programmers would achieve with loops and
iteration.

To help all programmers alike, let's give a definition of recursion to help
solidify our knowledge of this pariticular beast. A recursive function is one
that is **self-referential** -- it calls itself in its body. Since function calls
itself, if we ever want it to terminate then the next call to the function
should pass smaller arguments in the next iteration. Finally -- to also aid in
termination -- there should be a **base case** for which the function terminates
on.

Our canonical cases are the **factorial** and **fibonacci** functions:

```hs
-- | ∀ n ∈ ℕ
fib 0 = 1
fib 1 = 1
fib n = fib (n - 2) (n - 1)

-- | ∀ n ∈ ℕ
fac 0 = 1
fac n = n * fac (n - 1)
```

We are also used to seeing base cases in when defining functions on structures
such as lists and trees:

```hs
data List a
    = Cons a (List a)
    | Nil -- ^ The base case for a list

data Tree a
    = Branch (Tree a) (Tree a)
    | Leaf a -- ^ The base case for a tree
```
