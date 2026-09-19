# Sources and Provenance

This page records external/recovered technical material and how it is used.

## Project repositories

### From Lights to Flag

`https://github.com/HoraceAndTheSpider/From-Lights-to-Flag`

Role: primary FLTF repository.

Bootstrap access on 18 September 2026 returned 404 through available readers. Re-check after the owner uploads the continuity pack and prototype/data.

### Indy Heat WHD / reverse engineering

`https://github.com/HoraceAndTheSpider/Indy-Heat-WHD`

Wiki:
`https://github.com/HoraceAndTheSpider/Indy-Heat-WHD/wiki`

Role: **primary technical source for recovering the actual Indy Heat race engine**, not merely a design reference.

Use the current master/wiki/tests/runtime handovers as authority and do not repeat settled research. As recovered functions enter FLTF, record origin address/range and proof in `INDY_HEAT_ENGINE_RECOVERY.md`.

Keep original-derived code/data distinguishable from FLTF-authored code. Public distribution/release rights are not assumed resolved by technical recovery alone.

## Amiga programming references supplied by the owner

### English Amiga Board thread 109752

`https://eab.abime.net/showthread.php?t=109752`

Role: collection of Amiga assembly-learning/resources/tool references. Follow candidates to primary source/version/licence before inclusion.

### Codetapper's Amiga Site

`https://codetapper.com/amiga`

Role: reverse-engineering/commercial Amiga technique reference, useful for understanding shipped implementations and extraction methods.

### Stefano Coppi — Amiga Assembly Game Programming Tutorial

`https://github.com/stefanocoppi/amiga_game_prog`

Role: educational Amiga assembly/game-programming source/tutorial. Review specific source and licence before reuse.

### Reaktor — Crash Course to Amiga Assembly Programming

`https://www.reaktor.com/insights-and-events/crash-course-to-amiga-assembly-programming`

Role: fundamental custom-chip/Chip RAM/copper/bitplane/DMA/CIA/startup-shutdown reference. Useful foundation, not a production AGA engine specification.

## Hardware/platform documentation to add

Before low-level AGA code is treated as source-proven, record exact editions/links for:

- Amiga Hardware Reference Manual / AGA register documentation;
- A1200/AGA-specific chipset details;
- Motorola 68020 programming/reference material;
- AmigaOS NDK includes/autodocs used by startup/loading;
- four-player adapter hardware/protocol reference.

## Provenance rule

For every imported/recovered source component, record:

- upstream/original source;
- exact address/version/commit where applicable;
- author/rights holder where known;
- licence/redistribution status where available;
- local reconstructed source location;
- FLTF modifications;
- where it is used;
- runtime/source proof status.
