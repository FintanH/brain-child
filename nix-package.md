---
title: Getting a Binary
date: 2020-11-16T21:08
tags: [nix, nixos, learning, package, derivation, nix-env, nix-shell]
---

There are two ways I'm aware of for grabbing a binary using Nix. That is
`nix-env` and `nix-shell`. If I wanted to install `cowsay` for my profile I
would simply call:

```
$ nix-env -i cowsay
```

I try to avoid this. I don't generally want to have a package permanantly --
especially not `cowsay`. But if I just want to quickly fuck around with `cowsay`
I can simply start a shell with it available.

```
$ nix-shell -p cowsay
$ which cowsay
/nix/store/dfb0lxa7fqbc6y5v1msxx9p87akx3mdk-cowsay-3.03+dfsg2/bin/cowsay
$ cowsay "Do a kickflip"
 _______________
< Do a kickflip >
 ---------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

If I did install a package using `nix-env` I could upgrade the package to a
newer version, if available, by calling:

```
nix-env -u cowsay
```

If I want to list all the packages I currently have in my profile I can call:

```
$ nix-env -q
ark-19.08.2
cabal-install-3.0.0.0
cabal2nix-2.14.4
cachix-0.3.8
chromium-83.0.4103.106
cmake-3.15.1
git-bug-0.5.0
google-chrome-78.0.3904.108
mirage-0.9.5.2
neovim-0.4.3
nix-prefetch-git
openssl-1.1.1d
patchelf-0.9
pkg-config-0.29.2
rust_crate2nix-0.7.1
sane-backends-2017-12-01
spectacle-19.08.2
stack-2.1.3.1
tree-1.8.0
vlc-3.0.8
xclip-0.13
zip-3.0
zoom-us-5.4.53350.1027
```

And I'm suddenly wondering why I even have some of these...
