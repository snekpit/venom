# venom

Early bringup recipes intended to demonstrate fitness for purpose of the Serpent OS tooling.

This is a draft repo which will be deleted at some point in the not too distant future. Plan accordingly and don't get too attached to your work here.

## Scope

Terminal-only goodies that add value in a bootable systemd-nspawn container context. No graphical packages allowed at this stage.

The point of this repository is to have a collection of draft-quality recipes with which to flush out bugs and generate feature requests + PRs related to the tooling.

The goal is also to eventually have all recipes work, at which point we can migrate them to either the main or the community recipe repos (depending on applicability)

### Recipe tree structure

The goal is to be inspired by the [SolusOS2](https://github.com/SolusOS-discontinued/packages) organisation and the [Exherbo git monorepo trees](https://git.exherbo.org/) and see where that gets us.

Note that `base/` is reserved for critical, self-hosting systemd-nspawn container stuff that must always be in working order. A good example would be `readline`, because shells and compilers included in the self-hosting systemd-nspawn containers set rely on it.

We're going to aim for consensus decisions to begin with, so everyone is expected to keep things civil. That said, if the BDFL chips in, his decisions take precedence.

EDIT: Log of discussion in serpentos-devel on matrix:

```
livingsilver94
tbh I think think categorization is strictly personal subject.
The only tech reason is the limit in GH visualization and performance of directory walking.
we have a dictator for a reason :3
Ikey Doherty
yeah, I want to limit depth for that reason
finding the ymls + bins will take too long
good point
ideally 1 dir, max 2.
there.
if i dont like where something is ill just move it
and we'll organise as we go
sound good?
livingsilver94
perf. So now libmicrohttpd goes in net-libs and fuck everything till you decide differently
Ikey Doherty
grand
otherwise we'll be hung up for days deciding semantics
when its just a git mv away
```

### Package wishlist

There's a package list in [issue #1](https://github.com/snekpit/venom/issues/1)

If you encounter specific issues with moss or boulder, report them first in the serpentos-dev matrix channel in our [matrix space](https://matrix.to/#/!trFJOzhpDUejJKnPYg:matrix.org) and then go from there in terms of potentially capturing issues for the relevant tool in their respective code repos.

## Documentation

As the state of the tooling is still in flux, the best thing to do to get an idea for how things work is to look at the protosnek recipes which have been transplanted into the [main snekpit recipe repo](https://github.com/snekpit/main).

The other thing to do is to look at the macro `%actions` and `%(definitions)` in the [boulder code repo](https://github.com/serpent-os/boulder/tree/main/data/macros).

The naming of concepts has been tweaked compared to what some of you might be used to, with the primary purpose being more sensible and clear semantics in terms of natural speech and its supporting mental models.

Additionally, it might be worth pointing out that _this is not $otheros!_

You are encouraged to forget everything you thought you knew about how things are supposed to work and be open to the different goals of Serpent OS which spawned the tooling you're about to use.  The fully fleshed out workflow is also not yet ready for you to use, so things will feel rather manual initially.

### How to get started writing a recipe

To get a basic recipe, use `boulder new -h` to get started. And no, boulder does not yet support git sources ([issue](https://github.com/serpent-os/boulder/issues/25)).

### The recipe `pkg/` dir and `%(pkgdir)`

Place extra files such as patches, vendor configs etc. in the `pkg/` dir inside the  recipe dir.  Files inside `pkg/` will automatically be copied over to  `%(pkgdir)` during boulder builds, from where each can be referenced as `%(pkgdir)/path/filename` in the recipe.  The directory name `pkg/` was chosen because it's short and stands out in `tree` invocations.

### What to commit

    git add stone.yml manifest.x86_64.bin manifest.x86_64.jsonc

- `manifest.x86_64.bin` Binary moss readable file used to create moss collection stone.index files for dep resolution etc.
- `manifest.x86_64.jsonc` Human readable version of manifest.bin used for git diff introspection purposes
- `stone.yml` The actual build recipe

### Commit messages

Use a `category/pkg: verb <foo>` format with one commit per package change.

Example: `shells/fish: Add vX.Y` or `shells/fish: Update to vX.Y` or `shells/fish: Fix (...)`

Bump release for functional recipe changes only; do not bump release for no functional change commits (documentation typos, formatting).

No functional change commits use the [NFC] tag: `shells/fish: [NFC] Tweak comments`.

### Recipe licensing

We strongly prefer the Zlib license on code and recipes due to its uncomplicated nature. `boulder new` has been updated to use a REUSE compliant Zlib header, but existing recipes will need to be updated with the following REUSE-compliant verbiage at the top:

    #
    # SPDX-FileCopyrightText: © 2020-2022 Serpent OS Developers
    #
    # SPDX-License-Identifier: Zlib
    #
