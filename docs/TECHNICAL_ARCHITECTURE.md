# Technical Architecture

Status: **PROVISIONAL architecture baseline — no engine code is yet claimed as runtime-proven.**

## 1. Platform baseline

Target a stock PAL A1200 first:

- 68EC020 CPU;
- AGA chipset;
- 2 MB Chip RAM only;
- 50 Hz game update target;
- standard AmigaDOS launch for early development and HDD compatibility.

Avoid dependencies on Fast RAM, FPU, RTG, later CPUs or accelerator-specific timing.

## 2. Display strategy

### Race display

Start performance planning around a low-resolution PAL single-screen race display, provisionally **320×256**.

Do **not** assume that an AGA game must use eight bitplanes for racing. Eight 320×256 planes consume about 80 KiB per screen buffer before any masks, backgrounds, sprites, audio or game data are counted, and additional planes increase display DMA and blitter work.

A provisional race target of **5 or 6 bitplanes (32/64 colours)** is therefore preferred for the first engine milestone. AGA still provides a much larger palette and better colour control than ECS while preserving more DMA/blitter time for cars and effects.

Menus, garage and communications screens may use a different depth (potentially 8 bitplanes/256 colours) if profiling shows that this is useful and affordable.

### Buffering and moving objects

The circuit is largely static while cars/objects move. A promising first implementation is:

- immutable background bitmap for the loaded circuit;
- two displayed/draw race buffers;
- before drawing a car into the non-visible buffer, restore the object's previous dirty rectangle in that buffer from the immutable background;
- blitter-draw masked car/object BOBs;
- swap buffers on vertical blank.

This avoids copying the entire track bitmap every frame while keeping object rendering flexible.

Hardware sprites remain available for experimentation (HUD markers, cursor, effects or possibly cars), but four car BOBs are the safer first architecture because they are not constrained by sprite pairing, width, palette allocation or multiplexing rules.

## 3. Track data model

Borrow the useful separation established by the Indy Heat research, but define an original project format.

A loaded track package is expected to contain some or all of:

- background/race bitmap;
- palette;
- foreground/occlusion mask (likely 1 bpp or another compact mask);
- surface/traction map (compact packed values rather than display pixels where possible);
- AI waypoint/routes;
- checkpoints/lap validation data;
- start-grid positions and headings;
- pit positions/route/service data;
- lap tower/flagman/track-object positions if the selected presentation uses them;
- minimap/map data if needed;
- track metadata such as name, laps and event identifiers.

Keep display art separate from semantic race data. The engine must not need to infer road behaviour from pixel colours at runtime.

## 4. Race simulation

The race simulation should operate in fixed-point integer maths suitable for the 68020.

Likely per-car state includes:

- world/screen X/Y at sub-pixel precision;
- heading/rotation frame;
- velocity/speed;
- steering input;
- acceleration/braking state;
- current surface;
- route/waypoint target for AI;
- lap/checkpoint state;
- pit state;
- damage/fuel/tyres/upgrades only if selected game rules require them.

The exact fixed-point format and handling model remain open until the AMOS prototype and current Indy Heat findings have been reviewed together.

## 5. Input

Abstract player input behind four logical controller records.

Initial intended physical sources:

- joystick ports 1 and 2;
- a conventional Amiga four-player/parallel-port joystick adapter for players 3 and 4.

Keyboard/debug input may be supported during development but must not be required for normal four-player play.

The exact multiplayer-adapter electrical/register protocol must be verified before implementation.

## 6. Game-state architecture

Use an explicit high-level state machine. Candidate states:

- boot/load;
- title/intro;
- main menu;
- mode/championship selection;
- driver/team selection;
- garage/upgrades;
- communications;
- track loading;
- pre-race/grid;
- race;
- results;
- championship standings/progression;
- game over/championship complete.

Each state should expose clear init/update/render/exit responsibilities or an equivalent interface. Race-specific code should not own unrelated menu/dialogue progression.

## 7. Disk and HDD loading

Use a loader abstraction so gameplay code requests logical assets without caring whether they came from floppy or HDD.

Early development should favour ordinary AmigaDOS files because this gives:

- simple CLI/HDD testing;
- easier iteration;
- a path to standard install tools;
- less risk than designing a custom raw-disk filesystem before content size is known.

A future floppy build may use compressed payloads or grouped resource files. HDD builds should prefer uncompressed/preconverted data where that materially reduces CPU overhead and seek complexity.

Do not choose a packer until representative ILBM, MOD, 8SVX and track packages can be benchmarked for size and 020 depack speed.

## 8. Memory planning

The 2 MB Chip RAM target makes a memory map mandatory before content grows.

Track at minimum:

- executable/code/data;
- two race buffers;
- immutable track background;
- palette/copper list(s);
- car/object graphics and masks;
- foreground mask;
- surface map;
- waypoint/checkpoint structures;
- audio channels/sample data;
- music/module/player workspace;
- decompression/load scratch buffer;
- mode/UI assets;
- stack and general work memory.

Prefer loading only the current track/event presentation rather than retaining multiple tracks in memory.

## 9. Audio

Plan separate APIs for:

- music/module playback;
- sound effects/8SVX-derived samples;
- master enable/disable and state transitions.

A ProTracker-compatible replay routine such as a suitable P61-family player is a candidate, not yet a committed dependency. Source and licence must be checked before inclusion.

8SVX authoring files should normally be converted offline to the signed 8-bit PCM and metadata expected by Paula rather than parsed as IFF during every playback operation.

## 10. Timing

Target one deterministic simulation update per PAL frame initially. Rendering and audio must be profiled against the 50 Hz budget.

Do not make game physics depend on emulator host speed or uncalibrated busy loops. Vertical blank interrupt or equivalent frame synchronisation will be required for the finished engine.

## 11. Source organisation

A likely modular split once coding begins:

- `main.asm` — entry point and top-level state dispatch;
- `system.asm` — OS ownership, interrupts, shutdown;
- `display.asm` — copper, bitplanes, buffering;
- `blitter.asm` — common blitter helpers;
- `input.asm` — 1–4 player input;
- `loader.asm` — filesystem/resource loading;
- `depack.asm` — optional packed-resource interface;
- `audio.asm` / `music.asm` — Paula SFX and MOD playback;
- `game_state.asm` — global mode/state transitions;
- `race.asm` — race orchestration;
- `car.asm` — car simulation/render data;
- `track.asm` — track semantic data and queries;
- `ai.asm` — waypoint/AI steering;
- `hud.asm` — race presentation;
- `garage.asm` — upgrades;
- `communications.asm` — question/answer screen;
- `championship.asm` — championship state/scoring.

This is a responsibility map, not yet a frozen filename list.
