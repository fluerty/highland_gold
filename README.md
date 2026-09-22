# Highland Gold — Recorder

A single-purpose field data recorder for the rest of this season. **Not** the full app —
no maps, no layers, no model. It does one job: make sure every pan you work this autumn
becomes a usable record for the winter analysis.

## Getting it on the phone (10 minutes, once)

Geolocation needs a secure origin, so opening the file from storage won't work.

1. New GitHub repo, drop these four files in the root, Settings → Pages → deploy from
   `main` / root.
2. Open the Pages URL on the phone in Chrome.
3. Menu → **Add to Home Screen**.

After that it opens full-screen and works with no signal. Data lives on the device.

## Using it

**Quick pin** — one tap. Saves position, grid reference, accuracy, time. Half a second,
wet hands, no thinking. Pins with no detail yet show a red dot in the list.

**Tap any pin** to fill in the rest — tap-select chips and counters, nothing to type
except notes. Do it at the spot if it's easy, or in the van, or that evening. Everything
autosaves as you tap; there's no save button.

**Add pin from grid ref** — the backup when GPS fails. Read the reference off the paper map
by resection, type it in, add the time it was recorded. The app converts it back to lat/long
and the pin behaves like any other. Accuracy is recorded honestly as the precision of the
quoted square: ±500 m for a six-figure ref, ±50 m for eight. Pins entered this way are marked
`from map` in the list and carry `position_source: "manual"` in the export, so they never get
mistaken for satellite fixes in the analysis.

**Export GeoJSON** at the end of each trip. Flat schema, opens straight in QGIS.

## Record the blanks

`pans_worked: 4, flake_count: 0` is a **result**, not a missing record. A model tuned only
on successes can't discriminate — it learns "everywhere is good". Log every spot you work,
including the ones that gave nothing.

And deliberately work one spot per trip that you *don't* rate. That contrast is what makes
the winter regression mean anything.

## Photos

Use the normal camera app, not this. Phone photos carry their own GPS and timestamp, they
get backed up automatically, and they match to pins by time back at the bench. Building
photo capture into a web app is the fiddliest part of the whole project and buys nothing
this season.

Include the **pan lip, a trowel or a coin** in every shot, or you'll get home with a picture
of a crevice and no idea whether it's 3 cm or 30.

Worth taking three shots per spot: the trap itself from above with scale, the trap in
context showing which way the water runs, and the pan if there's colour.

## Fields, and why

| Field | Why it's there |
|---|---|
| `pans_worked` | Denominator. Without it a flake count means nothing |
| `flake_count`, `picker_count` | Yield. Crude but consistent, which is what regression needs |
| `grain_character` | **The highest-value field.** Grain shape is a direction indicator — crystalline means near source, flour means far-travelled. It's how BGS drainage surveys vectored onto targets |
| `trap_type` | Tests whether confluences are really the right proxy |
| `bedrock_type` | `till_only` and `boulders_only` record *no accessible bedrock* — a real and common reason a good-looking spot gives nothing |
| `flow_state` | Gold is emplaced in spates, not at summer flow |
| `crevice_strike_deg` | Direction the structure runs — correlates against vein trend. Dip matters less |
| `pin_type` | `vantage` marks a photo standpoint for repeat photography; `access` marks parking and crossings |

## Limits, honestly

- Data is in browser storage on that phone. **Export after every trip** and keep the file.
  Clearing site data loses everything.
- No map. Deliberate — the map needs tiles, and tiles need a pipeline that isn't built yet.
  Use the paper OS Explorer sheet alongside, as you already do.
- No compass capture. Take strike with a real compass and type the number.
- **Check the accuracy figure before dropping a pin.** A network-derived position can read
  ±2000 m and still produce a plausible-looking grid reference. The header says "fix" only
  below ±20 m. If it's bad: step into the open, give it a minute, and check Chrome's location
  permission is set to precise rather than approximate — it can revert after an update.

## If GPS fails in the field

1. Step into the open, wait a full minute — canopy and steep sides are the usual cause
2. Check Google Maps knows where you are. If it does and this doesn't, it's a permission
   problem, not a satellite one
3. Turn off battery saver, which throttles location
4. Otherwise: paper map, compass, resection, and **Add pin from grid ref**. Waterproof
   notebook and pencil — biro won't write wet. Record the time with every entry; it's what
   reconciles the paper record with your photos afterwards.
