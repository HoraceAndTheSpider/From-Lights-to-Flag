# Handover

## Current state — 18 September 2026

This is the initial continuity pack for **From Lights to Flag**. There is no engine revision to inherit yet.

### Read first

1. `/AGENTS.md`
2. `docs/PROJECT_OVERVIEW.md`
3. `docs/DEVELOPMENT_LOG.md`
4. `docs/TECHNICAL_ARCHITECTURE.md`
5. `docs/OPEN_DECISIONS.md`
6. `docs/ASSET_PIPELINE.md`
7. `docs/SOURCES_AND_PROVENANCE.md`

### Current authority

The owner's initial brief plus these docs define the current project intent. Once source exists, current repository source and runtime test results outrank provisional architecture prose.

### Important project requirements

- Game: four-car single-screen top-down racer, 1–4 players.
- Main modes: Arcade and Championship.
- Communications/question screen can affect player rewards/progression.
- Likely target: stock 2 MB A1200, AGA, 68EC020, PAL 50 Hz.
- Disk 1 core game; Disk 2 championship/content concept; HDD install supported.
- Authoring assets: ILBM, 8SVX and MOD.
- Use Indy Heat research as a reference for track/race mechanics, not as code/assets to redistribute.
- The owner has AMOS prototypes that should be reviewed before hard-coding game behaviour.
- Keep documentation up to date so new threads do not redo settled investigation.
- Any ChatGPT response modifying ASM must provide a complete ZIP containing all current project `.asm` files and required build/include files.

### Current provisional technical direction

- 320×256 PAL race display.
- 5/6 bitplanes preferred as the first race target pending actual art/profiling; richer bit depth may be used on non-race screens.
- Cars initially planned as masked blitter BOBs.
- Race buffers use dirty-region restoration from a pristine track bitmap rather than a full-screen copy every frame, subject to profiling.
- Track packages keep visible background separate from semantic foreground/surface/waypoint/checkpoint/pit/start data.
- Ordinary AmigaDOS file loading first; disk/HDD differences hidden behind a loader API.
- No compression choice until measured on project data.

### Known access issue

During bootstrap, the new `From-Lights-to-Flag` GitHub URL returned 404 through public and connected GitHub retrieval. Re-check repository access in the next thread. Do not infer that the repository is empty once the owner has uploaded this pack.

### Immediate next task

Review any newly uploaded repository files and owner-supplied AMOS prototype/assets. Then resolve the toolchain/display-depth decisions and build **Milestone 0: safe AGA bootstrap + frame timing + joystick input + one background + one movable masked car**.

Do not jump directly into championship/comms implementation before the low-level display, input, memory and asset-loading foundations are proven.
