---
type: threat
domain: cyber
vector: technical
abbreviation: H
---

# Hacking

Direct technical exploitation of networked systems — SCADA/ICS compromise, firmware manipulation, network intrusion.

## Grid Impact

- [compromises:: [[Power Plant]]] — SCADA manipulation, unauthorized generation control
- [compromises:: [[Transmission]]] — false telemetry injection, relay manipulation
- [compromises:: [[Substation]]] — breaker control, protection relay disabling
- [compromises:: [[Feeders]]] — AMI/smart meter network exploitation

## Base Impact

- [compromises:: [[Data Center]]] — network intrusion, data exfiltration
- [compromises:: [[Control Tower]]] — ATC system disruption
- [compromises:: [[Operations]]] — C2 system degradation

## Cascade by Order

Computed by following typed links outward from this note: order 1 is what this threat hits directly, order 2 is what those failures take down, and so on. Requires the Dataview plugin with JavaScript queries enabled.

```dataviewjs
const kinds = ["interdicts", "disrupts", "compromises", "feeds", "fuels", "backs", "supports"];
const start = dv.current().file.path;
const found = new Map([[start, { order: 0 }]]);
let frontier = [start];
for (let order = 1; frontier.length > 0 && order <= 6; order++) {
  const next = [];
  for (const path of frontier) {
    const page = dv.page(path);
    if (!page) continue;
    for (const kind of kinds) {
      for (const link of [].concat(page[kind] ?? [])) {
        if (!link || !link.path || found.has(link.path)) continue;
        found.set(link.path, { order, via: path, kind });
        next.push(link.path);
      }
    }
  }
  frontier = next;
}
const rows = [...found]
  .filter(([, v]) => v.order > 0)
  .sort((a, b) => a[1].order - b[1].order)
  .map(([p, v]) => [v.order, dv.fileLink(p), dv.fileLink(v.via), v.kind]);
dv.table(["Order", "Affected", "Via", "Link type"], rows);
```

## Attack Patterns

- ICS/SCADA exploitation via IT-OT bridge
- Firmware implants on PLCs and RTUs
- Man-in-the-middle on unencrypted serial protocols (Modbus, DNP3)
- Ransomware on IT systems with OT bleedover

## Historical Examples

- CRASHOVERRIDE / Industroyer (2016): automated attack on Ukraine power grid — opened breakers via ICS protocols
- Colonial Pipeline (2021): ransomware on IT side forced OT shutdown
