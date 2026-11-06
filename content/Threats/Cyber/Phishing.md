---
type: threat
domain: cyber
vector: human
abbreviation: Ph
---

# Phishing

Credential harvesting or malware delivery via deceptive communication targeting utility/base personnel.

## Grid Impact

- [compromises:: [[Power Plant]]] — operator credential theft → control system access
- [compromises:: [[Substation]]] — vendor credential compromise → remote access to RTUs

## Base Impact

- [compromises:: [[Operations]]] — credential theft from base personnel
- [compromises:: [[Intel]]] — targeted spearphishing for classified system access
- [compromises:: [[Data Center]]] — admin credential harvesting

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

- Spearphishing utility operators with fake vendor portals
- Watering-hole attacks on industry-specific sites
- Credential stuffing from breached utility employee databases
- Business email compromise targeting procurement/vendor relationships
