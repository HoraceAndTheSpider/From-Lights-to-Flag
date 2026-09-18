# Open Decisions

Only decisions that materially affect design/implementation should remain here. When resolved, move the answer into the appropriate canonical document and note the date in the development log.

## A. Immediate decisions before the first playable engine slice

### A1. Race screen depth

Provisional recommendation: 320×256 PAL, 5 or 6 bitplanes for the race.

Need: representative track/car art before fixing 5 vs 6 planes. The choice affects palette freedom, Chip RAM, display DMA and blitter cost.

### A2. Car rendering method

Provisional recommendation: masked blitter BOBs first, with hardware sprites retained for later experiments/HUD/effects.

Alternative: AGA hardware sprites may be viable for four cars, but palette/pairing/width/overlap requirements should be proved with the actual car art before designing the engine around them.

### A3. Handling model

Need: owner-supplied AMOS prototype and/or description of intended steering, acceleration, collisions, sliding and upgrades.

The Indy Heat research can inform structure, but From Lights to Flag should not accidentally inherit handling behaviours the owner does not want.

### A4. Four-player adapter

Need: confirm the intended/common parallel-port four-player adapter standard and verify register/bit handling from a reliable hardware reference before coding it.

### A5. Toolchain

Provisional preference: a modern cross-build using VASM Motorola syntax and a Hunk executable, while keeping source readable for classic Amiga assemblers where practical.

Need to choose exact assembler/linker versions and include strategy before the first source delivery so build instructions remain stable.

### A6. OS-friendly vs full takeover boundary

Recommendation: use AmigaOS for startup/file loading and clean shutdown, then own the custom chipset during race/game screens as required for deterministic performance.

Need to define how much OS remains active during gameplay and how disk-change/loading transitions are handled.

## B. Content/data decisions

### B1. Disk 2 packaging

Options include ordinary files/directories or a custom grouped resource container. Do not freeze this until sample championship content gives realistic disk-size and file-count data.

### B2. Compression

No packer selected. Compare representative project data and depack speed on a stock 020 first.

### B3. Championship persistence

Need to decide whether championship state is saved to disk, represented by passwords/codes, or both. This affects write-protection expectations and disk layout.

### B4. Communications data format

Need to see the AMOS prototype/content. Prefer external data defining prompt, answers, outcomes and conditions rather than hard-coded dialogue branches.

## C. Presentation decisions

### C1. AGA enhancement level

Early assets may be ECS-oriented. Need to decide whether the release aesthetic aims for:

- mostly ECS-like race graphics with richer AGA menus;
- 64-colour AGA race art;
- heavier 256-colour use outside the race;
- other palette/copper enhancements.

### C2. PAL-only first release vs NTSC adaptation

Current baseline is PAL 50 Hz. NTSC support should be treated as a later explicit compatibility milestone rather than silently assumed.
