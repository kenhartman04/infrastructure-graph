---
type: threat
domain: natural
hazard_class: wind-water
---

# Hurricane

Sustained winds >74 mph with storm surge and flooding. Multi-day event with advance warning.

## Direct Impacts (1st order)

What the hurricane physically destroys or degrades on contact.

### Grid
- [disrupts:: [[Power Plant]]] — structural damage, cooling system compromise
- [interdicts:: [[Transmission]]] — tower collapse, line galloping
- [disrupts:: [[Substation]]] — wind debris, localized flooding
- [interdicts:: [[Feeders]]] — pole snaps, downed distribution lines

### Base
- [disrupts:: [[Runway]]] — FOD, standing water, lighting damage
- [disrupts:: [[Hangars]]] — roof/door damage from wind loading
- [disrupts:: [[Perimeter]]] — fence breach, sensor damage
- [disrupts:: [[POL]]] — supply chain interruption, tank farm exposure

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

### Why it matters

Once generators start, the clock is fuel: [[POL]] reserves set how long mission functions stay up, and resupply runs on the same roads, ports and pipelines the storm damaged.

## Historical Examples

- Hurricane Maria (2017): 100% grid loss in Puerto Rico, months-long restoration
- Winter Storm Uri (2021): cascading generation failures across ERCOT — not a hurricane but same grid-cascade pattern
