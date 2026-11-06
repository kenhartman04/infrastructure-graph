---
type: threat
domain: natural
hazard_class: winter
---

# Ice Storm

Freezing rain accumulation >0.25 inches on surfaces. Degrades all exposed infrastructure.

## Grid Impact

- [interdicts:: [[Transmission]]] — conductor icing causes galloping and tower buckling
- [disrupts:: [[Substation]]] — bushing flashover, switch mechanism freeze
- [interdicts:: [[Feeders]]] — line breakage from ice weight, tree limb loading

## Base Impact

- [interdicts:: [[Runway]]] — ice accumulation, de-icing required
- [disrupts:: [[Gates]]] — mechanical freeze, sensor degradation
- [disrupts:: [[Perimeter]]] — camera/sensor icing, reduced visibility

## Cascading Effects

Grid generation loss (fuel supply + equipment freeze) coincides with peak heating demand → load shedding → base loses commercial power → backup generation under sustained cold-weather stress.

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

## Historical Examples

- Winter Storm Uri (2021): ERCOT generation collapsed under combined freeze + demand spike — military installations in Texas affected
