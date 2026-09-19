# Incoming Material Intake

Status: **READY FOR OWNER UPLOAD.**

The next repository update is expected to include AMOS prototype code and substantial prepared data. This page defines how it should be reviewed without losing provenance or prematurely redesigning it.

## 1. First-pass inventory

For every incoming file/folder, record:

- path/name;
- file type/format;
- purpose if known;
- whether it is authored FLTF material, recovered Indy Heat material, third-party support material or generated output;
- dimensions/size/record count where relevant;
- dependencies/related files;
- whether it is current, experimental or obsolete if that can be established.

## 2. AMOS prototype review

Extract/design-map at least:

- screen/state flow;
- menu/options behaviour;
- Arcade vs Championship rules;
- lap/scoring rules;
- player/team/driver selection;
- garage/upgrades and currencies/resources;
- communications questions/outcomes;
- pre/post-race flow;
- persistence/save assumptions;
- any race behaviour already prototyped;
- asset naming/ID conventions;
- any existing prepared data formats.

Do not assume AMOS implementation details must be copied literally into ASM. Treat it as behavioural/design authority where it expresses intended game behaviour.

## 3. Prepared race data review

Map supplied race/track data against:

- known Indy Heat structures already documented;
- recovered-core requirements;
- resolution assumptions;
- coordinate units/scales;
- surface/waypoint/checkpoint/pit/start semantics;
- expected editor/conversion workflow.

Where prepared data already solves a problem, adapt the engine/converter rather than throwing it away without cause.

## 4. Asset review outputs

After intake, update:

- `PROJECT_OVERVIEW.md` for confirmed game rules;
- `TECHNICAL_ARCHITECTURE.md` for confirmed technical constraints;
- `MODULE_CONTRACTS.md` for shared data structures;
- `ASSET_PIPELINE.md` for real formats/conversion steps;
- `OPEN_DECISIONS.md` to close questions now answered;
- `DEVELOPMENT_LOG.md` and `HANDOVER.md`.

## 5. Do not do on intake

- Do not bulk rename assets without preserving a mapping.
- Do not discard apparently redundant data before understanding consumers.
- Do not convert palettes/resolutions destructively.
- Do not fold recovered Indy Heat material into FLTF-authored data without provenance labels.
- Do not start rewriting the race engine until the current Indy Heat research state and incoming data have been reconciled.
