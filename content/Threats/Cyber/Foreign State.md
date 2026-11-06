---
type: threat
domain: cyber
vector: state-sponsored
abbreviation: F
---

# Foreign State

Nation-state cyber operations targeting critical infrastructure — highest capability, lowest frequency, highest consequence.

## Grid Impact

- [compromises:: [[Power Plant]]] — pre-positioned malware for wartime activation
- [interdicts:: [[Substation]]] — coordinated breaker attacks (CRASHOVERRIDE-class)
- [compromises:: [[Transmission]]] — EMS/SCADA persistent access for intelligence collection and contingency disruption

## Base Impact

- [compromises:: [[Data Center]]] — espionage, data exfiltration
- [compromises:: [[Intel]]] — counterintelligence targeting
- [compromises:: [[Operations]]] — C2 degradation as part of broader campaign
- [interdicts:: [[Control Tower]]] — ATC disruption during conflict escalation

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

- Supply chain compromise (hardware implants, software backdoors)
- Zero-day exploitation of ICS/SCADA systems
- Long-dwell persistent access (months to years before activation)
- Combined cyber-kinetic operations during conflict
- Targeting of grid as asymmetric deterrent

## Known Actors (Open Source)

- VOLT TYPHOON (PRC) — pre-positioned in US critical infrastructure
- SANDWORM (Russia/GRU) — Ukraine grid attacks 2015, 2016
