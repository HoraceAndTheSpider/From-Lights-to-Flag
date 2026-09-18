# Sources and Provenance

This page records external technical references and how they are being used. It is not a licence to copy third-party game code or assets.

## Project repositories

### From Lights to Flag

`https://github.com/HoraceAndTheSpider/From-Lights-to-Flag`

Role: primary project repository.

Status at bootstrap (18 September 2026): the repository returned 404 through both public GitHub retrieval and the connected GitHub reader available in the initial ChatGPT thread. Therefore no pre-existing repository files were assumed. Re-check at the start of the next thread after the owner has uploaded this bootstrap pack.

### Indy Heat WHD / reverse engineering

`https://github.com/HoraceAndTheSpider/Indy-Heat-WHD`

Wiki:
`https://github.com/HoraceAndTheSpider/Indy-Heat-WHD/wiki`

Role: technical/design reference for the data model and behaviour of an existing single-screen Amiga racer.

Current wiki authority observed on 18 September 2026 states that current master, checked-in tests, current wiki and runtime-tested handover are authoritative, with live runtime behaviour the acceptance result when static assumptions disagree. Current work has established track/runtime setup, waypoint/AI behaviour, car/pit structures, race presentation/graphics and custom track/editor workflows. Do not restart settled investigations merely for this new game.

Use: learn structure/behaviour and design a new implementation. Do not copy or redistribute original game code/assets.

## Amiga programming references supplied by the owner

### English Amiga Board thread 109752

`https://eab.abime.net/showthread.php?t=109752`

Role: collection of Amiga assembly-learning resources/tools.

Retrieval note: direct fetch returned a gateway error in the bootstrap thread. Search results referencing the thread identify resources including Photon's MiniStartup/ASMSKOOL material, Asm-One/AsmPro/AsmTwo, P6112 and Nibbler. Any code/tool taken from those links must be followed to its primary source and licence before project inclusion.

### Codetapper's Amiga Site

`https://codetapper.com/amiga`

Role: reference material on commercial Amiga graphics techniques, reverse engineering, sprites, graphics/map extraction and programmer interviews.

Useful because it illustrates how shipped games balanced bitplanes, sprites and DMA rather than providing a ready-made AGA engine. Any game-specific material remains third-party reference material.

### Stefano Coppi — Amiga Assembly Game Programming Tutorial

`https://github.com/stefanocoppi/amiga_game_prog`

Role: educational source/tutorial repository for Amiga assembly game programming.

The repository describes itself as a beginner-oriented game-programming tutorial assuming Motorola 68000 assembly knowledge. Review specific source files and licences before reusing code rather than merely concepts.

### Reaktor — Crash Course to Amiga Assembly Programming

`https://www.reaktor.com/insights-and-events/crash-course-to-amiga-assembly-programming`

Role: clear reference for fundamental custom-chip programming and a simple OS-friendly startup/shutdown pattern.

Relevant topics in the article include:

- custom-chip register access;
- chip-memory requirements for copper/display data;
- bitplanes and modulo;
- display window/data fetch;
- DMA and interrupts;
- copper list construction;
- CIA input;
- vertical blank synchronisation concepts;
- restoring system state on exit.

Caution: the example is deliberately simple/educational and discusses a small ECS-style display. It is not sufficient by itself for an AGA production engine.

## Primary hardware documentation to add

Before AGA display code is treated as source-proven, add and cite the exact editions used for:

- Amiga Hardware Reference Manual / AGA register documentation;
- A1200/AGA chipset details (including BPLCON3/BPLCON4, FMODE and palette writes);
- Motorola 68020 programmer/reference material;
- AmigaOS NDK includes/autodocs for any OS/library calls used by startup/loading.

## Provenance rule

For every imported third-party source component, record:

- upstream URL/repository;
- exact version/commit where possible;
- author;
- licence;
- local modifications;
- where it is used.

Do not copy third-party source into the project based only on a forum post or code fragment without checking redistribution terms.
