# PlanBridge

**Import HYROX training plans into Intervals.icu**

Live app → **[planbridgeapp.github.io/planbridge](https://planbridgeapp.github.io/planbridge)**

---

## What it does

PlanBridge reads a structured backup file and uploads each workout as a calendar event in [Intervals.icu](https://intervals.icu) — with full support for:

- **Structured running workouts** — interval steps, paces, and zones auto-generated from your 5k pace, visible as charts and synced to Garmin
- **Strength & conditioning days** — section headers and exercise descriptions preserved cleanly
- **Upsert by date** — re-uploading the same file updates existing events instead of creating duplicates
- **One-click undo** — remove all events from the last upload instantly

---

## How to use

### Step 1 — Open PlanBridge

Go to **[planbridgeapp.github.io/planbridge](https://planbridgeapp.github.io/planbridge)**.

### Step 2 — Enter your credentials

- **API Key** — find it at intervals.icu → Settings → API
- **5k Run Pace** — enter as `mm:ss` per km (e.g. `4:30`). Used to convert running workouts into structured Intervals.icu format with auto-calculated training load. Leave blank to upload running sessions as plain text instead.

Credentials are stored locally in your browser and never leave your machine.

### Step 3 — Drop your backup file

Drag the `.txt` backup file onto the drop zone, or click to select it. PlanBridge parses the file and shows a preview of all workouts with their dates, types, and descriptions.

### Step 4 — Upload

Click **Upload to Intervals.icu**. A single bulk request sends all workouts. Done.

---

## Sharing the plan with training partners

Each athlete opens PlanBridge in their own browser and enters their own API Key and 5k pace. Since paces are individual, each athlete gets running workouts calibrated to their own fitness level.

To share the plan:
1. Upload to your Intervals.icu account
2. Generate a share link from the Intervals.icu calendar
3. Your training partners open the link and import the plan into their own calendar with one click

---

## File format

PlanBridge expects:

- Block separator: `─` × 50 (Unicode U+2500) between days
- Header separator: `─` × 30 between the title line and content
- Title line: `HYROX DOUBLES RACE PLAN Mon, April 27 Week 9, Day 1`
- Content: section headers natively from the FITR DOM (`## WARM UP / ACTIVATION`, `## STRENGTH A)`, etc.)

---

## Running workout conversion

When a 5k pace is provided, running workouts are converted from relative notation into Intervals.icu's structured workout format.

| relative notation | Example (4:30/km base) | Intervals.icu |
|---|---|---|
| `@5k+90"` | Easy / Z1 | `6:00/km Pace` |
| `@5k+25"` | Race pace | `4:55/km Pace` |
| `@5k` | Threshold | `4:30/km Pace` |
| `@5k-20"` | VO2max | `4:10/km Pace` |
| `@5k-45/60"` | Anaerobic range | `3:45/km-3:30/km Pace` |
| `@easy` | Zone 1 | `Z1 Pace` |
| `200m ACE*` | Progressive strides | `200mtr Z1 Pace ACE progressive strides` |

Strength and conditioning sections are always uploaded as plain text — no conversion attempted.

---

## License

MIT

