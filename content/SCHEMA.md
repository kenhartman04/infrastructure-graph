---
type: meta
---

# Infrastructure Resilience Knowledge Graph — Schema

## The One Rule

Every typed link points **the way failure travels**: from the thing that fails to the thing it takes down. Because of that, the order of an effect is not stored anywhere. It is computed: the number of links between a threat and whatever it reaches.

## Node Types

| `type` value | Description | Folder |
|---|---|---|
| `grid-component` | Electrical infrastructure node | `Grid/` |
| `threat` | Natural disaster or cyber/physical threat | `Threats/` |
| `base` | Military installation (top-level) | `Base/` |
| `base-component` | Functional element within a base | `Base/<Branch>/` |
| `meta` | Schema and reference notes | root |

## Typed Links (Dataview inline fields)

Written in a note's body as `[field:: [[Target]]]`, for example `- [feeds:: [[Substation]]]`.

### Threat effects (threat → target)

| Field | Meaning |
|---|---|
| `interdicts` | Cuts the target off entirely |
| `disrupts` | Degrades the target; it keeps partial function |
| `compromises` | Cyber: the target keeps running but can't be trusted |

### How failure spreads (provider → dependent)

| Field | Meaning | Example |
|---|---|---|
| `feeds` | Supplies grid power | `Substation` → `Feeders` |
| `fuels` | Supplies fuel | `POL` → `Backup Generation` |
| `backs` | Provides backup power | `Backup Generation` → `Runway` |
| `supports` | One function depends on another | `Data Center` → `Operations` |

Untyped lines such as "Fed by [[Feeders]]" are readable back-references. They draw a line in graph view but are not followed when computing a cascade.

## Cascade by Order

Every threat note ends with a `dataviewjs` block that walks the typed links outward from that threat and prints a table: order, affected node, the node it came through, and the link type.

- Order 1 = what the threat hits directly; order 2 = what those failures take down; and so on, up to 6.
- Each node is listed once, at the **shortest** path from the threat.
- It shows **exposure**: everything downstream that could be affected. It does not say whether backup power holds or how likely each step is. A compromise of the power plant appears to propagate down the grid because an attacker with that access could act on it; whether they do is a scenario question.

Setup: install the Dataview community plugin and turn on **Enable JavaScript Queries** in its settings. The table renders in Reading view and Live Preview.

## Frontmatter Fields

### Grid Components
- `tier`: generation | transmission | distribution
- `voltage_class`: high | medium | low
- `backup_power`: true | false | partial

### Threats
- `domain`: natural | cyber
- `hazard_class` (natural): wind-water | winter | water | seismic | thermal | fire
- `vector` (cyber): technical | human | physical | structural | state-sponsored
- `abbreviation`: single-letter code from notebook notation (P, Ph, L, H, S, F)

### Base Components
- `functional_area`: flight-ops | security | mission-support | sustainment | power
- `priority`: mission-critical | high | medium
- `has_backup_power`: true | false | partial | N/A

## Extending This Graph

- **New threat:** copy a note from `Threats/`, list what it hits as `interdicts`, `disrupts` or `compromises` fields, and keep the Cascade by Order block.
- **New grid or base node:** add the typed links that leave it (what it feeds, fuels, backs or supports). Don't add a typed link pointing upstream; write that as a plain "Fed by" line.
- **New relationship type:** add the field name to the `kinds` list in the cascade block of every threat note.
- **Specific installation** (e.g., Joint Base San Antonio): create a folder under `Base/`, link its feeders and functions with the same fields, and every threat's cascade picks it up automatically.
