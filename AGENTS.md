# From Lights to Flag — AGENTS.md

This file is the mandatory starting point for any new ChatGPT/Codex thread working on **From Lights to Flag (FLTF)**.

## 1. Startup protocol

Before changing code or documentation:

1. Read this file in full.
2. Read `docs/HANDOVER.md`.
3. Read `docs/DEVELOPMENT_LOG.md` from newest entry backwards until the current milestone is understood.
4. Read `docs/TECHNICAL_ARCHITECTURE.md` and `docs/MODULE_CONTRACTS.md` before changing module boundaries or shared structures.
5. For race work, also read `docs/INDY_HEAT_ENGINE_RECOVERY.md` and the current authoritative Indy Heat research/wiki identified in `docs/SOURCES_AND_PROVENANCE.md`.
6. Review `docs/ASSET_PIPELINE.md`, `docs/INCOMING_MATERIAL.md` and `docs/OPEN_DECISIONS.md` as relevant.
7. Inspect the current repository branch and treat checked-in source plus runtime proof as implementation authority.
8. Do not repeat settled reverse engineering merely because work has moved to a fresh thread.
9. State material contradictions between source, docs and observed runtime behaviour before replacing a proven result.

## 2. Evidence hierarchy

Use this authority order when information conflicts:

1. Runtime behaviour on a real A1200 or correctly configured emulator.
2. Reproducible build/test results from the current FLTF source.
3. Runtime-proven Indy Heat behaviour for recovered race-engine functions.
4. Source/data proof from the current FLTF or Indy Heat research repositories.
5. Current project documentation.
6. External technical reference material.
7. Assumptions or analogy.

Label material where useful as:

- **RUNTIME-PROVEN** — demonstrated in the relevant target runtime.
- **SOURCE-PROVEN** — directly established from source/data but not yet runtime-tested.
- **RECOVERED-EQUIVALENT** — reconstructed from Indy Heat and demonstrated to preserve the relevant original behaviour.
- **FLTF-ADAPTED** — an intentional FLTF change to a recovered or new implementation.
- **PROVISIONAL** — deliberate working assumption awaiting proof.
- **REJECTED** — tested/investigated and shown not to be the implementation to use.

Never promote a plausible theory to proven fact without evidence.

## 3. Core race-engine objective

The FLTF race module is **not** intended to be a clean-room recreation merely inspired by Indy Heat.

The intended approach is to:

1. identify the actual Indy Heat racing-engine routines and required data;
2. reconstruct/extract them into maintainable labelled 68k source;
3. document their inputs, outputs, state, dependencies and assumptions;
4. prove recovered behaviour against the original game where practical;
5. isolate the recovered race core behind explicit FLTF interfaces;
6. then make intentional FLTF changes, including resolution/display changes and any revised game rules.

Do not casually rewrite a recovered mechanic just because a new implementation seems cleaner. Preserve known behaviour first; adapt second.

Keep recovered/original-derived material clearly identifiable from newly written FLTF code. Distribution/licensing implications are a separate release concern and must not be silently assumed resolved.

## 4. Mandatory modularity rule

FLTF must be developed so major game areas can progress independently.

Expected top-level modules include:

- title/menu/options;
- driver/team/mode selection;
- pre-race;
- garage/upgrades;
- communications;
- race;
- results/post-race;
- championship/arcade progression;
- common platform services (display, input, audio, loader, memory, persistence).

Rules:

- A module receives explicit inputs/shared state and returns explicit outputs/state changes.
- Do not make one unfinished screen/module a prerequisite for testing another unless a genuine shared platform dependency exists.
- Provide stand-alone test harnesses or direct-entry debug modes for modules where useful.
- Shared structures and constants belong in canonical includes, not duplicated local offsets.
- Avoid hidden writes into another module's private state.
- Changes to shared interfaces must be documented in `docs/MODULE_CONTRACTS.md`.

The race module may internally contain substantial recovered Indy Heat code, but the rest of FLTF must interact with it through documented FLTF contracts rather than depending on Indy Heat internals.

