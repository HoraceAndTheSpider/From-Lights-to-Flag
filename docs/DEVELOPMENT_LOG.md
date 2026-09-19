# Development Log

## 2026-09-19 — Architecture correction: extract/adapt actual Indy Heat race engine

### Owner clarification

The race-engine objective was corrected substantially:

- FLTF should **not merely imitate or clean-room reimplement Indy Heat mechanics**;
- the intention is to recover/extract the actual original Amiga Indy Heat racing-engine routines/data;
- reconstruct them into maintainable 68k source;
- preserve/prove original behaviour first;
- then adapt the recovered core for FLTF, including a larger race display/resolution and other intentional changes.

### Mandatory modularity clarified

Major sections must be independently developable/testable, including menu, pre-race, garage, communications and race.

They will exchange documented shared inputs/outputs rather than relying on each other's private implementation state. Stand-alone/direct-entry harnesses are an explicit development goal.

### Documentation changes

Updated the continuity pack to:

- replace the original "Indy Heat as design reference only" assumption;
- establish recovered-code provenance/proof rules;
- add `INDY_HEAT_ENGINE_RECOVERY.md`;
- add `MODULE_CONTRACTS.md`;
- add `INCOMING_MATERIAL.md` for the forthcoming AMOS prototype and prepared data;
- revise architecture/open decisions/asset pipeline/handover accordingly.

### Current coding state

No FLTF `.asm` files have yet been created or changed. Therefore there is no source revision to assemble/test in this pack.

### Next input expected

The owner intends to upload this documentation to GitHub together with:

- AMOS prototype code;
- substantial prepared data/assets.

The next work should begin with repository/material intake and reconciliation against the current Indy Heat research before committing shared structures or race-core modifications.

---

## 2026-09-18 — Initial project bootstrap / continuity pack

### Request established

The owner defined FLTF as a 1–4 player, four-car, single-screen top-down Amiga racer with Arcade and Championship modes, a *Super Cars II*-style communications screen, likely stock-A1200 AGA target, Disk 1 core game, Disk 2 championship/content and HDD support. Authoring assets are expected in ILBM, 8SVX and MOD formats, with existing AMOS prototypes to follow.

### Initial bootstrap created

Created root `AGENTS.md`, `agents.ai` pointer and initial project/architecture/assets/sources/open-decisions/handover docs.

### Superseded assumption

The 18 September pack described Indy Heat primarily as a behavioural/data-model reference and suggested reimplementing mechanics. That assumption is **superseded by the 19 September owner clarification** above.
