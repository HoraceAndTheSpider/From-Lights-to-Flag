# Development Log

## 2026-09-18 — Project bootstrap / continuity pack

### Request established

The owner defined the game as a 1–4 player, four-car, single-screen top-down racer for Amiga, broadly inspired by *Super Sprint*, *Indy Heat* and *Super Off Road*, with:

- Arcade and Championship modes;
- differing scoring/laps/upgrades between modes;
- a *Super Cars II*-style communications/question screen with rewards for successful responses;
- likely AGA/A1200 target on stock 2 MB memory;
- early ECS-oriented assets that can later be adapted/enhanced;
- Disk 1 containing the core game and Disk 2 containing championship/content data;
- HDD installation support;
- ILBM, 8SVX and MOD source assets;
- possible floppy compression where worthwhile but no requirement to impose that overhead on HDD loading;
- existing AMOS prototypes to be supplied later;
- Indy Heat reverse-engineering work to inform racing/track mechanics.

### Continuity/workflow established

Created:

- root `AGENTS.md` with mandatory startup protocol, evidence hierarchy, collaboration rules and complete-ASM-ZIP delivery requirement;
- `agents.ai` pointer because that filename appeared in the initial brief;
- project overview;
- provisional technical architecture;
- asset pipeline plan;
- sources/provenance log;
- open-decisions list;
- handover page.

### Repository access result

`https://github.com/HoraceAndTheSpider/From-Lights-to-Flag` returned 404 through public retrieval and the connected GitHub reader used in this thread. No existing repository file was therefore overwritten or assumed.

### External research checked

Reviewed the owner-supplied references sufficiently to classify their role:

- Codetapper: useful commercial-game technique/reverse-engineering reference;
- Stefano Coppi repository: educational Amiga assembly game-programming source/tutorial;
- Reaktor article: useful fundamentals for custom chipset, chip RAM, copper, DMA, bitplanes, CIA input and system restoration;
- EAB thread: direct fetch failed, but indexed references show a resource collection including Photon's materials, P61 and Nibbler candidates;
- Indy Heat wiki: current 18 September 2026 home page confirms runtime/source evidence discipline and documents current race/track/AI/editor findings.

### Architecture proposed (PROVISIONAL)

- A1200 / 68EC020 / AGA / 2 MB Chip RAM / PAL 50 Hz baseline.
- 320×256 race screen as starting point.
- Prefer 5/6 race bitplanes over automatically choosing 8, pending real art/profiling.
- Masked blitter BOBs as first car renderer.
- Double-buffer race display with dirty-rectangle restoration from an immutable track background.
- Semantic track data separated from visible art: surface map, foreground mask, waypoints, checkpoints, pits/start positions etc.
- Explicit game-state modules for race, garage, communications and championship flow.
- File/resource loader abstracts floppy vs HDD.
- Compression deferred until representative asset benchmarks exist.

### Not done / not claimed

- No assembly engine source has yet been created.
- No assembler/toolchain has been installed or executed in this ChatGPT environment.
- No AGA hardware takeover code is claimed working.
- No exact car physics model has been chosen.
- No final disk format or compression library has been selected.

### Next recommended milestone

**Milestone 0 — toolchain + safe AGA display/input bootstrap**

After the owner uploads this documentation and supplies any AMOS prototype/source/assets that should constrain the architecture:

1. freeze the assembler/build convention;
2. create the first complete ASM source tree;
3. open a PAL low-res screen or safely take over the display;
4. establish 50 Hz frame timing;
5. read two standard joysticks (then add four-player adapter support separately);
6. render a test race background and one movable masked car;
7. prove clean exit/restoration;
8. record exact memory use and emulator/real-hardware result.

Any response that changes `.asm` from that point onwards must include the complete ASM source ZIP required by `AGENTS.md`.
