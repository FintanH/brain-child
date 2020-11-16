---
title: Nix Channels
date: 2020-11-16T21:38
tags: [nix, nixos, learning, channels]
---

Packages come from channels. Simple as that. We can list what channels we have:

```
$ nix-channel --list
nixos https://nixos.org/channels/nixos-20.09
nixos-20.03 https://nixos.org/channels/nixos-20.03
nixos-unstable https://nixos.org/channels/nixos-unstable
unison https://github.com/ceedubs/unison-nix/archive/trunk.tar.gz
```

`nixos` is the default, stable channel I use. Before today it pointed to
`https://nixos.org/channels/nixos-20.03`. To switch to the latest channel I
created a new channel by doing:

```
$ nix-channel --add https://nixos.org/channels/nixos-20.03 nixos-20.03
$ nix-channel --add https://nixos.org/channels/nixos-20.09 nixos
```

Then I finished off the process by calling:

```
$ nix-channel --update nixos
```
