# Asset Pipeline

Status: **PROVISIONAL** until representative project assets are supplied and measured.

## 1. Principle

Keep authoring formats convenient for artists/musicians, but make runtime formats convenient for a stock A1200.

Original assets should remain available unchanged. Runtime conversion should be reproducible from source assets.

## 2. ILBM/IFF graphics

Expected authoring format: ILBM.

Likely offline processing steps:

1. validate dimensions, bit depth and palette;
2. preserve the source file;
3. extract/convert planar BODY data into the exact layout required by the relevant screen/object renderer;
4. generate masks for BOBs where required;
5. generate compact semantic masks/maps separately when they are game data rather than visible art;
6. optionally pack the runtime payload for floppy distribution;
7. emit a manifest containing dimensions, planes, palette count, byte sizes and source file/hash.

Avoid runtime ILBM parsing for hot-path objects. Loading/parsing an ILBM at a screen transition may be acceptable during prototyping, but the release pipeline should favour direct runtime data.

### Race backgrounds

A 320×256 bitmap uses approximately:

- 5 planes: 50 KiB;
- 6 planes: 60 KiB;
- 8 planes: 80 KiB.

This excludes palette, copper, masks and buffers. These figures are useful when deciding whether extra colours justify the DMA/memory cost.

### Cars and track objects

For blitter BOBs, generate:

- planar image data;
- mask data suitable for the selected cookie-cut/blit method;
- frame metadata (width, height, modulo/alignment, anchor point);
- optional collision footprint independent of the visual mask.

Pre-shifted variants may improve speed but multiply memory usage. Do not adopt them until car size/frame count and measured blitter cost are known.

## 3. 8SVX sound effects

Expected authoring format: 8SVX.

Offline conversion should extract:

- signed 8-bit PCM sample bytes;
- playback period/frequency information;
- loop start/length if used;
- nominal volume;
- sample name/ID.

Paula DMA requires sample data in Chip RAM. Do not retain IFF chunk overhead in runtime memory unless a loader has a specific reason to do so.

## 4. MOD music

Expected authoring format: ProTracker-compatible MOD.

The module may remain in a conventional MOD layout if the selected replay routine consumes it directly. The replay routine and module memory footprint must be measured with realistic songs.

Candidate replay code mentioned by the supplied Amiga programming resources includes the P61 family. Treat this only as a candidate until its exact version, integration method and licence/distribution terms are recorded.

## 5. Track package

The release track package should separate visible art from race semantics. Candidate logical members:

- `track_bitmap`;
- `track_palette`;
- `foreground_mask`;
- `surface_map`;
- `waypoints`;
- `checkpoints`;
- `start_positions`;
- `pit_data`;
- `track_objects`;
- `track_meta`.

The on-disk representation may eventually be a directory of files or a compact container. Keep the in-memory APIs independent of that packaging choice.

## 6. Championship/content disk

Disk 2 is expected to supply championship/content data rather than another executable copy wherever practical. Candidate data:

- track packages;
- event order;
- driver/team records;
- driver/team portraits or presentation art;
- car graphics/liveries;
- communications data;
- championship scoring/setup data.

The loader must fail gracefully if the required volume/content is unavailable and prompt for the expected disk rather than assuming a fixed drive number.

## 7. Compression policy

Do not compress merely because the release uses floppy disks.

Choose per resource after measuring:

- packed size;
- 68EC020 depack time;
- scratch memory;
- whether the load occurs during a tolerated transition or during gameplay;
- HDD penalty/benefit.

The supplied EAB resource list references Nibbler as a fast Amiga cruncher/depacker; it is a research candidate, not yet a dependency. Other packers/depackers should be compared on project data before a choice is recorded.

## 8. Reproducibility

Every converter should eventually support a deterministic command-line build. Generated runtime assets should be replaceable from originals without manual hex editing.
