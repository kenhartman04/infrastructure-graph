---
type: threat
domain: cyber
vector: structural
abbreviation: L
---

# Legacy Systems

Outdated, unpatched, or unsupported hardware/software in OT environments — not an attacker per se, but a persistent vulnerability that amplifies all other cyber threats.

## Grid Impact

- [compromises:: [[Substation]]] — serial protocols (DNP3, Modbus) with no authentication or encryption
- [compromises:: [[Power Plant]]] — legacy DCS/PLC firmware with known CVEs, no vendor patches

## Base Impact

- [compromises:: [[Control Tower]]] — legacy ATC systems with long upgrade cycles
- [compromises:: [[Data Center]]] — end-of-life servers, unsupported OS in SCIF environments

## Why This Matters

- OT equipment lifecycle: 20–30 years vs. IT lifecycle of 3–5 years
- Many substations still run Windows XP or embedded RTOS with no security updates
- Air-gap assumptions are increasingly invalid — remote access added for efficiency
- Vendor remote access portals (e.g., TeamViewer, VPN) often poorly secured

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
