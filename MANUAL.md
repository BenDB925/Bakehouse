# Bakehouse user manual

Whisk and the Whisk Expander for VCV Rack 2.

- **Whisk** is free. It is a complete, self-contained generative sequencer.
- **Whisk Expander** is a separate paid plugin (US $5) that adds an eight-scene
  launcher, per-layer pitch shifting and a small patch bay to Whisk.

The Expander is optional. Whisk generates, evolves and plays both layers on its
own. Everything in the Whisk section works without the Expander or its plugin.

**Contents:** [Whisk](#whisk) · [Whisk Expander](#whisk-expander) ·
[Scale sync](#scale-sync) · [Support](#support)

---

## Whisk

*Free plugin `Bakehouse` · 12 HP · Sequencer, Random, Dual*

Whisk plays two independent melodies, **Layer 1** and **Layer 2**, in one shared
scale. Each layer starts with a generated phrase and gradually changes as it
plays. Most changes are subtle, some are bolder, and the melody eventually
finds its way home. The layers listen to each other too, which helps them sound
like a duet rather than two unrelated lines.

Patch a clock in, take pitch and gate out of each layer into a voice, press
`GEN`, and turn `DRIFT` up when you want the tune to start travelling.

### Global controls

| Control | What it does |
| --- | --- |
| `ROOT` | Tonic of the scale, `C` to `B`. |
| `SCALE` | Major, Minor, Dorian, Mixolydian, Pent. Major, Pent. Minor, Blues, Chromatic. |
| `SHIFT` | Latch. While it is lit, the four per-layer knobs of **both** layers change meaning (see below). Nothing moves until you turn a knob. |
| `EXPANDER` | Small button in the header. When Bakehouse Treats is installed and licensed it reads `+ EXPANDER` / `- EXPANDER`, adding the Expander directly to Whisk's right or removing it and its cables; either action can be undone. Otherwise it stays dimmed with a lock, and its tooltip points to Whisk's right-click menu. |

### Per-layer knobs

Each layer has the same four knobs. `SHIFT` gives each of them a second job.

| Knob | Normal meaning | With `SHIFT` latched |
| --- | --- | --- |
| `PACE` | Clock divider/multiplier for this layer: `÷8 ÷6 ÷4 ÷3 ÷2 ÷1.5 ×1 ×1.5 ×2 ×3 ×4 ×6 ×8`, centre `×1`. Default `×1` on Layer 1 and `÷2` on Layer 2. | `PERS` sets the persona: Root Only, Triadic, Balanced, Colourful or Free. It controls how adventurous the note choices can be. Default Balanced on Layer 1 and Triadic on Layer 2. |
| `DENS` | How much of the phrase you hear. Turn it down to keep only the most important notes, or turn it up to bring notes back. It responds from the next note, with no `GEN` needed. Default 70%. | `LEN` sets the phrase length from 1 to 32 steps. Default 16 on Layer 1 and 8 on Layer 2. Turning it up keeps every note of the tune and writes new steps around it; turning it down hides the end without losing it. |
| `OCT` | Centre octave, `−3` to `+3`. Default `0` on Layer 1 and `−1` on Layer 2, so a new Whisk starts as a lead over a slower, lower counterline. | `RNG` sets how far the next generated phrase can roam: half an octave at minimum, about 1¼ at centre, and two octaves at maximum. Default half of the way up. |
| `DRIFT` | How **often** the melody evolves while it plays. At zero it stays where it is. Default 50% on Layer 1 and 25% on Layer 2. | `SHP` sets how closely the second half of a phrase answers the first. Default 70%. |

#### What the personalities mean

`PERS` decides which notes in the selected scale can be the melody's main
destinations. Whisk ranks the available notes from settled to colourful: the
tonic first, then the closest notes the selected scale has to a fifth, major
third, major seventh, major second, major sixth and fourth. Each personality
opens more of that list:

| Personality | Main note pool | In a seven-note major scale |
| --- | --- | --- |
| **Root Only** | Tonic only. | Root. |
| **Triadic** | The first 30% of the scale's notes, rounded to the nearest whole note. | Root and fifth. |
| **Balanced** | The first 55%: enough stable notes for melodic movement without using most of the scale's tension notes as destinations. | Root, fifth, third and seventh. |
| **Colourful** | The first 80%: most of the scale, including brighter and less settled destinations. | Root, fifth, third, seventh, second and sixth. |
| **Free** | Every note in the scale. | All seven notes. |

For reference, the five personalities admit `1 / 2 / 4 / 6 / 7` main notes in
a seven-note scale, `1 / 2 / 3 / 4 / 5` in a five-note scale, and
`1 / 4 / 7 / 10 / 12` in Chromatic. Balanced, Colourful and Free may also use
other in-scale notes briefly to connect two destinations smoothly; those notes
do not become part of the personality's main pool. About one phrase in four
also aims for a deliberately unsettled final note; for that final note only,
Balanced can draw from the same 80% pool as Colourful.

### Per-layer buttons and lights

| Control | What it does |
| --- | --- |
| `GEN` | Generates a new melody for that layer. Hold `SHIFT` and press `GEN` — the panel prints `UNDO` for this — to step *back* through that layer's melody history. Press it again to keep going back. |
| `MODE` | Flip switch: left `ANCH` for **Anchored**, right `FREE` for **Free**. Anchored stays near home. Free travels further and can take rare, bold excursions. Default Anchored on both layers. Switching mode does not rewrite the current melody. The current journey finishes first, then the new mode takes over. |
| `PULSE` | Lights green while that layer's gate is high, and amber instead when the note you are hearing has evolved away from the phrase's home version. |

### Inputs

| Jack | What it does |
| --- | --- |
| `CLK` | Clock. Every rising edge advances the sequence; each layer's `PACE` divides or multiplies it. |
| `RST` | Reset. Returns both layers to the start of their phrase and restarts both `PACE` clocks. Along with the clock and `GEN`, it acts at once rather than waiting for the next note the way knob and CV changes do. |
| `GEN` | Trigger input. Same as pressing a `GEN` button. Use **Gen trigger targets** in the right-click menu to send it to Layer 1, Layer 2 or Both (the default). |
| `DRIFT` | CV added to the `DRIFT` knob amount: each `1 V` adds 10 percentage points, so `+5 V` adds 50% and `+10 V` takes a zero knob to maximum. Negative voltage subtracts the same way. The final amount is clamped to 0–100%, so the exact rule is `clamp(knob + volts / 10)`. Use **Drift CV targets** in the right-click menu to send it to Layer 1, Layer 2 or Both (the default). |

### Outputs

| Jack | What it does |
| --- | --- |
| `CV 1`, `CV 2` | 1 V/octave pitch of that layer's current note. |
| `GATE 1`, `GATE 2` | 0 V or 10 V. High for that layer's sounding note; how much of the step it stays high is that layer's **Gate length** setting below. |

### Right-click menu

| Item | What it does |
| --- | --- |
| **Layer 1 ▸ Gate length**, **Layer 2 ▸ Gate length** | Slider, 0% to 100%, per layer, default 50%. The percentage is relative to that note's full slot: one step for an ordinary note and half a step for each hit of a double note. At 0% each hit is the shortest trigger a downstream module can still see. At 100% an ordinary note holds for its whole step, so consecutive sounding notes join into one continuous gate; double hits retain the tiny low edge needed to retrigger. Notes the phrase wrote as ties hold through as written, whatever this is set to. |
| **Layer 1 ▸ Melody reuse**, **Layer 2 ▸ Melody reuse** | Slider, 0% to 100%, per layer, default 25%. How much of the current melody the next `GEN` keeps. Each press keeps its share of the tune playing just before it, so one press gives a close cousin and mashing `GEN` seven or eight times wanders somewhere completely different. At 100% the next generation is the melody you already have; at 0% it starts from nothing. It means the same in every persona. |
| **Gen trigger targets** | Which layer the `GEN` input drives: Layer 1, Layer 2, or Both. |
| **Drift CV targets** | Which layer the `DRIFT` input drives: Layer 1, Layer 2, or Both. |
| **Scale sync** | Auto, Master or Off. See [Scale sync](#scale-sync). |
| **Add Whisk Expander** / **Remove Whisk Expander** | Available when Bakehouse Treats is licensed; the same undoable action as the panel button. |
| **Buy Whisk Expander...** | Shown when the paid Expander is not available. Opens its VCV Library page. While Rack is still checking or downloading a key, a checking message appears instead of asking you to buy. If the plugin is installed but its key is missing, **Whisk Expander license unavailable** appears above it. |
| **Already purchased?** | Owner help: sign into the VCV account used for the purchase, use **Library > Update all** to install or refresh the key, or contact VCV license support. |

### What DRIFT actually does

`DRIFT` controls how **often** a melody evolves, how many changes it makes
before turning back, and how long it rests at home once it returns. Turn it up
for a busier melody that travels further; turn it down for occasional changes
and a quick return. In **Anchored** it also tilts the odds toward bolder
changes.

Most changes are small and rework one part of the phrase. A medium change
reshapes half the phrase for a repetition or two. A rare **wild excursion**
goes further: in **Free** it rewrites half the phrase, and in **Anchored** it
reworks the whole thing while keeping the opening and the ending of the tune
you started with. **Free** wanders further from home before it turns back.

The original tune never disappears completely. Every ordinary change keeps at
least two recognizable parts of the phrase, such as its opening, cadence,
signature holds or the relationship between its two halves. Phrases with one to
three notes are left alone, and an empty phrase does not evolve.

Eventually the melody comes home, and it always arrives exactly on the phrase
it left — but not in one jump. It gives back a little more of home over two or
three playthroughs. Home then plays untouched for a few playthroughs before
anything can change again, and the higher `DRIFT` is, the longer that rest.

Set `DRIFT` to zero to pause the melody where it is. Turn it back up and the
journey continues. A completed `SHIFT`+`GEN` undo returns to that layer's
previous melody. Both `GEN` and a completed undo set a new home for future
returns. `RST` is the only immediate jump.

### When a change is heard

Knob and CV changes on Whisk or the Expander wait for the next note. The current
note keeps its pitch and full length. If you shorten `LEN` during a phrase, the
current note still finishes, so the shorter phrase may wrap early. Clock, reset
and generate remain immediate.

Turning `LEN` up past the end of the tune keeps every note of it exactly where
it is and fills the new steps the way `GEN` would: the tune's hook comes back
in them and the phrase ends properly on its new last step. The new steps are
worked out afresh from the tune for each length, so the same `LEN` always
gives the same phrase however you reached it — notes you only hear in the
added steps may change while you are still turning. Turning `LEN` down into
the tune hides its end; turn it back up and exactly the hidden notes return.
`GEN`, a completed undo or a scene launch gives `LEN` a new tune to grow from.

Saving and reloading a patch keeps what you are hearing and what home is.

---

## Whisk Expander

*Paid plugin `Bakehouse Treats`, US $5 · 20 HP · Rack only · Expander, Sequencer*

The Whisk Expander mounts directly to a Whisk's **right** and turns it into an
eight-scene launcher. You can save and recall complete Layer 1 / Layer 2 moments,
or select them from one CV input. All of its controls are on the panel, with no
pages, menus, long presses or assignment modes. Together the pair is 32 HP.

The Expander makes no sound of its own. Whisk reads its knobs and jacks and
drives its lights and outputs. It also checks that the module on its right is a
Whisk Expander. If it finds another module or a placeholder for a missing
plugin, Whisk carries on as normal. Move the Expander away during a patch and
any pitch shift is removed immediately. Its trigger outputs also return low.

It is not available on MetaModule.

### If it is not licensed

Without a Bakehouse Treats licence the Expander still appears in the module
browser and can be placed, but Rack covers its panel with a lock overlay and
Whisk treats it as if it were not there: its knobs, jacks and buttons do
nothing, and no pitch shift reaches either layer. Clicking the locked panel
opens the Whisk Expander's VCV Library page, and so does **Buy Whisk
Expander...** in the Expander's own right-click menu. Once the key arrives the
panel unlocks by itself, with no need to remove and re-add it.

### Scene launcher

| Control | What it does |
| --- | --- |
| `SAVE` | Arms one capture. Press it again to cancel. Otherwise, the next `A`–`H` press writes that slot and disarms. A capture saves both sounding phrases and each layer's `PACE`, `DENS`, `OCT`, `DRIFT`, `PERS`, `LEN`, `RNG` and `SHP`. It does not interrupt the current note. |
| `A` `B` `C` `D` `E` `F` `G` `H` | Eight scene slots. With `SAVE` armed, a press saves into that slot. Otherwise a press **cues** that scene; pressing the scene already playing re-launches it. Each button is lit: dark for an empty slot, a dim glow for one holding a scene, full brightness for the scene you are hearing, a slow pulse for one cued and waiting, and a berry pulse across all eight while `SAVE` is armed. |
| `SCENE` | Scene selector CV: `A` below `1.25 V`; `B` from `1.25` to below `2.50 V`; `C` from `2.50` to below `3.75 V`; `D` from `3.75` to below `5.00 V`; `E` from `5.00` to below `6.25 V`; `F` from `6.25` to below `7.50 V`; `G` from `7.50` to below `8.75 V`; `H` from `8.75 V` upward. Voltages outside 0–10 V clamp to `A` or `H`. Empty slots do nothing and a steady voltage does not retrigger. With nothing patched it selects nothing. |

### Launch row

Read left to right: *when* the scene arrives, *how long* it takes, *what* it
brings back.

| Control | What it does |
| --- | --- |
| `PHRASE` / `NOTE` | **`PHRASE`** (left, default) waits for the next Layer 1 phrase boundary, then starts both layers from the beginning. **`NOTE`** (right) lets the current Layer 1 note finish and plays one more as a lead-in. It hands over on the following Layer 1 onset. Each layer enters near the same point in its saved phrase, so the new scene joins in mid-phrase rather than starting over. |
| `FLOW` | At maximum (default) the scene dissolves in over about three playthroughs, with the incoming scene's most characteristic notes crossing over first. Turned down it arrives sooner; at zero it cuts in instantly. Cue another scene during a changeover and it re-aims over a fresh changeover of the same length. |
| `ALL` / `TUNE` | **`ALL`** (left, default) recalls the saved melodies and all eight saved controls per layer. **`TUNE`** (right) recalls only the melodies and leaves the live controls where they are. A tune shorter than the current `LEN` repeats to fill the phrase. A longer one keeps its opening and final note while dropping interior notes to fit. Its pitches are adjusted to the live `RNG` and `PERS`. |

### Scale shift

| Control | What it does |
| --- | --- |
| `LAYER 1` knob, `LAYER 2` knob | Moves that layer up or down by whole scale steps, with a limit of one octave in either direction. This does not alter saved scenes. Return the knob to centre with no CV to hear the saved pitch again. |
| `LAYER 1 CV`, `LAYER 2 CV` | `1 V` per scale step: `+1 V` moves up one note of the selected scale and `−1 V` moves down one. Fractional voltages are rounded to the nearest whole volt (`±0.5 V` starts the first step), then added to the knob's whole-step shift. The result is limited to one scale octave up or down. Unpatched adds nothing. |

The two layers are independent, so either can move alone.

### Patch bay

One row, inputs then outputs.

| Jack | What it does |
| --- | --- |
| `GEN LAYER 1`, `GEN LAYER 2` | Generates a new phrase for that layer alone on each rising edge, exactly as that layer's own `GEN` button does. A held gate fires once. Neither jack saves or recalls a scene. |
| `FLOW CV` | Only ever lengthens a changeover. Each `1 V` adds 10% to the `FLOW` knob, with the total clamped at 100%; negative voltage adds nothing. With the knob at zero: `0 V` cuts instantly, above `0` through `3⅓ V` gives one intermediate playthrough, above `3⅓` through `6⅔ V` gives two, and above `6⅔ V` gives three. Unpatching it puts the knob back in sole charge. |
| `END LAYER 1`, `END LAYER 2` | Fires when that layer finishes a playthrough and starts the next. It sends one trigger per phrase, whatever the phrase length. A held note is not a boundary, and reset does not fire it. |
| `ARRIVE` | Fires once when a launched scene has fully taken over. With `FLOW` at zero, it fires at the handoff. With `FLOW` raised, it fires at the end of the changeover. If you choose another scene during a changeover, only the scene that finally arrives sends the trigger. |

Every output here is a 10 V trigger at least 1 ms long; a new event while one is
still high restarts it in full.

---

## Scale sync

Several Whisks in one patch share their root and scale automatically: the first
one placed leads and the others follow, so a rack of them stays in one key
without a single cable. Use **Scale sync** in Whisk's right-click menu to
override this. Choose **Auto** (the default), **Master** to make this Whisk lead,
or **Off** to leave it out of scale sync.

---

## Support

Questions, bug reports and feature requests:
**bennydelaneybrownlow@gmail.com**

Changelog: [CHANGELOG.md](CHANGELOG.md) · Licence: [LICENSE.md](LICENSE.md)
