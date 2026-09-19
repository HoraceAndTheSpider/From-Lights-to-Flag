# Technical Architecture

Status: **PROVISIONAL FLTF architecture; race-core recovery approach is now a firm project requirement.**

## 1. Platform baseline

Target a stock PAL A1200 first:

- 68EC020 CPU;
- AGA chipset;
- 2 MB Chip RAM only;
- 50 Hz primary update target;
- standard HDD/AmigaDOS development path plus floppy release support.

Do not assume Fast RAM, FPU, RTG, later CPUs or accelerator timing.

## 2. High-level module architecture

Treat FLTF as a set of cooperating modules around common platform services.

Conceptual flow:

```text
Boot/Common Services
       |
Main Menu / Mode Selection
       |
Pre-Race ---- Garage ---- Communications
       |          |              |
       +----------+--------------+
                  |
               Race
                  |
           Results/Post-Race
                  |
       Arcade/Championship Flow
```

This is a flow model, not a dependency graph. Garage, communications, race and presentation modules must be individually testable through harnesses/direct-entry builds.

## 3. Common services

Expected shared services include:

- startup/shutdown and OS/custom-chip ownership;
- display/copper/blitter primitives;
- memory management/allocation conventions;
- 1–4 player input abstraction;
- music/SFX;
- logical asset/resource loading;
- optional depacking;
- persistence/save services;
- global/shared game-state structures.

Modules should call these services through stable entry points rather than each implementing their own hardware/file logic.

## 4. Race module: recovered Indy Heat core

The race module is exceptional internally because its mechanics are intended to originate from recovered Indy Heat code.

Desired decomposition after recovery may include:

- race orchestration/state;
- vehicle movement and handling;
- player control interpretation;
- AI/waypoint steering;
- surface/environment response;
- collision/interactions;
- lap/checkpoint logic;
- pits/service behaviour;
- race timing/position/result logic;
- track semantic-data access;
- rendering/presentation wrappers.

File boundaries should follow proven dependencies rather than arbitrarily splitting original code too early.

### Recovery before adaptation

For a recovered subsystem:

1. locate the original routines/data;
2. map calling convention and state;
3. reconstruct labelled source;
4. prove expected behaviour;
5. isolate hard-coded original-game assumptions;
6. then apply FLTF changes.

Do not alter resolution constants, coordinate spaces or state formats during initial recovery unless necessary to get a test harness running and the change is documented.

## 5. Race/display coordinate separation

FLTF expects a larger race presentation than retail Indy Heat. The exact resolution remains open until original data assumptions and incoming art are reviewed.

Prefer to separate:

- simulation/world coordinates;
- track-data coordinates;
- display/screen coordinates;
- object-render coordinates.

If original Indy Heat mechanics use display coordinates directly, preserve them during recovery first, then identify and remove/parameterise those assumptions deliberately.

## 6. Display strategy

A provisional AGA race display remains low-resolution PAL, likely around 320×256 or another verified expanded viewport depending on the intended FLTF design and recovered engine constraints.

Do not assume eight bitplanes simply because AGA supports 256 colours. Race depth should be chosen from real asset requirements and measured DMA/blitter cost. Menus, garage and communications may use different depths.

Car/object rendering method is not yet frozen. The recovered Indy Heat presentation path must be understood before committing FLTF to a replacement renderer.

## 7. Track/data strategy

Because the race engine is being recovered, the first priority is to understand and support the actual data structures it consumes.

Where practical, FLTF track packages should ultimately separate visible presentation from semantics such as:

- foreground/occlusion;
- surface/traction;
- routes/waypoints;
- checkpoints/lap validation;
- start positions/headings;
- pit/service information;
- object/flagman/board positions;
- metadata.

However, do not prematurely invent a new format that forces unnecessary translation before the recovered engine is working. A conversion layer can bridge authored FLTF data to the recovered core.

## 8. Game-state/module interfaces

Each module should accept a context/input structure and return explicit output/state. Examples:

- `RaceSetup` -> race module -> `RaceResult`;
- `GarageContext` -> garage -> updated `PlayerState`/car setup;
- `CommsContext` -> communications -> outcome/reward result;
- `PreRaceContext` -> pre-race -> ready/selection state.

Exact binary layouts will be frozen only once source work begins. See `MODULE_CONTRACTS.md`.

## 9. Stand-alone test harnesses

Provide direct-entry or debug harnesses where useful, for example:

- race test: boot/load one track and start race immediately;
- garage test: fabricated players/resources, no championship required;
- communications test: select/cycle conversations directly;
- menu test: exercise navigation without loading a race;
- asset/display test: show a converted ILBM/palette/object set.

A harness may be a build flag, alternate entry point or small wrapper executable. Prefer whichever keeps shared production code unchanged.

## 10. Input

Abstract input behind four logical player/controller records.

Expected physical support:

- joystick ports 1 and 2;
- common Amiga four-player/parallel-port adapter for players 3 and 4;
- keyboard/debug controls during development if useful.

The exact adapter protocol must be verified before implementation.

## 11. Disk/HDD loading

Use a loader abstraction so gameplay modules request logical assets without depending on media layout.

Development/HDD builds should favour straightforward files and fast loading. Floppy builds may group and/or compress resources once representative data has been benchmarked.

Disk 2 should behave as a content package rather than requiring a second distinct engine executable wherever practical.

## 12. Memory planning

A stock 2 MB Chip RAM target requires explicit budgeting for:

- executable/code/data;
- race display buffers/background;
- recovered race-core state/data;
- current track semantics;
- car/object graphics;
- UI/module assets for the current state only;
- music/SFX/sample data;
- loader/depack scratch;
- stack/workspace.

Prefer state-based loading/unloading over retaining assets for unrelated modules.

## 13. Source organisation

Provisional structure once coding begins:

```text
src/
  main.asm
  common/
    constants.i
    structs.i
    macros.i
    system.asm
    display.asm
    blitter.asm
    input.asm
    loader.asm
    memory.asm
    audio.asm
  menu/
  prerace/
  garage/
  comms/
  race/
    race.asm
    recovered/
    adapters/
    render/
  results/
  championship/
  debug/
```

The `race/recovered/` area is intended to keep reconstructed original-engine material clearly separated from FLTF adapters/new code. Exact files will follow evidence from the actual recovery.
