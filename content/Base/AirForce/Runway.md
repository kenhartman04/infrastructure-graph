---
type: base-component
functional_area: flight-ops
priority: mission-critical
has_backup_power: true
---

# Runway

Primary launch and recovery surface. Mission-critical — no runway, no sortie generation.

## Relationships

- Fed by [[Air Force Base]] power (lighting and electronics)
- Backed up by [[Backup Generation]] (lights, NAVAIDs, ILS)
- Supported by [[Control Tower]]
- Operationally linked to [[Taxiways]], [[Aprons]]
- Part of [[Air Force Base]]

## Subsystems Requiring Power

- Runway edge/threshold/touchdown zone lighting — Backed up by generator + UPS
- Approach lighting system (ALS) — Backed up by generator
- ILS (localizer, glide slope) — Backed up by generator + UPS
- PAPI/VASI — Backed up by generator
- Runway surface condition sensors
- Arresting gear electronics (if equipped)

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Interdicts — FOD, standing water, lighting damage | Critical |
| [[Flood]] | Interdicts — surface inundation | Critical |
| [[Ice Storm]] | Interdicts — ice accumulation, de-icing required | High |
| [[Earthquake]] | Disrupts — surface cracking, NAVAID misalignment | High |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Hacking]] | ILS/NAVAID system compromise | Compromises — false approach guidance |
| [[Foreign State]] | Lighting control system malware | Interdicts — runway lighting disabled during operations |

## Notes

- Backup power transfer time is critical — UPS bridges the gap for NAVAIDs
- Power loss to runway lighting at night = immediate mission stop
- De-icing chemical stockpile is a logistics dependency separate from power
