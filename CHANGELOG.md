# Changelog

All notable changes to the Bakehouse plugins for VCV Rack.

## 2.0.0: first release

First public release of both plugins.

### Bakehouse (free): Whisk

- **Whisk**, a 12 HP dual-layer generative sequencer. Layer 1 and Layer 2 each
  generate a phrase in a shared root and scale and keep evolving it while it
  plays, and the two layers listen to each other so they cohere as a duet.
- Per layer: `PACE`, `DENS`, `OCT` and `DRIFT` knobs, a `GEN` button, an
  Anchored/Free `MODE` switch and a pulse light. A shared `SHIFT` latch gives
  the four knobs their second meanings: `PERS`, `LEN`, `RNG`, `SHP`.
- `SHIFT`+`GEN` steps a layer back through its own melody history.
- `CLK`, `RST`, `GEN` and `DRIFT` inputs; `CV` and `GATE` outputs per layer.
  The `GEN` and `DRIFT` inputs are assignable to Layer 1, Layer 2 or Both.
- **Gate length** and **Melody reuse** sliders per layer in the right-click
  menu, defaulting to 50% and 75%.
- Automatic root/scale sharing between Whisk instances, overridable with
  **Scale sync**.
- No knob or CV change is heard mid-note: the sounding note keeps its pitch and
  full length, and the change lands at the next onset.

### Bakehouse Treats (US $5): Whisk Expander

- **Whisk Expander**, a 20 HP Rack-only expander that mounts to a Whisk's right
  and turns it into an eight-scene launcher.
- Eight lit scene slots `A`–`H` with `SAVE`, and a `SCENE` CV input covering
  them across 0–10 V.
- A launch row that reads left to right: `PHRASE`/`NOTE` for when a scene
  arrives, `FLOW` for how long the changeover takes, `ALL`/`TUNE` for whether a
  launch restores the saved controls or refits the saved tune to the live ones.
- Independent per-layer Scale Shift, knob plus 1 V-per-step CV, clamped to one
  octave of the scale in play.
- Patch bay: `GEN LAYER 1`, `GEN LAYER 2` and `FLOW CV` in; `END LAYER 1`,
  `END LAYER 2` and `ARRIVE` out.
