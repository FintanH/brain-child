---
title: NixOS OOM /boot
date: 2020-11-18T16:41
tags: [nix, nixos, oom, os]
---

I just had a mini heart attack when I couldn't run `nixos-rebuild switch`. Every
time I would try, I would see the following:

```
OSError: [Errno 28] No space left on device
warning: error(s) occurred while switching to the new configuration
```

I did some spelunking on GitHub to eventually find this [issue comment][issue]
which boiled down to: delete past generations. I had accrued a lot of stale
generations that I didn't need to rollback for and so this gave me back some of
my `/boot` real estate.

The command that I found was:

```
sudo nix-collect-garbage --delete-older-than 60d
```

[issue]: https://github.com/NixOS/nixpkgs/issues/23926#issuecomment-347745220
