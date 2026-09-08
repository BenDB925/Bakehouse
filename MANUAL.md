# Bakehouse — user manual

Whisk and the Whisk Expander for VCV Rack 2.

- **Whisk** is free. It is a complete, self-contained generative sequencer.
- **Whisk Expander** is a separate paid plugin (US $5) that adds an eight-scene
  launcher, per-layer pitch shifting and a small patch bay to Whisk.

You never need the Expander. Whisk generates, evolves and plays both of its
layers on its own, and everything in the Whisk section below works with no
Expander installed and no Expander plugin bought.

**Contents** — [Whisk](#whisk) · [Whisk Expander](#whisk-expander) ·
[Scale sync](#scale-sync) · [Support](#support)

---

## Whisk

*Free plugin `Bakehouse` · 12 HP · Sequencer, Random*

Whisk runs **two independent melodies** — **Layer 1** and **Layer 2** — in one
shared scale. Each layer generates a phrase and then keeps evolving it while it
plays: small changes mostly, occasionally something bolder, always finding its
way home. The two layers listen to each other, so in one patch they cohere into
a duet rather than two unrelated lines.

Patch a clock in, take pitch and gate out of each layer into a voice, press
`GEN`, and turn `DRIFT` up when you want the tune to start travelling.

### Global controls

| Control | What it does |
| --- | --- |
| `ROOT` | Tonic of the scale, `C` to `B`. |
| `SCALE` | Major, Minor, Dorian, Mixolydian, Pent. Major, Pent. Minor, Blues, Chromatic. |
| `SHIFT` | Latch. While it is lit, the four per-layer knobs of **both** layers change meaning (see below). Nothing moves until you turn a knob. |
| `+ EXPANDER` / `− EXPANDER` | Small button in the header. Adds a Whisk Expander directly to the right, or removes the attached one and its cables — one undoable action either way. Without the paid plugin installed there is nothing to add and the button does nothing. |

### Per-layer knobs

Each layer has the same four knobs. `SHIFT` gives each of them a second job.

| Knob | Normal meaning | With `SHIFT` latched |
| --- | --- | --- |
| `PACE` | Clock divider/multiplier for this layer: `÷8 ÷6 ÷4 ÷3 ÷2 ÷1.5 ×1 ×1.5 ×2 ×3 ×4 ×6 ×8`, centre `×1`. | `PERS` — persona: Root Only, Triadic, Balanced, Colourful, Free. How adventurous the note choice is. |
| `DENS` | How much of the phrase you hear. Turning it down thins the phrase to its most essential notes and turning it up puts them back — live, from the next note, with no `GEN` needed. Default 50%. | `LEN` — phrase length, 1 to 32 steps. |
| `OCT` | Centre octave, `−3` to `+3`. | `RNG` — how wide the next generated phrase roams: half an octave at minimum, about 1¼ at centre, two octaves at maximum. |
| `DRIFT` | How **often** the melody evolves while it plays. At zero it is frozen where it stands. Default 0. | `SHP` — how tightly the second half of a phrase answers the first. |

### Per-layer buttons and lights

| Control | What it does |
| --- | --- |
| `GEN` | Generates a new melody for that layer. Hold `SHIFT` and press `GEN` to step *back* through that layer's own melody history instead — press repeatedly to keep going back. |
| `MODE` | Flip switch: left `ANCH` for **Anchored**, right `FREE` for **Free**. Anchored stays near home; Free travels further and can take rare bold excursions. Switching mode never rewrites what you are hearing — the current journey finishes, and the new mode governs what happens next. |
| `PULSE` | Lights green while that layer's gate is high, and amber instead when the note you are hearing has evolved away from the phrase's home version. |

### Inputs

| Jack | What it does |
| --- | --- |
| `CLK` | Clock. Every rising edge advances the sequence; each layer's `PACE` divides or multiplies it. |
| `RST` | Reset. Returns both layers to the start of their phrase and restarts both `PACE` clocks. This is the only control that takes effect immediately rather than at the next note. |
| `GEN` | Trigger input. Same as pressing a `GEN` button. Which layer it reaches is set by **Gen trigger targets** in the right-click menu — Layer 1, Layer 2, or Both (the default). |
| `DRIFT` | CV added to the `DRIFT` knob amount. Which layer it reaches is set by **Drift CV targets** in the right-click menu — Layer 1, Layer 2, or Both (the default). |

### Outputs

| Jack | What it does |
| --- | --- |
| `CV 1`, `CV 2` | 1 V/octave pitch of that layer's current note. |
| `GATE 1`, `GATE 2` | 0 V or 10 V. High for that layer's sounding note; how much of the step it stays high is that layer's **Gate length** setting below. |

### Right-click menu

| Item | What it does |
| --- | --- |
| **Layer 1 ▸ Gate length**, **Layer 2 ▸ Gate length** | Slider, 0% to 100%, per layer, default 50%. At 0% each note is the shortest trigger a downstream module can still see. At 100% a note holds for its whole step, so consecutive sounding notes join into one continuous gate. In between, the gate is that fraction of the step. Notes the phrase wrote as ties hold through as written, whatever this is set to. |
| **Layer 1 ▸ Melody reuse**, **Layer 2 ▸ Melody reuse** | Slider, 0% to 100%, per layer, default 75%. How much of the current melody the next `GEN` keeps. At 100% the next generation is the melody you already have; below it the new phrase is recognizably related but meaningfully changed; at 0% it starts from nothing. |
| **Gen trigger targets** | Which layer the `GEN` input drives: Layer 1, Layer 2, or Both. |
| **Drift CV targets** | Which layer the `DRIFT` input drives: Layer 1, Layer 2, or Both. |
| **Scale sync** | Auto, Master or Off — see [Scale sync](#scale-sync). |
| **Add Whisk Expander** / **Remove Whisk Expander** | The same action as the panel's `+ EXPANDER` button. |

### What DRIFT actually does

`DRIFT` sets how **often** a melody evolves, not how much it changes. Turn it up
and changes come thick and fast; turn it down and they are occasional. The size
of each change is a separate roll, so a slow `DRIFT` and a fast `DRIFT` explore
the same kinds of ideas at different rates.

Most changes are small — one cell of the phrase gets reworked. Sometimes a
medium change reshapes a stretch inside one half of the phrase and holds that
new shape for a repetition or two. In **Free** mode only, rarely, a layer takes
a **wild excursion**: a bolder transformation that lives for a few repetitions
before coming back. **Anchored** stays with small and occasional medium changes.

Whatever it does, it keeps hold of the tune. Every ordinary change has to leave
at least two recognizable landmarks of the original phrase intact — its opening
gesture, its cadence, its signature holds, or the relationship between its two
halves. Very sparse phrases of one to three notes are protected exactly and
never go wild, and an empty phrase does not evolve at all.

Journeys end by coming home. Most returns are transformed — unmistakably the
original phrase, carrying one meaningful thing the journey found along the way.
Occasionally the return is exact, and that is deliberate: it is the strong
punctuation. Either way the arrival is heard intact for at least one full
playthrough before anything is allowed to touch it.

Your hands always win. `DRIFT` at zero pauses evolution where it stands and
nothing is lost — raise it and the journey picks up where it was. A completed
`SHIFT`+`GEN` undo travels back to that layer's previous melody. `GEN` and a
completed undo each set a new home for the automatic returns to aim at. `RST` is
the only immediate jump.

### When a change is heard

**No knob or CV, on Whisk or on the Expander, is ever heard mid-note.** The
sounding note keeps its pitch and its full intended length, and the change lands
at the next note onset. Shortening `LEN` mid-phrase lets the current note
finish, so a shorter phrase may wrap early. Clock, reset and generate are
transport and stay instant.

Saving and reloading a patch keeps what you are hearing and what home is.

---

## Whisk Expander

*Paid plugin `Bakehouse Plus`, US $5 · 20 HP · Rack only · Expander, Sequencer*

The Whisk Expander mounts directly to a Whisk's **right** and turns it into an
eight-scene launcher: save complete Layer 1 / Layer 2 moments, recall them
cleanly, and select them from one CV input. Everything is on the face — no
pages, menus, long presses or assignment modes. Together the pair is 32 HP.

The Expander makes no sound of its own. It is a panel of knobs, jacks and lights
that the Whisk beside it reads and writes, after checking that the module on its
right really is a Whisk Expander. Anything else to Whisk's right — another
module, or a placeholder for a plugin you have not bought — is simply not an
Expander, and Whisk plays exactly as it does alone. Move the Expander away
mid-patch and Whisk returns to itself at once, with no leftover pitch shift and
no trigger jack stuck high.

It is not available on MetaModule.

### Scene launcher

| Control | What it does |
| --- | --- |
| `SAVE` | Arms one capture. Press it again to cancel; otherwise the next `A`–`H` press writes that slot and disarms. A capture takes both layers at once — the phrases they are sounding plus each layer's `PACE`, `DENS`, `OCT`, `DRIFT`, `PERS`, `LEN`, `RNG` and `SHP` — and never interrupts the sounding note. |
| `A` `B` `C` `D` `E` `F` `G` `H` | Eight scene slots. With `SAVE` armed, a press saves into that slot. Otherwise a press **cues** that scene; pressing the scene already playing re-launches it. Each button is lit: dark for an empty slot, a dim glow for one holding a scene, full brightness for the scene you are hearing, a slow pulse for one cued and waiting, and a berry pulse across all eight while `SAVE` is armed. |
| `SCENE` | Scene selector CV. 0–10 V across eight equal bands, `A` at the bottom to `H` at the top, clamping outside that range. Empty slots do nothing and a steady voltage does not retrigger. With nothing patched it selects nothing. |

### Launch row

Read left to right: *when* the scene arrives, *how long* it takes, *what* it
brings back.

| Control | What it does |
| --- | --- |
| `PHRASE` / `NOTE` | **`PHRASE`** (left, default) waits for the next Layer 1 phrase boundary, then both layers start together at their openings. **`NOTE`** (right) lets the current Layer 1 note finish, plays one more as a lead-in, then hands over at the Layer 1 onset after that — each layer entering at the onset nearest its own equivalent position in its saved phrase, so the handoff lands mid-phrase rather than restarting. |
| `FLOW` | At zero (default) the scene cuts in instantly. Turned up it dissolves instead, taking up to about three playthroughs, with the incoming scene's most characteristic notes crossing over first. Cue another scene during a changeover and it re-aims over a fresh changeover of the same length. |
| `ALL` / `TUNE` | **`ALL`** (left, default) recalls everything — the saved melodies **and** all eight saved controls per layer, so the moment returns exactly as you left it. **`TUNE`** (right) recalls only the tunes and leaves every live control precisely where your hands have it: a tune saved shorter than the current `LEN` loops round to fill the phrase, a longer one keeps its opening and its final note and sheds interior notes to fit, and its pitches bend into the live `RNG` and `PERS`. |

### Scale shift

| Control | What it does |
| --- | --- |
| `LAYER 1` knob, `LAYER 2` knob | Moves that layer by whole scale steps, up to exactly one octave of the scale in play either way. Live and non-destructive: saved scenes are untouched, and back at centre with no CV that layer's pitch is exactly as saved. |
| `LAYER 1 CV`, `LAYER 2 CV` | 1 V per scale step, added to that layer's knob before the one-octave limit. Unpatched adds nothing. |

The two layers are independent, so either can move alone.

### Patch bay

One row, inputs then outputs.

| Jack | What it does |
| --- | --- |
| `GEN LAYER 1`, `GEN LAYER 2` | Generates a new phrase for that layer alone on each rising edge, exactly as that layer's own `GEN` button does. A held gate fires once. Neither jack saves or recalls a scene. |
| `FLOW CV` | Only ever lengthens a changeover. 0–10 V adds up to the full extra length on top of the `FLOW` knob and stops at the same maximum; negative voltage adds nothing, and unpatching it puts the knob back in sole charge. |
| `END LAYER 1`, `END LAYER 2` | Fires the moment that layer finishes a playthrough and starts the next — one per phrase, whatever its length. A held note is not a boundary, and reset fires nothing. |
| `ARRIVE` | Fires once when a launched scene has fully taken over: at the handoff with `FLOW` at zero, at the end of the changeover above it, and — if you re-aim a running changeover — only for the scene that actually lands. |

Every output here is a 10 V trigger at least 1 ms long; a new event while one is
still high restarts it in full.

---

## Scale sync

Several Whisks in one patch share their root and scale automatically: the first
one placed leads and the others follow, so a rack of them stays in one key
without a single cable. Use **Scale sync** in Whisk's right-click menu to
override — **Auto** (the default), **Master** to force this one to lead, or
**Off** to leave it out of it.

---

## Support

Questions, bug reports and feature requests:
**bennydelaneybrownlow@gmail.com**

Changelog: [CHANGELOG.md](CHANGELOG.md) · Licence: [LICENSE.md](LICENSE.md)
