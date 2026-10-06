# Highland Gold — Recorder

A single-page offline app for recording pan results and rock samples in the field.
No network calls, no CDN, no accounts, no tracking. Everything stays on the phone
until you export it.

## Two tabs

### Pins
Pan results and site observations, as before. Quick pin from GPS, or enter a grid
reference from the paper map. Exports GeoJSON.

### Samples — new
Field capture for rocks. Deliberately short: this gets filled in standing in a river
with cold hands, so it only asks for what cannot be recorded later.

| Field | Why it is here |
|---|---|
| Sample ID | Auto `TYN-001`, `TYN-002`… Tap the prefix line to change area |
| Grid reference | From GPS with accuracy, or entered from the map |
| Photos | **In situ first, before you touch it.** Then with scale, then wet |
| Context | Where it was lying. The field that decides whether the rest means anything |
| Why you picked it up | One line. Future-you will not remember |
| Taken / left in place | A boulder you left is still a record |

Dimensions, mass, SG, hardness, streak, magnet, acid, microscope and identification
are **bench work**. They go in the vault, not here.

## Photos

Stored shrunk — 1600 px long edge, JPEG — in the phone's own database (IndexedDB).
Keep the full-size originals in your camera roll; they are the archive, this is the record.

Shrinking matters: a few hundred full-resolution photos will fill the storage quota and
exports will fail. At 1600 px each shot is roughly 300–500 KB.

## Export

**Export samples (.zip)** produces one file:

```
highland-gold-samples-YYYY-MM-DD.zip
├── samples.json       every field, for the vault script
├── samples.geojson    points for QGIS
└── photos/
    └── TYN-001_01_in_situ.jpg
```

Photo filenames carry the sample ID and the shot kind, so nothing can be orphaned if
the zip is ever unpacked loose.

The ZIP is written in-browser with no library — stored, uncompressed, because JPEGs are
already compressed. Opens in anything.

Pins still export separately as GeoJSON.

## Offline

There are no network requests in this app at all. GPS, camera, storage and export are
all local. The service worker is network-first so updates reach the installed app when
there is signal, and falls back to cache when there is not — so it works in a glen with
no bars.

GPS needs no signal. It is satellite positioning and works anywhere with sky view.

## Installing

Open the URL in Chrome, then menu → Add to Home screen. It runs full-screen from then on.

Location permission must be set to **Precise**, not Approximate. Approximate returns a
plausible-looking grid reference that is wrong by kilometres — check the accuracy figure
reads single or low double digits before trusting a fix.

## Data safety

Everything lives in the phone's local storage. Clearing site data for this URL deletes
all of it, pins and photos both. **Export after every trip.**
