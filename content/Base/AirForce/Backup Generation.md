---
type: base-component
functional_area: power
priority: mission-critical
has_backup_power: N/A
---

# Backup Generation

Diesel generators providing emergency power when commercial utility service ([[Feeders]]) is lost.

## Relationships

- [backs:: [[Runway]]] (lights, NAVAIDs, ILS)
- [backs:: [[Control Tower]]]
- [backs:: [[Data Center]]]
- [backs:: [[Operations]]]
- [backs:: [[Intel]]]
- [backs:: [[Perimeter]]] (priority sensors only)
- Fueled by [[POL]]
- Takes over when [[Feeders]] power is lost

## Natural Disaster Vulnerabilities

- [[Flood]] — Interdicts — generator submersion if ground-level
- [[Extreme Heat]] — Disrupts — derated output, cooling system stress

## Notes

- Transfer time (10-30 seconds typical) bridged by UPS for critical loads
- Fuel consumption under full load determines mission sustainability window
- Generator maintenance status directly affects reliability during extended outages
