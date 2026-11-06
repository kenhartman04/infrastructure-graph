---
type: threat
domain: cyber
vector: physical
abbreviation: P
---

# Physical Attack

Kinetic or physical sabotage of infrastructure — overlaps cyber domain when physical access enables digital compromise.

## Grid Impact

- [interdicts:: [[Substation]]] — rifle attack on transformers (Metcalf-style), arson
- [interdicts:: [[Transmission]]] — tower cutting/bombing
- [interdicts:: [[Feeders]]] — pole/transformer vandalism

## Base Impact

- [interdicts:: [[Perimeter]]] — fence breach, IED
- [interdicts:: [[Runway]]] — FOD placement, surface damage
- [interdicts:: [[POL]]] — fuel storage sabotage

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

- Long-range rifle fire on transformer cooling oil (drain → overheat → failure)
- Cutting/bombing transmission towers at remote locations
- Physical access to substations for device implantation
- Coordinated multi-site physical attacks to overwhelm response

## Historical Examples

- Metcalf Sniper Attack (2013): coordinated rifle fire on PG&E substation transformers — $15M damage, no arrests
