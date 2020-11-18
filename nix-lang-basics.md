---
title: Nix Language Basics
date: 2020-11-17T21:09
tags: [nix, nixos, learning, functional, repl]
---

Two familiar concepts off the bat:
  1. Everything is an expression in Nix
  2. Values are immutable

To play around with Nix expressions we can launch the REPL with `nix repl`.

## Arithmetic

The language supports basic arithmetic operations $+$, $-$, $\*$, $/$.

```
nix-repl> 1 + 1
2

nix-repl> 9 * 0
0

nix-repl> 5 - 6
-1

nix-repl> 3 / (7 * 0)
error: division by zero, at (string):1:1

nix-repl> 5 / 2
2
```

It's important to note that the division symbol, $/$, is overloaded since it is
also used for path seperation.

```
nix-repl> 4/2
/home/haptop/Developer/brain-child/4/2
```

## Operators

There's the whole slew of usual characters.

The boolean family:
- `||`
- `&&`
- `!`

The two sides of equality:
- `!=`
- `==`

The preorder possy:
- `<`
- `>`
- `<=`
- `>=`

## A note on identifiers

We have our usual way of writing identifiers but it's important to note that `-`
is also valid in an identifier name.

## Strings

We have our friend the String represented by characters between `"` and `"` or `''` and `''`.

```
nix-repl> "brain child"
"brain child"

nix-repl> ''brain child''
"brain child"
```

We can also interpolate strings:

```
nix-repl> brain = "brain"
nix-repl> "${brain} child"
"brain child"
```

## Lists

Lists are space separated items between `[` and `]`. The items of the list can
be of different types.

```
nix-repl> [ "brain" 42 "child" true ]

## Attribute Sets

Attribute sets are key-value maps where keys can _only_ be strings. For
convenience they don't need to be quoted strings. The separator for each
key-value pair is `;`.

```
nix-repl> s = { brain = "child"; "life" = 42; }

nix-repl> s."brain"
"child"

nix-repl> s.life
42
```
```

We can refer to keys _within_ a set by use the keyword `rec`

```
nix-repl> rec { brain = "brain"; child = "${brain} child"; }
{ brain = "brain"; child = "brain child"; }
```

## Let

`let` allows you to assign values to variables that can then be used `in` a following
expression. We can assign multiple variabls in one `let` block:

```
nix-repl> let a = 3; b = 4; in a * b
12
```

But we cannot shadow them this way, i.e. `let a = 3; a = "nope";`. We can
shadow, if we nest a `let` inside an outer expression, i.e. `let a = 3; in let a
= 8;`.

## With

We can use `with` to bring in an attribute set's keys into scope with qualifying
them.

```
nix-repl> brain-child = { brain = "brain"; child = "child"; }
nix-repl> with brain-child; "${brain}-${child}"
"brain-child"
```
