---
type: grid-component
tier: transmission
backup_power: false
voltage_class: high
---

# Transmission

High-voltage lines (69kV–765kV) carrying bulk power from generation to substations.

## Relationships

- [feeds:: [[Substation]]]
- Fed by [[Power Plant]]

## Natural Disaster Vulnerabilities

| Threat | Effect | Severity |
|--------|--------|----------|
| [[Hurricane]] | Interdicts — tower collapse, line galloping | Critical |
| [[Ice Storm]] | Interdicts — conductor icing, tower buckling | Critical |
| [[Wildfire]] | Interdicts — line sag into vegetation, tower damage | High |
| [[Tornado]] | Interdicts — localized tower destruction | High |
| [[Flood]] | Disrupts — tower foundation erosion | Medium |

## Cyber Vulnerabilities

| Threat | Vector | Effect |
|--------|--------|--------|
| [[Hacking]] | EMS/SCADA compromise | Compromises — false telemetry, relay manipulation |
| [[Physical Attack]] | Tower/conductor sabotage | Interdicts — line severed |
| [[Social Engineering]] | Utility employee targeting | Compromises — access to switching procedures |
| [[Foreign State]] | Coordinated multi-point attack | Interdicts — cascading line failures |

## Notes

- Most geographically exposed grid component — long corridors through open terrain
- Restoration time: days to weeks for tower replacement
- Right-of-way vegetation management is a persistent wildfire ignition risk
