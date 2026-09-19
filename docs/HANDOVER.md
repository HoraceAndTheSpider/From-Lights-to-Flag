# Handover

## Current state — 19 September 2026

This is the second FLTF continuity pack. It corrects the most important architectural assumption from the initial bootstrap.

There is still **no FLTF ASM revision** to inherit yet.

## Read first

1. `/AGENTS.md`
2. `docs/PROJECT_OVERVIEW.md`
3. `docs/DEVELOPMENT_LOG.md`
4. `docs/INDY_HEAT_ENGINE_RECOVERY.md`
5. `docs/TECHNICAL_ARCHITECTURE.md`
6. `docs/MODULE_CONTRACTS.md`
7. `docs/INCOMING_MATERIAL.md`
8. `docs/OPEN_DECISIONS.md`
9. `docs/ASSET_PIPELINE.md`
10. `docs/SOURCES_AND_PROVENANCE.md`

## Critical correction from first bootstrap

**Do not treat Indy Heat merely as inspiration/reference for a newly written race engine.**

The intended race strategy is to recover the actual original Amiga Indy Heat racing engine, reconstruct it in maintainable 68k source, prove behaviour, then adapt it for FLTF.

The first pack's clean-room/new-engine wording is superseded.

## Modular architecture requirement

FLTF must allow independent work on:

- menus/options;
- pre-race;
- garage/upgrades;
- communications;
- race;
- results;
- championship/arcade progression.

Use documented shared structures and module inputs/outputs. Provide stand-alone/direct-entry harnesses when practical. The rest of FLTF should not depend directly on recovered Indy Heat globals.

## Platform baseline

Still provisional unless incoming material changes it:

- stock Amiga 1200;
- 68EC020;
- AGA;
- 2 MB Chip RAM;
- PAL 50 Hz primary target;
- floppy + HDD support.

The exact race resolution/bitplane/renderer strategy is deliberately reopened pending recovered-engine analysis and owner assets.

## Incoming material expected

The owner plans to upload:

- AMOS prototype source;
- substantial prepared data/assets;
- this documentation pack.

First action in the next thread should be to inventory that material, map its intended behaviour/data structures, and reconcile it with the current Indy Heat research state.

## Race-core next milestone

The first meaningful race milestone is **not** "write an Indy-like handling engine".

It is:

> Recover a minimal self-contained Indy Heat race-core slice and prove that one retail-equivalent player-controlled car can execute the original mechanics outside the normal Indy Heat front-end, with dependencies documented.

Then progressively add surfaces/collision, AI/multi-car, lap/checkpoint/pit/result logic and finally FLTF adaptations such as resolution/display changes.

## Other modules

Menu, garage, communications and other modules do not have to wait for race recovery. They may proceed in parallel once their inputs/outputs are established from the AMOS prototype/data.

## Delivery rule

Any future ChatGPT response changing `.asm` must provide the complete current ASM/include/build source set as a ZIP, with manifest and test status.
