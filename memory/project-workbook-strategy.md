---
name: project-workbook-strategy
description: Strategy and design decisions for the submodule 1.1 interactive workbooks (multi-domain)
metadata:
  type: project
---

Submodule 1.1 gets one HTML workbook per domain — separate files, shared CSS approach. Two domains confirmed: Naruto (done) and Greek/Roman mythology (in progress). Music ecosystem ruled out for now.

**Why:** Different learners; anime friend vs. classics friend. Each file is self-contained, openable locally with Fuseki, no build tooling needed. Nav bar at top of each links to the other: "Dataset: [Naruto] · [Greek mythology]."

**File locations:**
- Workbooks live in the **curriculum repo** at `modules/01-foundations/submodules/`
- Data files live in the **starter kit repo** at `data/` (multiple alternatives to ship with the kit)
- Current file: `1-1-workbook.html` (Naruto) — may need renaming to `1-1-workbook-naruto.html`
- New file: `1-1-workbook-mythology.html`

**Why:** Workbooks stay in curriculum repo (teaching context); data files stay in starter kit repo (runnable environment). They are companion artifacts, not co-located.

**Mythology dataset design (confirmed decisions):**
- 8 deities across 3 realms: Olympians (Zeus, Athena, Apollo, Ares), Sea (Poseidon, Triton), Underworld (Hades, Persephone)
- Group concept: `sensemaking:Realm` (not pantheon, not domain)
- Optional ability: `sensemaking:hasPower` — Ares intentionally has NONE (key teaching moment for OPTIONAL + open-world assumption)
- Symmetric rivalry: `sensemaking:rivalOf` — same property name as Naruto
- Directed mentor analog: `sensemaking:championed` — Zeus championed Athena/Apollo/Ares (3), Poseidon championed Triton (1), Hades championed Persephone (1)
- Inferred peer relationship (q05 CONSTRUCT): `sensemaking:pantheonmateOf`
- Multilingual: Greek (@el) and Latin (@la) names on all deities — Zeus/Jupiter, Athena/Minerva, Apollo/Apollo (same — good teaching gotcha), Ares/Mars, Poseidon/Neptunus, Triton/Triton (same), Hades/Pluto, Persephone/Proserpina

**Why championed over parentOf:** parentOf is genealogical (flat). championed captures the active conferral of domain/authority that defines these relationships in mythology. Creates richer comprehension questions — e.g., "Zeus championed both Athena and Ares, who are rivals. What does that say about his role?"

**Challenge C1 in mythology:** "Find deities with no powers listed" (not "find deities without a realm" — all 8 have realms). Answer: Ares (and possibly Triton depending on final dataset).

**How to apply:** When building mythology workbook, use this as the canonical source of truth. Don't re-litigate these decisions unless user explicitly revisits them.
