# Project Overview

## Working title

**From Lights to Flag**

## Core concept

A single-screen top-down Amiga racing game in the tradition of *Super Sprint*, *Indy Heat* and *Super Off Road*.

Four cars race simultaneously. Intended player count is 1–4, with AI filling unused positions as required.

## Game modes

### Arcade

A faster/self-contained mode which may differ from Championship in scoring, lap counts, upgrades, event sequence, communications usage and persistence.

### Championship

A structured series with teams/drivers, event order, points, upgrades/progression, communications encounters and championship-specific presentation/content.

Current distribution concept:

- **Disk 1:** core executable, common engine/services and common presentation assets.
- **Disk 2:** championship/content package including tracks, teams/drivers, car graphics and related data.
- **HDD:** same logical content presented through files/directories with HDD-appropriate loading.

The disk layout is not yet frozen.

## Communications screen

A non-racing interaction inspired by the broad idea of *Super Cars II*: a situation/question with player responses and resulting rewards/penalties/state changes.

Communications is its own module and should be testable independently of the race engine.

## Race-engine strategy

The race module is intended to use the **actual Indy Heat Amiga racing engine as its starting point**, not merely imitate its style.

The project will recover/reconstruct the relevant Indy Heat routines and data, prove their behaviour where practical, then adapt them for FLTF. Expected recovered areas include, subject to evidence:

- vehicle movement/handling;
- steering, acceleration and deceleration;
- car/car and car/environment interactions;
- track/surface handling;
- AI/waypoint behaviour;
- checkpoints/laps;
- pits and race-state handling;
- race timing/position logic;
- any other tightly coupled mechanics needed for equivalent race operation.

FLTF changes such as increased screen resolution, revised input/player support, presentation, content packaging or game rules should be layered on after the original behaviour is understood and isolated.

## Modular development principle

Major areas must be independently developable and testable. Menu, pre-race, garage, communications, race, results and championship progression communicate through documented shared structures and explicit inputs/outputs.

A module should not need another unfinished module merely to be exercised. Debug/direct-entry harnesses are encouraged.

## Existing prototype/material

The owner has:

- AMOS prototype source covering a number of game elements;
- substantial prepared data/assets to be uploaded.

These materials should be inventoried before hard-coding behaviour that they may already define.

## Initial hardware target

Provisional baseline:

- Amiga 1200;
- AGA;
- stock 2 MB Chip RAM;
- 68EC020;
- PAL 50 Hz;
- floppy and HDD support;
- no required accelerator, Fast RAM or FPU.

Early graphics may be ECS-oriented before AGA enhancement.
