---
type: grid-component
tier: distribution
backup_power: false
voltage_class: low
---

# Feeders

Distribution lines (4kV–35kV) delivering power from substations to end users — POIs, households, and critical facilities including military bases.

## Relationships

- [feeds:: [[Air Force Base]]] (designated/priority circuits)
- [feeds:: [[POI]]]
- [feeds:: [[Household]]]
- Fed by [[Substation]]

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Interdicts — pole snaps, downed lines | Critical |
| [[Ice Storm]] | Interdicts — conductor breakage from ice loading | Critical |
| [[Tornado]] | Interdicts — localized total destruction | High |
| [[Flood]] | Disrupts — pad-mount transformer submersion | High |
| [[Wildfire]] | Interdicts — pole combustion, PSPS de-energization | High |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Hacking]] | Smart meter / AMI network compromise | Compromises — load data exfiltration, false demand signals |
| [[Physical Attack]] | Pole/transformer sabotage | Interdicts — localized outage |

## Notes

- Last mile — highest outage frequency, lowest restoration priority relative to transmission
- Overhead vs. underground: overhead cheaper but more exposed to wind/ice; underground resilient to wind but vulnerable to flooding
- Military base feeders are typically designated/priority circuits but still depend on upstream grid health
