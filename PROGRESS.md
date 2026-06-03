# Progress

> Live tracker for the Sensemaking Semantic Web curriculum. Updated weekly. Most recent activity at top.

**Currently:** Module 1 — Foundations
**Module:** Module 1
**Next milestone:** Complete Submodule 1.1 exercises; begin primary project (Resume Graph RDF slice)
**Last updated:** 2026-06-02

---

## How to read this file

Three sections matter:

1. **Activity log** — what happened recently, most recent at top. The narrative.
2. **Module checklists** — what's been completed, what's queued. The structure.
3. **Artifacts produced** — links to the published work as it ships. The receipts.

If you're catching up after a long absence, read the activity log top-down for the story arc.

---

## Activity log

### Module 1 launch — 2026-05-31

Module 1 launched. All three submodule synthesis pages are written and published, along with five hands-on workbooks (1.1 and 1.2 Naruto and mythology variants, plus the 1.3 resume workbook), a reading companion for the Allemang/DuCharme chapters, and the Module 1 cheat sheet. The resume artifact (`resume-001.ttl`) is committed to the repo. Navigation between submodules is wired.

Shipped materials:

- `modules/01-foundations/submodules/1-1-rdf-vs-lpg.html` — RDF vs. LPG synthesis essay
- `modules/01-foundations/submodules/1-1-workbook-naruto.html` — 1.1 Naruto workbook
- `modules/01-foundations/submodules/1-1-workbook-mythology.html` — 1.1 mythology workbook
- `modules/01-foundations/submodules/1-1-reading-companion.pdf` — Allemang/DuCharme reading companion
- `modules/01-foundations/submodules/1-2-sparql-basics.html` — SPARQL query forms synthesis
- `modules/01-foundations/submodules/1-2-workbook-naruto.html` — 1.2 Naruto workbook
- `modules/01-foundations/submodules/1-2-workbook-mythology.html` — 1.2 mythology workbook
- `modules/01-foundations/submodules/1-3-vocabulary-landscape.html` — vocabulary landscape synthesis
- `modules/01-foundations/submodules/1-3-workbook-resume.html` — 1.3 resume workbook
- `modules/01-foundations/artifacts/resume-graph/ttl/resume-001.ttl` — resume RDF data
- `reference/cheatsheets/module-1-cheatsheet.html` — Module 1 cheat sheet

### Week 0 — Setup *(complete as of 2026-05-31)*

- [x] Repo initialized and pushed to GitHub
- [x] Required reading materials acquired (Allemang/Hendler/Gandon, DuCharme bookmarks)
- [ ] Apache Jena + Fuseki installed locally and verified running on `localhost:3030`
- [ ] Protégé installed and opened once
- [ ] Hogan et al. introduction skimmed (sections 1-2 of kgbook.org)
- [ ] Calendar blocked for Module 1 reading and project time

---

## Module 1 — Foundations *(Weeks 1-3)*

**Status:** In progress

### Reading
- [ ] Allemang Ch 1-3 (RDF foundations, RDFS)
- [ ] W3C RDF 1.1 Primer
- [ ] W3C Turtle spec (skim for reference)
- [ ] DuCharme Ch 1-2 (Learning SPARQL)

### Exercises
- [ ] Exercise 1.1: Wikidata orientation
- [ ] Exercise 1.2: Hand-written FOAF graph in Turtle
- [ ] Exercise 1.3: Resume Graph Explorer RDF slice (primary project)
- [ ] Exercise 1.4: Naruto Graph Turtle slice (secondary)

### Synthesis notes
- [ ] Week 1 notes published
- [ ] Week 2 notes published
- [ ] Week 3 notes published

### Module deliverables
- [ ] Blog post drafted: *"LPG vs RDF for resume graphs: a side-by-side"*
- [ ] Blog post published on sensemaking-ai.com
- [ ] LinkedIn post linking to blog
- [ ] End-of-module reflection added to REFLECTIONS.md

**Checkpoint:** Can I explain in 30 seconds why someone would choose RDF over LPG (or vice versa)? If yes, foundations landed. If no, redo Exercise 1.3 before moving to Module 2.

---

## Module 2 — Modeling *(Weeks 4-6)*

**Status:** Not started

### Reading
- [ ] Allemang Ch 6-8 (RDFS Plus, basic OWL, modeling patterns)
- [ ] W3C OWL 2 Primer
- [ ] Hogan et al. Section 5 (schema, identity, context)

### Exercises
- [ ] Exercise 2.1: Protégé pizza walkthrough
- [ ] Exercise 2.2: Read one FIBO module
- [ ] Exercise 2.3: Naruto ontology v1.0 (primary project)

### Synthesis notes
- [ ] Week 4 notes published
- [ ] Week 5 notes published
- [ ] Week 6 notes published

### Module deliverables
- [ ] `naruto-ontology-1.0.0.ttl` published
- [ ] Ontology README + REUSE.md complete
- [ ] WebVOWL visualization captured
- [ ] SHACL shapes validate against real data
- [ ] Blog post: *"Designing an anime ontology in public: the small modeling decisions that compound"*
- [ ] LinkedIn post linking to ontology release

