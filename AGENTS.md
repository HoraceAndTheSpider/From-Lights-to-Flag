# From Lights to Flag — AGENTS.md

This file is the mandatory starting point for any new ChatGPT/Codex thread working on **From Lights to Flag**.

## 1. Startup protocol

Before changing code or documentation:

1. Read this file in full.
2. Read `docs/HANDOVER.md`.
3. Read `docs/DEVELOPMENT_LOG.md` from newest entry backwards until the current milestone is understood.
4. Read `docs/TECHNICAL_ARCHITECTURE.md`, `docs/ASSET_PIPELINE.md`, `docs/SOURCES_AND_PROVENANCE.md` and `docs/OPEN_DECISIONS.md` as relevant.
5. Inspect the current repository branch and treat checked-in source as the implementation authority.
6. For racing mechanics and track data, consult the current Indy Heat research only where the local docs explicitly identify it as a reference. Do not re-investigate settled Indy Heat findings merely because this is a new thread.
7. State any important contradiction between code, docs and observed runtime behaviour before replacing a proven result.

## 2. Evidence hierarchy

Use this authority order when information conflicts:

1. Runtime behaviour on a real A1200 or a correctly configured emulator.
2. Reproducible build/test results from the current source.
3. Source/data proof from the current repository or explicitly referenced research repositories.
4. Current project documentation.
5. External reference material.
6. Assumptions or analogy with another game.

Label material where useful as:

- **RUNTIME-PROVEN** — demonstrated in the target runtime.
- **SOURCE-PROVEN** — directly established from source/data but not yet runtime-tested.
- **PROVISIONAL** — a deliberate working assumption awaiting proof.
- **REJECTED** — tested or investigated and shown not to be the implementation to use.

Never upgrade a provisional theory to a proven fact simply because it is plausible.

## 3. Collaboration style

The project owner wants a collaborative development process.

- Explain material architecture choices and trade-offs before silently locking them in.
- When more than one approach is genuinely viable, identify the alternatives and the practical consequence of each.
- Ask the owner where a decision materially affects game design, compatibility, presentation or workflow and existing project material does not already answer it.
- Do not repeatedly ask questions whose answers are already in the repo or current thread.
- Prefer tangible outputs: source, test data, build artefacts, diagrams/tables in docs, or small diagnostic tools.
- Keep prose concise but sufficiently developed to be useful in a future handover.
- Use British English in project documentation unless source syntax or a quoted external term requires otherwise.

## 4. Source-code delivery rule

While development is being conducted through ChatGPT rather than a repository-writing coding agent:

- **Every response that changes any `.asm` file must provide a ZIP containing the complete current set of project `.asm` files, not just the changed files or a patch.**
- Include any required `.i`/include files, build scripts and data definitions needed to build that source revision.
- The ZIP must contain a short manifest or development-log entry identifying what changed and what was actually tested.
- Do not claim a source revision assembles or runs unless it has actually been assembled/tested. If the environment lacks the toolchain, say so clearly and provide the exact intended build command.

The owner may manually upload delivered files to GitHub. Once work migrates to a coding agent with direct repository access, repository commits become the primary delivery mechanism, but complete source/build traceability remains mandatory.

## 5. Build and test discipline

Target baseline unless deliberately changed in `OPEN_DECISIONS.md`:

- Commodore Amiga 1200.
- Stock 2 MB Chip RAM.
- 68EC020 CPU; do not assume Fast RAM, FPU or accelerator.
- AGA chipset.
- PAL/50 Hz primary target.
- Hard-drive installation supported alongside floppy distribution.

For each meaningful code milestone, record:

- assembler/linker and version;
- command line or build script;
- emulator model/configuration or real-hardware configuration;
- disk/HDD launch method;
- observed result;
- unresolved defects or warnings.

Do not hide timing, memory, palette, DMA or compatibility regressions to make a milestone look complete.

## 6. Module and interface discipline

Prefer small modules with explicit responsibilities rather than one monolithic assembly source. Likely domains include:

- startup/shutdown and OS/hardware ownership;
- display/copper/blitter;
- input;
- audio/music;
- asset loading/depacking;
- game-state/mode control;
- race simulation;
- track package interpretation;
- car rendering;
- race HUD;
- menu/garage/upgrades;
- communications screen;
- championship persistence/scoring.

Exact file boundaries may evolve. Keep public entry points and shared structures documented. Do not duplicate constants or structure offsets across modules if they can live in a shared include.

## 7. Asset policy

Authoring assets may arrive as ILBM/IFF, 8SVX and ProTracker MOD.

- Preserve original authoring files.
- Prefer offline conversion to runtime-oriented planar/sample/module data where this lowers load-time or runtime overhead.
- Store converted/generated data separately from originals and make conversion reproducible.
- Do not introduce destructive palette changes without recording them.
- Compression is a distribution/loading concern, not an excuse to make runtime data opaque. Prefer raw/unpacked or rapidly loadable data on HDD; floppy builds may use compression where benchmarks justify it.
- Third-party players, depackers or snippets require a recorded source and licence before being committed/distributed.

## 8. Indy Heat relationship

The project may use the **documented behaviour and data-model lessons** learned from the separate Indy Heat Amiga reverse-engineering project as a design reference for single-screen racing mechanics, track representation, AI/waypoints, surfaces, pits and race presentation.

Do not copy or redistribute original Indy Heat copyrighted code or assets into this game. Re-implement required mechanics in original project source. Keep provenance clear enough that future maintainers can distinguish:

- facts learned from Indy Heat research;
- design decisions made for From Lights to Flag;
- original code/assets created for this project.

## 9. Documentation discipline

After each substantial investigation or implementation milestone:

- update `docs/DEVELOPMENT_LOG.md`;
- update the relevant technical document rather than leaving the result only in chat;
- update `docs/HANDOVER.md` so a fresh thread can resume without redoing settled work;
- add new external sources to `docs/SOURCES_AND_PROVENANCE.md`;
- move resolved questions out of `docs/OPEN_DECISIONS.md` and record the decision where it belongs.

Avoid proliferating overlapping documents. Prefer updating the existing canonical page for a subject.

## 10. Current project principle

Build a clean, data-driven Amiga racer first. Optimise against measured A1200 constraints, not nostalgia-driven assumptions. Preserve enough separation between engine, presentation and championship data that a second championship/content disk and an HDD installation can use the same core executable.
