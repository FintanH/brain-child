---
title: NixOS Updates
date: 2020-11-29T13:49
tags: [nix, nixos, updating, learning]
---

This is very much a case of me not RTFM'ing. I thought I was updating my NixOS
for the longest time, but it turned out I wasn't doing anything really. The
confusion came from this set of lines in my `configuration.nix`:

```
# This value determines the NixOS release with which your system is to be
# compatible, in order to avoid breaking some software such as database
# servers. You should change this only after NixOS release notes say you
# should.   
system.stateVersion = "19.09"; # Did you read the comment?
```

It says I should only change this whenever the release notes say I should. So I
would go to the release notes and see that 20.03 and 20.09 were released. Each
time I would change this string value and run `sudo nixos-rebuild switch`. I
thought it would pick up on the change and get me onto the version I specified.

Well, let me tell you something. It didn't. I didn't know that it didn't for the
longest time. It wasn't until I was talking to my friend, Greg Pfeil, about my
monitor woes that I noticed the command `nixos-version`. When I ran it, it would
say `19.09`. I was _very_ confused. Thankfully, Greg imparted the wisdom to,
"never change that variable".

What NixOS _actually_ does for updating is read from `root`'s channels. I didn't
even _think_ about `root` having channels because I would always manage my
profile's channels. So I would run `nix-channel --list` and see all my user
profile channels, usually working off of the latest stable version.

The crux of this learning is that to update your NixOS version you have to do
the following:

```
$ sudo nix-channel --add https://nixos.org/channels/<version> nixos
$ sudo nix-channel --update
$ sudo nixos-rebuild switch
```

You can confrim you're on the correct version by running `sudo nixos-version`.
