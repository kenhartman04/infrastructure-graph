---
type: base-component
functional_area: mission-support
priority: mission-critical
has_backup_power: true
---

# Data Center

Houses servers, networking, and communications infrastructure supporting base operations, C2, and intelligence systems.

## Relationships

- [supports:: [[Operations]]] (C2 systems, network)
- [supports:: [[Intel]]] (classified network infrastructure)
- [supports:: [[SecFo]]] (dispatch, alarm monitoring)
- Fed by [[Air Force Base]] power
- Backed up by [[Backup Generation]] and UPS (battery bridge during transfer)
- Part of [[Air Force Base]]

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Disrupts — utility power loss, potential structural damage | High |
| [[Flood]] | Interdicts — equipment submersion if below grade | Critical |
| [[Earthquake]] | Disrupts — rack displacement, cable damage, cooling failure | High |
| [[Extreme Heat]] | Disrupts — HVAC overload, thermal throttling | Medium |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Hacking]] | Network intrusion, ransomware | Compromises — data exfiltration, system encryption |
| [[Phishing]] | Admin credential theft | Compromises — privileged access to network infrastructure |
| [[Legacy Systems]] | End-of-life OS/firmware in SCIF enclaves | Compromises — unpatched vulnerabilities |
| [[Foreign State]] | Supply chain implant, persistent access | Compromises — long-dwell espionage |

## Notes

- Cooling is as critical as power — HVAC failure = thermal shutdown within minutes
- Classified and unclassified networks may share physical infrastructure but not logical connectivity
- Generator fuel burn rate determines standalone operations window → links to [[POL]]
