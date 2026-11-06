---
type: threat
domain: natural
hazard_class: fire
---

# Wildfire

Uncontrolled fire threatening infrastructure directly or triggering preemptive de-energization (PSPS).

## Grid Impact

- [disrupts:: [[Power Plant]]] — forced shutdown, air intake fouling
- [interdicts:: [[Transmission]]] — line sag into vegetation, tower damage
- [interdicts:: [[Feeders]]] — pole combustion, PSPS de-energization

## Base Impact

- [disrupts:: [[Perimeter]]] — fence/sensor damage in fire path
- [disrupts:: [[POL]]] — evacuation of fuel storage areas

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

## Notes

- Utility PSPS (Public Safety Power Shutoff) can interdict feeders preemptively even when fire is miles away
- Smoke/particulate degrades solar generation capacity
