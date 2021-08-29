---
title: Understanding Identity Document Histories
date: 2021-01-13T11:46
tags: [radicle, radicle-link, git, identities]
---

Using the example a project, when it first gets created a new reference can be
found in the monorepo, e.g.
`refs/namespaces/hnrkj86mackfhhfjcfiqiju4z8ooi8rz3mwqo/rad/id`.
If we were to inspect this using command line tools, we could call `more` on
this entry and we would see a commit.

```
$ more refs/namespaces/hnrkj86mackfhhfjcfiqiju4z8ooi8rz3mwqo/refs/rad/id
3d1786e244edef16e0cdb0f1b98db9d2639faf01
```

Using `git cat-file` to inspect this further we could see something like the
following:

```
$ git cat-file -p 3d1786e244edef16e0cdb0f1b98db9d2639faf01
tree 0a1b49731c8e55c9d5182896da1f9c3112588ba5
author anonymous <anonymous@hybdawop4njtagz81zxo8awcjetmkkkhc96ceubibtw99rzdkx1raq> 1610536800 +0000
committer anonymous <anonymous@hybdawop4njtagz81zxo8awcjetmkkkhc96ceubibtw99rzdkx1raq> 1610536800 +0000

Initialised project identity 93f978628bce152c2d5d54cf573c215392f95d1d

X-Rad-Signature: hybdawop4njtagz81zxo8awcjetmkkkhc96ceubibtw99rzdkx1raq
  hydrbtckend64j9m975673zzpod8ewxz1pfrtaaw5zg68m51f4eqjysz9e7qewbirndt5dikhcu4awe5qn4w5944acndfhj1tow993uyf
```

So, this object is a `Commit`, which contains some metadata information as well
as a `Tree` object. We can keep pulling on this thread by using `git cat-file`
on the tree object as well.

```
$ git cat-file -p 0a1b49731c8e55c9d5182896da1f9c3112588ba5
100644 blob 93f978628bce152c2d5d54cf573c215392f95d1d	93f978628bce152c2d5d54cf573c215392f95d1d
040000 tree 6a5eca7a1628f98de7b0ce0bd58073eebbb7b058	delegations
```

Here we've found a `Blob` and another `Tree`. The listing format, from left to
right, shows us the file permissions, the object type, the object identifier,
and the name of the object. So we have a `Blob` that is named after its
identifier. Let's keep pulling on that thread.

```
$ git cat-file -p 93f978628bce152c2d5d54cf573c215392f95d1d
{
   "delegations":[
      "rad:git:hnrkekgfukxrg8fwr38bykemoawk3pypfkjfo"
   ],
   "payload":{
      "https://radicle.xyz/link/identities/project/v1":{
         "default_branch":"next",
         "description":"pea two pea",
         "name":"radicle-link"
      }
   },
   "replaces":null,
   "version":0
}
```

This is exactly our identity document in its initialised form. We want to
understand how a history of a document works though. So let's say we update this
document, completely changing its contents -- let's fork this! We use the
`radicle-link` code to quickly change this and re-do this process.

```
$ more refs/namespaces/hnrkj86mackfhhfjcfiqiju4z8ooi8rz3mwqo/refs/rad/id
5c0fa1a6561a45ffd5d302c5986b0b8a03bd5458

$ git cat-file -p 5c0fa1a6561a45ffd5d302c5986b0b8a03bd5458
tree 428a1e6ec0773cc8a87dadadb49a79e72d58993b
parent 3d1786e244edef16e0cdb0f1b98db9d2639faf01
author anonymous <anonymous@hybbqpkmg8ypijjas7tanwrnq4jhn18zd8t3dfzz8p9bseeoxyxgus> 1610536800 +0000
committer anonymous <anonymous@hybbqpkmg8ypijjas7tanwrnq4jhn18zd8t3dfzz8p9bseeoxyxgus> 1610536800 +0000

Updated to revision 428a1e6ec0773cc8a87dadadb49a79e72d58993b

X-Rad-Signature: hybbqpkmg8ypijjas7tanwrnq4jhn18zd8t3dfzz8p9bseeoxyxgus
  hyd54oax88wkbqzeus7zt4aprargxid53y1xkuh37k66jytqcgykk67eqfw3x5hrnianyonbobod651tnduye5nsmtanbzd16f31azaof
```

We now have a commit that looks similar to the previous output except for:
  1. The information of the peer who changed it is used
  2. The message changed to tell us that it's an update
  3. There is also a parent object -- the parent commit

Doing a `git cat-file -p 3d1786e244edef16e0cdb0f1b98db9d2639faf01` will show us
the previous commit. Where the identifier for the tree is _unchanged_.

Re-doing the process on the `Tree` will give us the following:

```
$ git cat-file -p 428a1e6ec0773cc8a87dadadb49a79e72d58993b
100644 blob 2c8340affd577e3b2664436431ced8a34408f551	93f978628bce152c2d5d54cf573c215392f95d1d

$ git cat-file -p 2c8340affd577e3b2664436431ced8a34408f551
{
   "delegations":[
      "rad:git:hnrkekgfukxrg8fwr38bykemoawk3pypfkjfo"
   ],
   "payload":{
      "https://radicle.xyz/link/identities/project/v1":{
         "default_branch":null,
         "description":null,
         "name":"peer 3 fork"
      }
   },
   "replaces":"0a1b49731c8e55c9d5182896da1f9c3112588ba5",
   "version":0
}
```

We see that the `payload` has changed and the `replaces` field is now also set
and points to the previous identifier for the previous `Tree`.

There's a reason why I emphasises _unchanged_ above. Since `Commit`s have a lot
of metadata that go into creating the SHA -- i.e. author name, author email,
timestamp, our signatures -- they will differ from peer to peer. The `Tree`,
however, contains the metadata that we control and will be stable across the
signing process. So the identifier for `Tree`s will be the same from peer to peer.

So what we have to remember is that:
Commit histories will be different, but tree histories will be the same.

So if we want to ensure that peers are converging we just have to see that they
have the same identifiers for their trees. A fork can be identified by a
difference in tree identifiers. When that happens, it either calls for
convergence on signatures, or people to accept their new overlords.
