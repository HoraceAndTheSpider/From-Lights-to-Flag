# Project Overview

## Working title

**From Lights to Flag**

## Core concept

A single-screen top-down Amiga racing game in the broad tradition of *Super Sprint*, *Indy Heat* and *Super Off Road*.

Four cars race simultaneously on one circuit. The intended player count is 1–4, with computer-controlled cars filling unused positions as appropriate.

## Game modes

Two high-level modes are planned.

### Arcade

A faster self-contained structure. Arcade mode may differ from Championship mode in:

- scoring;
- race/lap counts;
- upgrade availability and progression;
- event sequence;
- communications-screen use;
- persistence requirements.

Exact rules remain a game-design decision and should be data-driven where practical rather than compiled into unrelated engine code.

### Championship

A structured series using championship-specific data and presentation. Intended features include:

- teams/drivers;
- track/event sequence;
- points/scoring;
- upgrades/progression;
- communications encounters;
- championship-specific car graphics and other presentation assets.

The current distribution concept is:

- **Disk 1:** core game executable, common engine/data and common presentation assets.
- **Disk 2:** championship/content data such as tracks, team/driver information and car graphics.
- **HDD install:** the same logical content exposed through directories/files with loading optimised for hard-disk access.

This split is a design target, not yet a frozen disk layout.

## Communications screen

A non-racing interaction screen inspired in broad structure by *Super Cars II*. The player receives a situation/question and chooses an answer. Successful responses can produce rewards or other state changes.

The implementation should be its own game-state/module rather than race-engine special-case code. Dialogue data, answer options and outcomes should be external/data-driven where reasonable.

## Racing-engine reference

The separate `Indy-Heat-WHD` reverse-engineering project is an important technical reference for:

- single-screen circuit representation;
- surface/collision data;
- foreground/occlusion information;
- waypoints and AI route data;
- pits and start positions;
- race-state and lap presentation concepts;
- track-package/editor workflow.

From Lights to Flag will implement its own engine and assets. Indy Heat findings are reference evidence, not source code to transplant.

## Existing prototype material

The owner has already prototyped a number of game elements in AMOS. These should be treated as valuable behavioural/design references when supplied. They may define screen flow, game rules or presentation more accurately than early architecture assumptions.

## Initial target

Provisional baseline:

- Amiga 1200;
- AGA;
- stock 2 MB Chip RAM;
- 68EC020;
- PAL 50 Hz;
- no required accelerator, Fast RAM or FPU;
- floppy and HDD support.

Early art may originate within ECS-style colour/depth constraints and later be enhanced for AGA.
