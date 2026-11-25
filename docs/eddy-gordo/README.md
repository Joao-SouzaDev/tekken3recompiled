# Eddy Gordo mod

Target: hybrid Tekken 3 Recompiled, USA SLUS-00402. Replace Eddy's appearance with a bald, bearded, bespectacled fighter with a very round torso, green Brazilian-themed shirt, black trousers and black/white shoes. Preserve original moves, timing and collision initially. No bag or lanyard.

## Verified baseline
`tools/MODEL_MAP.md` documents 52 3DMK records, 56-byte rows and bounded payload offsets; fighter identity, vertices, polygons and skeleton semantics remain unknown. Do not assume row indices are bones or assign an Eddy BNS ID without runtime evidence.

## Local investigation
1. Run `python -m unittest tools.tests.test_model_map -v`.
2. Run `python tools/model_map.py inventory --exe disc/SLUS_004.02 --source "disc/Tekken 3 (USA) (Track 1).bin" --json workspace/models/model-map.json --csv workspace/models/sections.csv` (adjust local paths).
3. Trace BNS record requests during character selection and battle with Eddy P1/P2; compare against another fighter and repeated runs. Record IDs, call sites and hashes, not retail bytes.
4. Correlate model parser reads with row offsets; prove coordinate stride, signedness, primitive indices, UV and transform semantics using controlled experiments. Build a read-only exporter only after evidence.
5. Create original low-poly geometry and textures, validate against proven constraints, then package using the existing guarded overlay tooling. If size constraints cannot be met, investigate runtime overrides separately.

## Acceptance
Stock game unchanged with mod disabled; Eddy appearance changes with mod enabled; no crashes or malformed primitives in selection, idle, ginga, kicks, sweeps, handstands, hit reactions and victory; original collision/timing retained. Test both player slots and outfits. Keep all retail extracts and disc images local and ignored. No game-ready asset or verified fighter ID exists yet.
