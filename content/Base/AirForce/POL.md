---
type: base-component
functional_area: sustainment
priority: mission-critical
has_backup_power: false
---

# POL

Petroleum, Oils, and Lubricants — fuel storage, distribution, and dispensing for aircraft, vehicles, and backup generators.

## Relationships

- [fuels:: [[Backup Generation]]] (diesel)
- Fuels aircraft operations
- Fed by [[Air Force Base]] power (fuel pumps)
- Resupplied by the off-base fuel chain (pipeline, truck, rail)
- Part of [[Air Force Base]]

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Disrupts — supply chain interruption, tank damage | High |
| [[Flood]] | Interdicts — tank farm inundation, environmental contamination | Critical |
| [[Earthquake]] | Disrupts — pipeline rupture, tank foundation failure | High |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Physical Attack]] | Sabotage of fuel storage | Interdicts — loss of fuel reserves |
| [[Hacking]] | Fuel management system compromise | Compromises — false inventory readings |

## Notes

- POL is the critical link between grid failure and mission sustainability: grid goes down → base goes to backup generators → generators burn fuel → POL reserves deplete → mission stops
- Fuel resupply depends on off-base transportation infrastructure, which faces the same natural disaster threats
- Typical base has 3–7 days of generator fuel without resupply (varies by installation and load)
