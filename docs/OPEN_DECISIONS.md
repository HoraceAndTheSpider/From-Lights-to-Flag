# Open Decisions

Only unresolved decisions that materially affect implementation should remain here. Move resolved answers into their canonical documents and note them in the development log.

## A. Immediate technical decisions

### A1. Exact FLTF race resolution

The user intends a larger screen than retail Indy Heat. Need to establish:

- intended visible dimensions from AMOS/art/prepared data;
- which original Indy Heat coordinate assumptions are mechanic-critical versus presentation-only;
- bitplane/depth implications on stock A1200.

Do not fix this from aesthetics alone before recovery mapping.

### A2. Race renderer strategy

The first pack provisionally assumed masked BOBs/dirty restore. That is no longer a committed approach.

Need to understand the actual Indy Heat race renderer and determine whether to preserve, extend or replace it after the mechanics core is isolated.

### A3. Toolchain

Provisional preference: modern VASM-based cross-build with standard Amiga executable/output formats and reproducible scripts.

Need to choose exact assembler/linker/includes before first ASM delivery.

### A4. Four-player adapter

Need reliable specification of the intended/common parallel-port four-player adapter and exact register/bit handling.

### A5. OS/takeover boundary

Likely use AmigaOS for startup/loading/clean shutdown while owning custom chipset resources during demanding screens. Exact boundary remains to be designed/tested.

## B. Race-core recovery decisions

### B1. Minimum extracted core boundary

Need to derive from current Indy Heat call graph/runtime evidence: which routines/data must move together to get one controllable race car operating correctly outside the original front end.

### B2. Source representation of recovered code

Need to choose naming/commenting conventions and whether exact original instruction layout is retained initially or reconstructed semantically while preserving behaviour.

### B3. Original renderer versus new FLTF renderer

Do not decide until the original presentation path and resolution coupling are understood.

## C. Game/content decisions awaiting incoming material

### C1. Arcade and Championship rules

AMOS prototype/prepared data should confirm scoring, laps, progression, upgrades and communication-screen use.

### C2. Garage economy/upgrades

Need AMOS/data review.

### C3. Communications data format

Need AMOS/content review. Prefer external data once real structure is understood.

### C4. Championship persistence

Need to establish save/password/other intended behaviour.

### C5. Disk 2 packaging

Defer until actual content/file sizes and dependencies are inventoried.

### C6. Compression

No packer selected; benchmark representative project data first.

## D. Presentation

### D1. AGA enhancement level

Need real assets and AMOS screens before fixing race/menu/garage/comms colour depths and palette strategy.

### D2. PAL-only first release versus NTSC

Current baseline remains PAL 50 Hz. NTSC should be a later explicit compatibility decision.