## 5. Collaboration style

The owner wants a collaborative development process.

- Explain material architecture choices and trade-offs before silently locking them in.
- When more than one viable approach exists, identify the alternatives and practical consequences.
- Ask the owner where a decision materially affects game design, compatibility, presentation or workflow and existing project material does not already answer it.
- Do not repeatedly ask questions already answered in repository material or the current thread.
- Prefer tangible outputs: source, test data, diagnostic builds/tools and concise canonical documentation.
- Use British English in project documentation unless syntax or an external term requires otherwise.

## 6. Source-code delivery rule

While development is being conducted through ChatGPT rather than a repository-writing coding agent:

- **Every response that changes any `.asm` file must provide a ZIP containing the complete current set of project `.asm` files, not just changed files or a patch.**
- Include required `.i`/include files, build scripts and data definitions needed for that revision.
- Include a manifest/development-log note identifying what changed and what was actually tested.
- Do not claim a source revision assembles or runs unless it has actually been assembled/tested.
- If the environment lacks the relevant toolchain, say so and provide the exact intended build command.

When work later migrates to a coding agent with direct repository access, repository commits may become the normal delivery mechanism, but complete traceability remains mandatory.

## 7. Build and test discipline

Target baseline unless deliberately changed in `OPEN_DECISIONS.md`:

- Commodore Amiga 1200;
- stock 2 MB Chip RAM;
- 68EC020 CPU;
- AGA chipset;
- PAL/50 Hz primary target;
- floppy distribution plus hard-drive installation.

For each meaningful milestone, record:

- assembler/linker and version;
- command/build script;
- emulator or real-hardware configuration;
- disk/HDD launch method;
- observed result;
- memory/timing measurements where relevant;
- unresolved defects/warnings.

Do not hide timing, memory, palette, DMA or compatibility regressions.

## 8. Recovered-code discipline

For every recovered Indy Heat routine or data structure entering FLTF, record at minimum:

- original address/range or other stable origin identifier;
- evidence/source used to identify it;
- original dependencies and global state accessed;
- reconstructed symbol names and structure offsets;
- known inputs/outputs/side effects;
- proof status;
- FLTF modifications, if any.

Prefer two-stage development:

**Stage A — recovery:** reconstruct and prove the original behaviour.

**Stage B — adaptation:** make FLTF-specific modifications and test each deliberate divergence.

When practical, retain a reference/recovery version or commit so regressions can be compared with the original behaviour.

## 9. Asset policy

Authoring assets may arrive as ILBM/IFF, 8SVX, MOD and prepared game-data files.

- Preserve original authoring/preparation files.
- Prefer reproducible offline conversion to runtime-oriented forms.
- Store generated data separately from originals.
- Do not introduce destructive palette/data changes without documenting them.
- Compression is a distribution/loading concern; HDD builds need not pay unnecessary depack overhead.
- Third-party players, depackers or source snippets require recorded origin/version/licence before public distribution.

## 10. Documentation discipline

After each substantial investigation or implementation milestone:

- update `docs/DEVELOPMENT_LOG.md`;
- update the relevant canonical technical document;
- update `docs/HANDOVER.md`;
- update `docs/INDY_HEAT_ENGINE_RECOVERY.md` for race-core recovery discoveries;
- update `docs/MODULE_CONTRACTS.md` for interface changes;
- add external sources to `docs/SOURCES_AND_PROVENANCE.md`;
- move resolved questions out of `docs/OPEN_DECISIONS.md`.

Avoid proliferating overlapping documents. Add a new canonical document only when it owns a distinct subject.

## 11. Current project principle

Build FLTF as a modular game around a recovered-and-adapted Indy Heat race core. Preserve original race behaviour where it is useful, isolate it behind FLTF module contracts, and change it deliberately rather than accidentally. Optimise against measured stock-A1200 constraints and keep content/data separable enough for Disk 2 championship packs and HDD installation.
