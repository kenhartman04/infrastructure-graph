---
type: base
branch: USAF
installation_class: major
---

# Air Force Base

Top-level node for a generic USAF installation. Subsystems below map to functional areas that each depend on grid power.

## Installation Components

### Flight Operations
- [[Runway]] — primary mission capability
- [[Taxiways]]
- [[Aprons]]
- [[Hangars]]
- [[Control Tower]]

### Security
- [[Perimeter]]
- [[Gates]]
- [[SecFo]]

### Mission Support
- [[Operations]]
- [[Intel]]
- [[Data Center]]
- [[Support]]

### Sustainment
- [[POL]] — fuel storage and distribution
- [[Personnel]]
- [[Food-Chow]]
- [[Gas Station]]

## Grid Dependencies

- Fed by [[Feeders]] (designated/priority utility circuits)
- Backed up by [[Backup Generation]] (diesel generators)
- Fuel: [[POL]] sustains backup generation, a finite supply window

## Base Power Distribution

Commercial power reaches each function through the base's own distribution.

- [feeds:: [[Runway]]]
- [feeds:: [[Control Tower]]]
- [feeds:: [[Hangars]]]
- [feeds:: [[Data Center]]]
- [feeds:: [[Operations]]]
- [feeds:: [[Intel]]]
- [feeds:: [[Perimeter]]]
- [feeds:: [[Gates]]]
- [feeds:: [[SecFo]]]
- [feeds:: [[POL]]] (fuel pumps)

## Vulnerability Summary

The base is a load node at the end of the grid dependency chain:
`[[Power Plant]]` → `[[Transmission]]` → `[[Substation]]` → `[[Feeders]]` → **Base**

Any upstream interdiction forces the base onto backup generation. Mission sustainability then depends on fuel reserves ([[POL]]) and resupply chain integrity.
