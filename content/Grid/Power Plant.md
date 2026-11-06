---
type: grid-component
tier: generation
backup_power: false
voltage_class: high
---

# Power Plant

Generation source — converts fuel/renewable resource to electrical energy.

## Relationships

- [feeds:: [[Transmission]]]

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Disrupts — physical damage to structures, cooling systems | High |
| [[Flood]] | Disrupts — inundation of ground-level equipment | High |
| [[Extreme Heat]] | Disrupts — derated capacity, cooling water limits | Medium |
| [[Wildfire]] | Disrupts — forced shutdown, air intake fouling | Medium |
| [[Ice Storm]] | Disrupts — fuel supply chain interruption | Medium |
| [[Earthquake]] | Disrupts — structural/mechanical damage | High |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Hacking]] | SCADA/ICS exploitation | Compromises — unauthorized control of generation |
| [[Phishing]] | Credential theft from operators | Compromises — lateral movement into OT network |
| [[Physical Attack]] | Unauthorized site access | Interdicts — sabotage of critical equipment |
| [[Social Engineering]] | Insider manipulation | Compromises — policy bypass, access escalation |
| [[Foreign State]] | Supply chain implant, zero-day | Compromises — persistent access to control systems |

## Notes

- Single point of failure for downstream grid if no generation redundancy
- Legacy SCADA systems common — air-gapped networks increasingly bridged to IT
