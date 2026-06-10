# CricketStudio Knowledge Graph — Sample

A **sample** of the CricketStudio cricket knowledge graph: the **Royal Challengers Bengaluru** squad
and their batter-vs-bowler matchup relationships, drawn from IPL 2026 plus
IPL-career head-to-head data.

Every entity links back to its canonical page on https://players.cricketstudio.ai via `canonical_url`.

## Files
| File | Rows | What |
|---|---|---|
| `nodes.json` / `nodes.csv` | 141 | entities — `id` (slug), `type`, `name`, `canonical_url` |
| `edges.json` / `edges.csv` | 777 | typed relationships — `plays_for`, `faced`, `dismissed_by` (matchup counts) |
| `schema.json` | — | node types + edge predicates (the vocabulary) |

## Edge semantics
- `plays_for`  — player → franchise
- `faced`        — batter → bowler, with `{deliveries, runs}` (IPL career)
- `dismissed_by` — batter → bowler, with `{dismissals}`

## Scope & the full graph
This is a **single-franchise sample** for evaluation. The complete graph — all ten
franchises, venues, matches, multi-league coverage, and the full matchup edge set —
is available through the CricketStudio API. Contact **hello@cricketstudio.ai**.

## Provenance
Every number derives from ball-by-ball data and is auditable on the linked page.
See https://players.cricketstudio.ai/about for methodology.

## License
**CC BY 4.0** — attribute "CricketStudio (https://players.cricketstudio.ai)".
