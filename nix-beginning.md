---
title: Nix Beginning
date: 2020-11-16T20:37
tags: [nix, nixos, learning]
---

The selling point of Nix is to have multiple versions of the same package on
your system at the same time without them interfering with each other. This is
because packages -- also known as derivations in Nix -- are atomic, immutable
units.  If a change is made to a derivation then the output is a completely
different output to the previous build of the derivation.

The output of derivations are placed in the `/nix/store` where they are
identified by a `hash` -- and there is a human readable `name` provided too. For
example, if I call `ll $(which bash)` on my system -- `ll` because it turns out
it's a symlink -- I will get the following output:

```
[haptop@nixos:~/Developer/brain-child]$ ll $(which bash)
lrwxrwxrwx 1 root root 77 Jan  1  1970 /run/current-system/sw/bin/bash -> /nix/store/lb3hli8d9536g45mndwfwyi6fpny0blh-bash-interactive-4.4-p23/bin/bash
```

Like most things, this is a design decision that has pay offs but also has its
downsides. I hope to learn more about these on this journery.
