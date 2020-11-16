---
title: Nix Generations
date: 2020-11-16T21:20
tags: [nix, nixos, learning, package, derivation, nix-env]
---

If I did use `nix-env` to install `cowsay` -- as in [[nix-package]], I could
rollback the installation easily by calling:

```
$ nix-env --rollback switching from generation 29 to 28
```

Whatever was in generation 29, `cowsay` in this case, is now not available
anymore.

To list the generations that I currently have I can call:

```
nix-env --list-generations
   1   2019-12-17 11:38:31
   2   2019-12-17 11:43:29
   3   2019-12-17 11:52:26
   4   2020-01-14 14:56:32
   5   2020-01-15 13:48:55
   6   2020-01-29 20:15:11
   7   2020-01-29 20:58:13
   8   2020-01-31 17:08:26
   9   2020-02-01 11:41:52
  10   2020-02-01 11:48:24
  11   2020-02-06 15:45:45
  12   2020-02-10 10:37:55
  13   2020-02-18 10:54:33
  14   2020-02-18 15:28:23
  15   2020-02-27 17:52:42
  16   2020-02-27 17:58:13
  17   2020-02-28 15:00:43
  18   2020-03-04 15:14:37
  19   2020-03-21 16:21:37
  20   2020-03-21 16:21:53
  21   2020-03-21 16:22:05
  22   2020-03-21 16:24:58
  23   2020-05-31 20:58:23
  24   2020-05-31 22:44:34
  25   2020-06-13 13:35:44
  26   2020-07-25 20:34:30
  27   2020-10-03 15:10:59
  28   2020-11-16 21:07:07   (current)
  29   2020-11-16 21:14:45
```

If I want to remove generation `29` I can call:

```
$ nix-env --delete-generations 29
removing generation 29
```

If I want to switch to a particular generation I can call:

```
$ nix-env -G 3
switching from generation 28 to 3
```
