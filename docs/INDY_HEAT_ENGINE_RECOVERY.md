# Indy Heat Race-Engine Recovery

Status: **PROJECT REQUIREMENT — detailed recovery map to be populated from the Indy Heat research repository and runtime work.**

## 1. Objective

Recover the actual Amiga *Indy Heat* race-engine routines/data required to reproduce its racing behaviour, reconstruct them into maintainable 68k source, and adapt that core for FLTF.

This is intentionally stronger than using Indy Heat merely as design inspiration.

## 2. Recovery principles

- Preserve original behaviour before changing it.
- Record concrete origin addresses/ranges and dependencies.
- Name routines/structures according to demonstrated purpose, not guesswork.
- Keep uncertain fields explicitly marked.
- Use existing Indy Heat wiki/tests/runtime proofs instead of restarting settled research.
- Separate recovered code from FLTF-specific wrappers/adaptations.

## 3. Candidate recovery domains

The exact boundary must follow evidence, but expected domains include:

- race initialisation/reset;
- car state/update loop;
- steering/acceleration/braking;
- rotation/heading/speed handling;
- surface effects;
- car/environment collision;
- car/car interaction;
- AI/waypoint route processing;
- checkpoints/lap progression;
- race position/finish state;
- pits/service behaviour;
- race timing/records where coupled to mechanics;
- track-object interactions required by the race core.

Rendering, HUD and front-end presentation may be replaced/adapted more aggressively once mechanics are isolated.

## 4. Recovery record template

For each routine/subsystem record:

```text
Name:
Original address/range:
Evidence:
Status: SOURCE-PROVEN / RUNTIME-PROVEN / RECOVERED-EQUIVALENT
Inputs:
Outputs:
Registers clobbered:
Globals/structures read:
Globals/structures written:
Calls/dependencies:
Timing/ordering assumptions:
Original display/coordinate assumptions:
Reconstructed source location:
FLTF changes:
Tests:
Open questions:
```

## 5. Recovery sequence

Preferred sequence:

1. identify a minimal race entry/update path;
2. map car/race state structures and call graph;
3. reconstruct one-car player-controlled operation;
4. recover surfaces/collision needed for correct handling;
5. recover AI/waypoints and multi-car interaction;
6. recover laps/checkpoints/pits/result state;
7. isolate original display/front-end dependencies;
8. provide a FLTF `RaceSetup`/`RaceResult` adapter;
9. then adapt display resolution, player count/input and FLTF-specific rules.

The exact ordering may change where dependencies prove different.

## 6. Resolution adaptation

The user explicitly intends an increased FLTF race-screen resolution.

Do not assume this is only a renderer change. During recovery, identify every constant/structure tied to:

- screen width/height;
- clipping bounds;
- track bitmap dimensions;
- object coordinate origin;
- collision/surface-map dimensions;
- viewport/layout offsets;
- HUD reserve areas;
- waypoint/track coordinate scaling.

First prove what Indy Heat actually does. Then decide which values remain race-world semantics and which become FLTF presentation parameters.

## 7. Integration boundary

Recovered code should ultimately sit behind FLTF-owned wrappers/interfaces. Other modules should not need original Indy Heat address constants or private global structures.

A likely source separation is:

```text
src/race/recovered/   ; reconstructed original-engine logic
src/race/adapters/    ; FLTF state <-> recovered-core translation
src/race/render/      ; FLTF display/presentation changes
```

## 8. Rights/provenance note

Recovered code is third-party-origin material. Keep provenance explicit. The project may perform technical recovery/integration work, but public redistribution/release rights for original-derived code/assets must not be assumed resolved merely because recovery is technically successful.
