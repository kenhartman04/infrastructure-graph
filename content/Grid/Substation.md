---
type: grid-component
tier: distribution
backup_power: partial
voltage_class: medium
---

# Substation

Transforms voltage from transmission level down to distribution level (4kV–35kV). Contains transformers, circuit breakers, switches, and protection relays.

## Relationships

- [feeds:: [[Feeders]]]
- Steps power down from [[Transmission]]

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Disrupts — wind debris, structure damage | High |
| [[Flood]] | Interdicts — transformer submersion, total loss | Critical |
| [[Earthquake]] | Disrupts — bushing failure, foundation shift | High |
| [[Extreme Heat]] | Disrupts — transformer overheating, derated capacity | Medium |
| [[Ice Storm]] | Disrupts — bushing flashover from ice accumulation | Medium |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Hacking]] | Relay/RTU firmware exploitation | Compromises — false trip signals, protection disabled |
| [[Legacy Systems]] | Unpatched SCADA, serial protocols (DNP3/Modbus) | Compromises — no authentication on control commands |
| [[Physical Attack]] | Perimeter breach, transformer rifle attack | Interdicts — months-long replacement for custom transformers |
| [[Social Engineering]] | Vendor impersonation for site access | Compromises — implant on OT network |
| [[Foreign State]] | Pre-positioned malware (e.g., CRASHOVERRIDE-class) | Interdicts — coordinated breaker opening across substations |

## Notes

- Custom high-voltage transformers have 12–18 month lead times — single biggest long-pole for grid restoration
- Legacy substations often lack encryption, authentication, or network segmentation
- Physical security varies widely — rural substations often have only chain-link perimeter