**Checkpoint:** Is the Naruto ontology published with a real README and validation? If yes, modeling landed.

---

## Module 3 — Reasoning at the edge *(Weeks 7-9)* ★

**Status:** Not started · *Hardest module — plan extra time*

### Reading
- [ ] Allemang Ch 9-13 (deeper OWL, modeling for inference)
- [ ] W3C SHACL spec (abstract + core constraint components)
- [ ] Hogan et al. Section 6 (deductive knowledge)

### Exercises
- [ ] Exercise 3.1: Watch HermiT reasoner work in Protégé
- [ ] Exercise 3.2: Hand-write all four reification approaches
- [ ] Exercise 3.3: Naruto reification project (primary, Project A)
- [ ] Exercise 3.4: Resume skill inference (Project B)

### Synthesis notes
- [ ] Week 7 notes published
- [ ] Week 8 notes published
- [ ] Week 9 notes published

### Module deliverables
- [ ] Reified Naruto KG slice committed to repo
- [ ] Skill inference Jupyter notebook published
- [ ] Blog post: *"Where OWL reasoners beat (and lose to) LLM reasoning"*
- [ ] Public-friendly post: *"Reifying the Naruto-verse: what fan canon teaches about contested knowledge"*
- [ ] LinkedIn posts linking each

**Checkpoint:** Am I comfortable explaining the four reification approaches and when to use each? If no, do Exercise 3.2 again before Module 4.

---

## Module 4 — Shipping *(Weeks 10-12)*

**Status:** Not started

### Reading
- [ ] Allemang Ch 14-15 (modeling for the enterprise)
- [ ] DuCharme Ch 5-6 (UPDATE, federation, applications)
- [ ] Microsoft GraphRAG paper (Edge et al., 2024)
- [ ] W3C SPARQL 1.1 Update spec

### Exercises
- [ ] Exercise 4.1: Triplestore deployed on EC2
- [ ] Exercise 4.2: Federation experiment against Wikidata
- [ ] Exercise 4.3: TwinKit Semantic v2.0 capstone

### Synthesis notes
- [ ] Week 10 notes published
- [ ] Week 11 notes published
- [ ] Week 12 notes published

### Module deliverables
- [ ] TwinKit v2.0 released on GitHub
- [ ] Naruto KG Explorer deployed publicly
- [ ] Case study: *"Building a hybrid semantic + vector knowledge twin (with Naruto)"*
- [ ] Updated portfolio card on barbhs.com
- [ ] LinkedIn capstone announcement
- [ ] Final REFLECTIONS.md entry

**Final checkpoint:** Is the Naruto KG Explorer deployed and queryable by anyone with a browser? Would I confidently take on a 4-week paid engagement to advise a team on adopting knowledge graphs? Yes/no is the credential test.

---

## Artifacts produced

| Artifact | Date | Module |
|---|---|---|
| [1.1 RDF vs. LPG synthesis](./modules/01-foundations/submodules/1-1-rdf-vs-lpg.html) | 2026-05-31 | Module 1 |
| [1.1 reading companion (PDF)](./modules/01-foundations/submodules/1-1-reading-companion.pdf) | 2026-05-31 | Module 1 |
| [1.1 Naruto workbook](./modules/01-foundations/submodules/1-1-workbook-naruto.html) | 2026-05-31 | Module 1 |
| [1.1 mythology workbook](./modules/01-foundations/submodules/1-1-workbook-mythology.html) | 2026-05-31 | Module 1 |
| [1.2 SPARQL query forms synthesis](./modules/01-foundations/submodules/1-2-sparql-basics.html) | 2026-05-31 | Module 1 |
| [1.2 Naruto workbook](./modules/01-foundations/submodules/1-2-workbook-naruto.html) | 2026-05-31 | Module 1 |
| [1.2 mythology workbook](./modules/01-foundations/submodules/1-2-workbook-mythology.html) | 2026-05-31 | Module 1 |
| [1.3 vocabulary landscape synthesis](./modules/01-foundations/submodules/1-3-vocabulary-landscape.html) | 2026-05-31 | Module 1 |
| [1.3 resume workbook](./modules/01-foundations/submodules/1-3-workbook-resume.html) | 2026-05-31 | Module 1 |
| [Module 1 cheat sheet](./reference/cheatsheets/module-1-cheatsheet.html) | 2026-05-31 | Module 1 |
| [resume-001.ttl](./modules/01-foundations/artifacts/resume-graph/ttl/resume-001.ttl) | 2026-05-31 | Module 1 |

---

## Reading log

Books and key papers as they're completed.

_None yet._

---

## Tooling installed

- [ ] Apache Jena + Fuseki
- [ ] Protégé
- [ ] Oxigraph (alternative triplestore)
- [ ] rdflib (Python)
- [ ] WebVOWL bookmarked

---

## Pauses and detours

If the curriculum gets paused (job offer, client engagement, life), this section documents why and for how long. Honesty about the path beats fake-perfect progress charts.

_No pauses yet._
