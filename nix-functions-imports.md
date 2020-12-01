---
title: Functions & Imports
date: 2020-11-30T19:36
tags: [nix, nixos, learning, functional, repl]
---

## Function Basics

### Lambdas

Lambdas, like Haskell, provide the backbone of functions in Nix. The syntax is
simply the name of the variable, `x`, followed by a colon, `:`, and the body of
the function.

```
nix-repl> x: x * x
«lambda @ (string):1:1»
```

There's no sugar for compacting parameters, so to have more than one parameter
we have to use a colon separated list.

```
nix-repl> x: y: x * y
«lambda @ (string):1:1»
```

### Named Functions

When we introduce a lambda, in the repl, there's no way to use it other than
immediately.

```
nix-repl> (x: y: x * y) 6 7
42
```

So to be able to reuse a function in multiple places we can bind it to a name.
In the repl this is done by the name followed by `=`.

```
nix-repl> square = x: x * x
```

We can then use it in other expressions:

```
nix-repl> map square [ 1 2 3 4 5 6 7 8 9 10 ]
[ 1 4 9 16 25 36 49 64 81 100 ]
```

### Currying

We can see that the syntax for lambdas is pointing us to the fact that functions
can be curried. Each function takes one parameter and returns an express, which
can be another function.

```
nix-repl> times = x: y: x * y
nix-repl> times-six = times 6
nix-repl> times-six 9
54
```

## Sets as Parameters

### Basics

We can also use attribute sets as parameters to functions, accessing their
fields in the function body.

```
nix-repl> get-product = product: product.x * product.y
nix-repl> get-product { x = 6; y = 7; }
42
```

We introduce the attribute set as a named parameter, `product`. We can also
introduce the set directly by pattern matching on it.

```
nix-repl> get-product = { x, y }: x * y
```

This won't accept sets with extra keys such as `{ x = 6; y = 7; z = 10; }`.

### Defaults

We can also choose defaults for any key in the attribute set.

```
nix-repl> hello = { hello, world ? "fintohaps" }: "${hello}, ${world}"
nix-repl> hello { hello = "hey"; }
"hey, fintohaps"
```

### Variadics

If we don't want to restrict the attribute sets that get passed to the function
and just want to specify a particular set of keys, then we can use a variadic
format.

```
nix-repl> get-product = { x, y, ... }: x * y
nix-repl> get-product { x = 6; y = 7; z = 10; }
42
```

## Imports

Nix files end in the file extension `.nix`. If we have an expression defined in
one Nix file then we can import it by using the keyword `import` followed by the
file path pointing to the file.
