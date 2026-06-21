# CricketStudio Knowledge Graph

A **public sample** of the CricketStudio cricket knowledge graph: all **10 IPL
franchises** and their players, with batter-vs-bowler matchup relationships drawn from
IPL 2026 plus IPL-career head-to-head data.

Every entity links back to its canonical data page on https://players.cricketstudio.ai via `canonical_url`.

## What's new (v2, June 2026)

- **All 10 franchises** — previously a single-team teaser (RCB only). Now covers the full
  IPL 2026 squad set: Chennai Super Kings, Delhi Capitals, Gujarat Titans, Kolkata Knight Riders, Lucknow Super Giants, Mumbai Indians, Punjab Kings, Rajasthan Royals, Royal Challengers Bengaluru, Sunrisers Hyderabad.
- **Player attributes** — `role`, `battingHandedness`, `bowlingStyle`, `nationality` added
  to every player node where available (from CricketStudio's Wave 1+2 player-type backfill).
- **League presence** — `leagues` array on each player node lists which leagues have
  ball-by-ball coverage (e.g. `["ipl"]`, `["ipl", "mlc"]`).

## Files

| File | Rows | What |
|---|---|---|
| `nodes.json` / `nodes.csv` | 256 | entities — players + franchises |
| `edges.json` / `edges.csv` | 6861 | typed relationships |
| `schema.json` | — | node types + edge predicates + property vocabulary |

## Node schema

### Player (246 nodes)

| Field | Always present | Description |
|---|---|---|
| `id` | ✓ | Canonical slug (unique, stable) |
| `type` | ✓ | Always `"player"` |
| `name` | ✓ | Full display name |
| `canonical_url` | ✓ | Data page on https://players.cricketstudio.ai |
| `role` | Where known | batter / bowler / all-rounder / wk-batter |
| `battingHandedness` | Where known | `left` or `right` |
| `bowlingStyle` | Where known | e.g. `"right arm fast medium"`, `"slow left arm orthodox"` |
| `nationality` | Where known | Country of nationality |
| `leagues` | Where known | Leagues with CricketStudio ball-by-ball coverage |

### Franchise (10 nodes)

| Field | Always present | Description |
|---|---|---|
| `id` | ✓ | Team code slug (e.g. `rcb`, `mi`) |
| `type` | ✓ | Always `"franchise"` |
| `name` | ✓ | Full franchise name |
| `canonical_url` | ✓ | Team page on https://players.cricketstudio.ai |

## Edge semantics

| Predicate | Direction | Edge props |
|---|---|---|
| `plays_for` | player → franchise | — |
| `faced` | batter → bowler | `{deliveries, runs}` (IPL career) |
| `dismissed_by` | batter → bowler | `{dismissals}` |

## Example queries

**Find all left-handed batters:**
```js
nodes.filter(n => n.battingHandedness === 'left' && n.type === 'player')
```

**Find bowlers who dismissed Virat Kohli ≥3 times:**
```js
edges
  .filter(e => e.predicate === 'dismissed_by' && e.src === 'virat-kohli' && e.props?.dismissals >= 3)
  .map(e => e.dst)
```

**Find players with both IPL and MLC coverage:**
```js
nodes.filter(n => n.leagues?.includes('ipl') && n.leagues?.includes('mlc'))
```

## Scope & the full graph

This is a **public sample** for evaluation and research. The complete graph — all-time
career edges, multi-league matchup data, venues, matches, and the full relationship
set — is available through the CricketStudio API. Contact **hello@cricketstudio.ai**.

## Provenance

Every number derives from ball-by-ball data and is auditable on the linked canonical
page. See https://players.cricketstudio.ai/about for methodology.

## License

**CC BY 4.0** — attribute "CricketStudio (https://players.cricketstudio.ai)".
