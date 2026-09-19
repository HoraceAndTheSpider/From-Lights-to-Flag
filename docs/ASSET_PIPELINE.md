# Asset and Data Pipeline

Status: **PROVISIONAL until the incoming AMOS prototype and prepared data are inventoried.**

## 1. Principle

Preserve source/preparation material, but generate runtime forms suited to a stock A1200. Conversion should be reproducible and should not destroy the owner's authored/prepared inputs.

## 2. Incoming material categories

Expected inputs now include:

- AMOS prototype source/data;
- ILBM/IFF graphics;
- 8SVX sound effects;
- ProTracker MOD music;
- prepared track/race data;
- prepared menus, garage, communications, championship or driver/team data;
- material derived from the separate Indy Heat reverse-engineering project where relevant.

Inventory first; do not convert everything blindly.

## 3. ILBM/IFF graphics

For each asset record dimensions, planes, palette, masking/transparency, role and ownership/source.

Likely offline outputs may include:

- planar BODY data in the exact required layout;
- palette blocks;
- BOB/object masks;
- frame metadata/anchors;
- pre-shifted variants only if measured worthwhile;
- separate semantic masks/maps where art and mechanics differ.

Menus/comms/garage may use different display depths from the race.

## 4. Race graphics and recovered engine

Do not force incoming FLTF race graphics into a speculative format before the recovered Indy Heat renderer/data path is understood.

There may be three useful stages:

1. original Indy Heat-compatible data for recovery tests;
2. an FLTF adapter/converter feeding the recovered core;
3. a later FLTF-native representation where an intentional engine/display change justifies it.

## 5. 8SVX

Offline conversion should normally extract signed 8-bit PCM plus playback/loop metadata required by Paula. Sample data needed for DMA must reside in Chip RAM.

## 6. MOD

Keep conventional MOD files if the selected replay routine can consume them efficiently. Record player version/licence and measure memory/CPU using representative music.

## 7. Track/content packages

The eventual FLTF track package should be driven by what the recovered core requires and what the owner's existing prepared data already contains.

Likely logical elements include:

- visible track/background;
- palette;
- foreground/occlusion data;
- surface map;
- routes/waypoints;
- checkpoints;
- starts/headings;
- pits/service data;
- race objects;
- event/track metadata.

Do not discard prepared data simply because it differs from an early proposed format; map it against engine requirements first.

## 8. Disk 2 championship/content

Disk 2 is expected to carry data/content rather than a separate engine where practical:

- track packages;
- event order;
- driver/team records;
- portraits/presentation;
- car graphics/liveries;
- communications content;
- championship rules/scoring/setup.

## 9. Compression

Choose compression per resource after measuring packed size, 020 depack time, scratch memory and load context. HDD versions should not be forced through unnecessary compression/decompression merely to mirror floppy layout.

## 10. Reproducibility

Converters should eventually be deterministic command-line tools/build steps. Generated runtime assets must be reproducible from preserved originals/preparation inputs without manual hex edits.
