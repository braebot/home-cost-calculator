# Home Cost Calculator — Decisions & Rationale

Records the *why* behind design choices that the code itself doesn't explain.
For *what* the code does, read `index.html` (the constants at the top of the
`<script>` are the tuning surface).

## Firm constraints
- **Single-page app.** Ships as one self-contained `index.html` — no build step,
  no external dependencies. Every change must preserve this.

## Key decisions
- **One shared flow, only the sizing step is branched.** The user picks a size
  bucket *or* enters rooms individually. Everything before and after that step,
  and the results, are identical for both branches — so the manual branch only
  needs to produce numbers that feed the same calculation.
- **Manual size is measured relative to a reference medium home**, not as an
  absolute. Reason: the rest of the model is a base cost plus deltas where
  "medium = 0," so the manual branch has to return a delta to plug in cleanly.
- **Contractor fee applies to hard costs only** (site, structure, systems,
  finishes — not land, soft costs, or financing), because a GC fee isn't charged
  on land or financing. Rate is a fixed 18% (midpoint of a typical 15–25%
  custom-home range), deliberately not user-editable this iteration.
- **Location multiplier scales hard construction costs only** (site, structure,
  systems, finishes) — not land, soft costs, or financing. This matches the
  contractor-fee basis: a regional construction index shouldn't touch land
  (already priced by the Land Cost question) or financing. The total stays
  anchored to the base estimate, so location at 1.00× equals the no-location
  baseline. Same two-branch pattern as sizing: a preselected "Gunnison County =
  1.00×" default, or a custom region/multiplier with add-on factors. Add-on
  factors (freight/access, elevation) are kept **distinct from the Site
  Difficulty question** to avoid double-counting.

## Open / unresolved
- Per-room $/sq-ft rates and the base cost are **placeholder assumptions**
  awaiting the real spreadsheet numbers.
- **Possible double-count:** the contractor fee sits on top of the base all-in
  cost. If that base already includes builder margin, this overstates it —
  needs confirmation of what the base number represents.

## Deferred (intentionally not built yet)
- _(none currently)_
