---
type: base-component
functional_area: flight-ops
priority: mission-critical
has_backup_power: true
---

# Control Tower

Air traffic control for the installation — manages launch, recovery, and airspace deconfliction.

## Relationships

- [supports:: [[Runway]]] (air traffic control)
- Fed by [[Air Force Base]] power
- Backed up by [[Backup Generation]] and UPS
- Part of [[Air Force Base]]

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Disrupts — wind damage to antenna/radome, window breach | High |
| [[Earthquake]] | Disrupts — structural cracking, equipment displacement | High |
| [[Tornado]] | Interdicts — tower structural failure | Critical |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Hacking]] | ATC system exploitation | Compromises — false traffic data, comm disruption |
| [[Legacy Systems]] | Aging ATC software with long certification cycles | Compromises — known vulnerabilities unpatched |
| [[Foreign State]] | GPS spoofing/jamming, comm intercept | Compromises — degraded situational awareness |
