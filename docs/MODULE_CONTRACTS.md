# Module Contracts

Status: **ARCHITECTURAL RULE; binary layouts are provisional until implementation begins.**

## 1. Purpose

This page owns the interfaces between FLTF's major modules. It exists so any section can be developed/tested without requiring every other screen to exist.

## 2. Shared-state principle

Use a small set of canonical shared structures rather than ad-hoc globals.

Likely shared records:

- `GameState` — current mode/progression/high-level flags;
- `PlayerState[4]` — player identity, human/AI state, points/money/progression;
- `CarSetup[4]` — upgrades/parameters/livery identifiers;
- `EventState` — selected track/event/laps/difficulty/rules;
- `RaceSetup` — immutable/initial inputs needed by one race;
- `RaceResult` — finishing order, times, lap data and persistent consequences;
- `CommsContext` / `CommsResult`;
- `GarageContext` / result;
- `PreRaceContext` / result.

Do not freeze offsets until AMOS/data material and recovered race-state requirements are reviewed.

## 3. Race contract

The rest of FLTF should not depend on recovered Indy Heat globals directly.

Conceptually:

```text
Race_Init(RaceSetup*)
Race_Run()
Race_GetResult(RaceResult*)
Race_Shutdown()
```

The real assembly ABI may use registers/pointers differently, but the conceptual boundary should remain.

`RaceSetup` is expected to identify/provide:

- track package/data;
- 4 entrant/player/AI definitions;
- car setup/parameters;
- lap count/race rules;
- mode/difficulty flags;
- presentation/audio identifiers as needed.

`RaceResult` is expected to provide at least:

- finishing order/status;
- race times;
- fastest/best lap information where applicable;
- championship/arcade-relevant result data;
- any persistent car/player state the race is authorised to change.

## 4. Garage contract

Garage must operate on supplied player/car data and return changes. It must not require a live race module.

It should be possible to launch a garage harness with fabricated money/upgrade state.

## 5. Communications contract

Communications receives a selected encounter plus relevant player/game context and returns an explicit outcome. Conversation content/branching should be data-driven where practical.

No race-engine internal variable should be referenced directly.

## 6. Pre-race/menu/results contracts

Presentation modules may select or display shared data, but should not become the authority for race mechanics or championship calculation.

Where a screen needs calculated information, prefer a common/championship service to duplicating calculations in UI code.

## 7. Testability rule

Every major module should have at least one defined way to run without its normal predecessor/successor. This may be a debug menu, alternate entry point or build flag.

Document each harness here once created, including required inputs and expected outputs.
