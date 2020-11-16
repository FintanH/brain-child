---
title: Nix Dependencies
date: 2020-11-16T21:30
tags: [nix, nixos, learning, store, package, derivation, dependency]
---

We can also do interesting things like query the store for looking at run time
dependencies of packages.

```
$ nix-store -q --references `which nvim`
/nix/store/x7fr0bvnwvqvr3zg60di9jxvfwimcw7m-bash-4.4-p23
/nix/store/b20r43n39rlnza3l1hd8qax7czaqb3w1-python3-3.7.6-env
/nix/store/i2hhrr4bqsa8g40nizd8yf8ypr0kdrzc-neovim-ruby-env
/nix/store/n31jls10qr4wl9nma5zz572lqv46z0w8-python-2.7.18-env
/nix/store/njk3jna904rc6xh7x1yfw9h5951dkbab-neovim-unwrapped-0.4.3
/nix/store/h58cxri85a0jg375pbsg1pqcni0nd8i0-neovim-0.4.3
```

And if we want to go in the other direction and see the **reverse
dependencies**:

```
$ nix-store -q --referrers `which gcc`
/nix/store/291ldi6fqsbmkbvbs8is4mcg3jb64ld4-gcc-wrapper-8.3.0
/nix/store/08d1xl0zw7kgf6202jvd8ykrawg5mzqg-system-path
/nix/store/125qg15wnyyl0zhxx6qfsiwyda4wv9ag-system-path
/nix/store/13173x3cicbv49a2a0vsdwd0bhwaxv33-system-path
/nix/store/2rk2rwz0lxmqkqk6asb1nvidhl8lg675-system-path
/nix/store/49nmgq2rrc3hnzqqmkb08m4asryprr64-system-path
/nix/store/4zai32r3iw1kr3y9nxxxz024ky5vysji-system-path
/nix/store/59dxbw4vcn1ljx679ip1ch6grwmwlwpd-system-path
/nix/store/7zm9k3h4nyq13xbn74a2xwbjp24f4dcj-system-path
/nix/store/9jalp1kzh78ixjlsh290zkdjzpqibv85-system-path
/nix/store/ba2zbp17ja2v4fw97a0j5jmh0xi9mpnb-system-path
/nix/store/ba79gwd3sbnxp5cspifl0ph51sbab5ha-ruby-2.6.6
/nix/store/d4cd5pln9bm4sf8ialdvy846jpzjazp7-system-path
/nix/store/fcviz6barhsqaj3kgd6vzpa4hmybsg1k-libtool-2.4.6
/nix/store/gkq2j2hnrsg6kpzm0ibygwm3xgl6yl14-system-path
/nix/store/grwhp0bv5mfiz2m6pidp1c0jpknbz1pd-system-path
/nix/store/h3kc2i0z93k5pnb6gsl6678yvgaci708-ruby-2.6.5
/nix/store/k0fnp9qdw7ywn1x1b58r7narpi861gp8-system-path
/nix/store/m4kzx5bksq69wln8wkm0wkvwp9y7n8m7-system-path
/nix/store/m99h615hd732r0pz55y9zf9sxsbq0g8h-system-path
/nix/store/qghrkvk86f9llfkcr1bxsypqbw1a4qmw-stdenv-linux
/nix/store/qwpdvkgqqp9c40widb27y1w53afrvam4-system-path
/nix/store/smj2qljmm3pypzlkl5vhj10ga3fjz3i9-system-path
/nix/store/v1wsys5bcshxrbr8kf2xbsp57klia7vc-ghc-8.6.5
/nix/store/wbsvsq3arq20ks5qmrklqbpvm6lsxspv-system-path
/nix/store/y7zjpm0v5pi5jmhflz522yvlnk551mf0-system-path
/nix/store/yfnaprfyc88n3bmkfxvyw61pk97ibyda-system-path
/nix/store/yvl8hgy1rzrivlp6a07i8c77241s71g6-neuron-7.5
/nix/store/zh41y0cq0g0ypcjb4758wagpv4x4k2gi-system-path
```

Look at that! `neuron` relies on `gcc` :)

We can also do interesing things like getting the closure of dependencies using
`nix-store -qR`, or get the a transitive tree of dependencies using `nix-store
-q --tree`.
