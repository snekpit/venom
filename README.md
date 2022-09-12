# venom

Early bringup recipes that demonstrate repros for papercuts/issues in the Serpent OS tooling.

This is a draft repo which will be deleted at some point in the not too distant future. Plan accordingly and don't get too attached to your work here.

## Scope

Terminal-only goodies that add value in a bootable systemd-nspawn container context. No graphical packages allowed at this stage.

The point of this repository is to have a collection of draft-quality recipes with which to flush out bugs and generate feature requests + PRs related to the tooling.

The goal is to eventually have all recipes work, at which point we can migrate them to either the main or the community recipe repos (depending on applicability)

## Structure

The goal is to be inspired by FreeBSD and [SolusOS2](https://github.com/SolusOS-discontinued/packages) and see where that gets us.

We're going to aim for consensus decisions to begin with, so everyone is expected to keep civil.

## Documentation

As the state of the tooling is still in flux, the best thing to do to get an idea for how things work is to look at the protosnek recipes which have been transplanted into the [main snekpit recipe repo](https://github.com/snekpit/main).

The other thing to do is to look at the macro `%actions` and `%(definitions) in the [boulder code repo](https://github.com/serpent-os/boulder/tree/main/data/macros).

The naming of concepts has been tweaked compared to what some of you might be used to, with the primary purpose being more sensible and clear semantics in terms of natural speech and its supporting mental models.

Additionally, it might be worth pointing out that _this is not $otheros!_

You are encouraged to forget everything you thought you knew about how things are supposed to work and be open to the different goals of Serpent OS which spawned the tooling you're about to use.  The fully fleshed out workflow is also not yet ready for you to use, so things will feel rather manual initially.

To get a basic recipe, use `boulder new -h` to get started. And no, boulder does not yet support git sources (the help info is lying to you!).

## Recipe licensing

We strongly prefer the Zlib license on code and recipes. `boulder new` has been updated to use a REUSE compliant Zlib header, but existing recipes will need to be updated with the following verbiage at the top:

    #
    # SPDX-FileCopyrightText: © 2020-2022 Serpent OS Developers
    #
    # SPDX-License-Identifier: Zlib
    #

## Wishlist items

- [x] golang (broken)
- [ ] readline (basis for a lot of stuff)
- 
