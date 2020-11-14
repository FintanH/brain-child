---
title: Primitive Recursion
date: 2020-11-14T16:12
tags: [recursion, recursion-class]
---

For the more mathematically include, the definition of [Primitive Recursive
Functions is provided
here](https://plato.stanford.edu/entries/recursive-functions/#PrimRecuFuncPR).

For the mere mortals, such as me, I will attempt to give a more intuitional
definition. Primitive recursive functions are ones that act on natural numbers
-- or products of natural numbers, e.g. `mult(x, y)`, `add3(x, y, z)`. These
functions are allowed to use other primitive recursive functions and composition
of functions.

Looking at the Stanford article linked above, we can see a pleasant build up to
the schemes for primitive recursion. The first natural definition of a general
recursive function is:

$$
\begin{align} \label{prex2}
	h(0) & =  n  \\ \nonumber
	h(x+1) & =  g(x,h(x))
\end{align}
$$

We can see the basics of [[recursion]] here, where $0$ acts as the base case. In
the other case we are reducing the natural number by "peeling" off the $+ 1$
from $x$ and passing the result as an argument recursively to $h$. We should
also note that we are able to use another function on the natural numbers, $g$,
_and_ use $x$ as an argument to this function.

We are able to generalise this by allowing ourselves to pass arguments in the
recursive function.

$$
\begin{align}  \label{prex3}
	h(x,0) & =  f(x) \\ \nonumber
	h(x,y+1) & =  g(x,h(x,y))
\end{align}
$$

Here we pass $x$ as an argument, while recursively making $y$ smaller.

The final generalisation is allow ourselves to pass _many_ arguments to $g$.

$$
\begin{align}  \label{prscheme}
	h(x_0,\ldots,x_{k-1},0) & = f(x_0,\ldots,x_{k-1}) \\   \nonumber
	h(x_0,\ldots,x_{k-1},y+1) & = g(x_0,\ldots,x_{k-1},y,h(x_0,\ldots,x_{k-1},y))
\end{align}
$$
