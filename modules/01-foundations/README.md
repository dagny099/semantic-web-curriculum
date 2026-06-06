# Module 1 — Foundations

> RDF, Turtle, basic SPARQL. The conceptual core of the semantic web stack.

**Weeks:** 1-3
**Effort:** ~5-7 hours per week
**New ground:** Light — you've touched most of this

---

## Start here: choose your path through Module 1

Module 1 is organized as three self-paced submodules. Pick the path that fits how you learn.

### Path 1 — Full course path (recommended)

Best for learners who want the full conceptual foundation before building.

1. Read the module overview below and keep the [cheat sheet](../../reference/cheatsheets/module-1-cheatsheet.html) open.
2. For each submodule: do the canonical reading, read the Sensemaking synthesis page, run the workbook, save the receipt (see the table below).
3. Finish by building the Resume Graph Explorer RDF slice (Submodule 1.3).
4. Take the 30-second test: explain when you'd choose RDF over a labeled property graph, and when not to.

### Path 2 — Builder-first path

Best for learners who need a runnable win before the theory lands.

1. Start Fuseki and open the [cheat sheet](../../reference/cheatsheets/module-1-cheatsheet.html).
2. Run the [1.1 workbook](./submodules/1-1-workbook-naruto.html) (or the [mythology variant](./submodules/1-1-workbook-mythology.html)).
3. Run the [1.2 workbook](./submodules/1-2-workbook-naruto.html) (or [mythology variant](./submodules/1-2-workbook-mythology.html)).
4. Load `resume-001.ttl` and run the [1.3 resume workbook](./submodules/1-3-workbook-resume.html).
5. Then go back to the canonical readings and synthesis pages to understand what you just built.

### Path 3 — Artifact path

Best for advanced learners, portfolio builders, or return visits.

1. Read the [1.1 RDF vs. LPG synthesis](./submodules/1-1-rdf-vs-lpg.html).
2. Run enough workbook queries to confirm your data model intuitions.
3. Build your own resume RDF slice.
4. Write the side-by-side query comparison (Cypher vs. SPARQL).
5. Draft the end-of-module blog post or reflection.

---

## What you'll come away with

By the end of this module, you can:

- Read and write Turtle fluently
- Run basic SPARQL queries against multiple endpoints (local Fuseki + public Wikidata)
- Articulate clearly why RDF differs from JSON or a property graph — and when each fits
- Recognize when a domain naturally wants global identifiers vs. local ones

The **30-second test** for this module: explain to a working engineer why someone would choose RDF over a labeled property graph (or vice versa) without resorting to slogans. If you can do that confidently at the end of Week 3, the foundations have landed.

---

## Canonical readings by submodule

The rhythm for the full course path: read the canon → read the synthesis → run the workbook → save the receipt.

| Submodule | Canonical reading | Synthesis material | Workbook | Receipt |
|---|---|---|---|---|
| 1.1 — RDF as a data model | Allemang Ch. 1–3 · [W3C RDF Primer](https://www.w3.org/TR/rdf11-primer/) · [Turtle spec](https://www.w3.org/TR/turtle/) (skim) | [1.1 RDF vs. LPG](./submodules/1-1-rdf-vs-lpg.html) · [reading companion](./submodules/1-1-reading-companion.pdf) | [Naruto](./submodules/1-1-workbook-naruto.html) or [mythology](./submodules/1-1-workbook-mythology.html) | Explain the URI tax; inspect or create a small Turtle graph |
| 1.2 — SPARQL basics | DuCharme Ch. 1–2 | [1.2 SPARQL query forms](./submodules/1-2-sparql-basics.html) | [Naruto](./submodules/1-2-workbook-naruto.html) or [mythology](./submodules/1-2-workbook-mythology.html) · Wikidata orientation (Exercise 1.1) | Run SELECT, ASK, CONSTRUCT, DESCRIBE; save three query patterns |
| 1.3 — Vocabulary landscape | [Hogan et al., sections 3–4](https://kgbook.org/) · optional [Linked Data design note](https://www.w3.org/DesignIssues/LinkedData.html) | [1.3 vocabulary landscape](./submodules/1-3-vocabulary-landscape.html) | [Resume workbook](./submodules/1-3-workbook-resume.html) | Build or adapt a resume RDF slice; run the ESCO/SKOS interop query |

The W3C Primer is surprisingly readable — don't skip it just because it's a spec. The Turtle spec is a reference; bookmark it and skim §1-3 for orientation.

---

## Dataset paths

The Module 1 workbooks support two narrative datasets plus one resume dataset.

**Naruto path.** Use the Naruto workbooks if you want continuity with the rest of the curriculum. The Naruto graph carries forward into Module 2 ontology design, Module 3 reification and provenance, and Module 4 deployment.

**Greek mythology path.** Use the mythology workbooks if you want the same RDF, Turtle, and SPARQL patterns in a domain that may feel more familiar or less anime-specific. This is a fully supported alternate path, not a lesser version of the exercises.

**Resume path.** The 1.3 resume workbook is the professional-data path and the bridge into the module's primary artifact: a resume graph slice with RDF, SKOS, and ESCO-style interoperability.

## What runs where

The synthesis pages, reading companion, and cheat sheet are standalone — no Fuseki required; open them in any browser.

The hands-on workbooks (1.1, 1.2, 1.3) require a running Fuseki instance plus the Naruto or mythology example data from the [starter kit](https://github.com/dagny099/semantic-web-curriculum) (data files not yet included in this repo). Exception: `1-3-workbook-resume.html` uses `artifacts/resume-graph/ttl/resume-001.ttl`, which lives in this repo.

---

## Exercises

### Exercise 1.1 — Wikidata orientation *(1 hour)*

Open the [Wikidata Query Service](https://query.wikidata.org/) and run these queries. Use the helper UI to find Q-numbers and modify example queries rather than starting from scratch.

- All books written by Adrian Tchaikovsky (find his Q-number via search)
- All people who studied at MIT and have a Wikipedia article
- All ESCO-classified occupations whose label contains "data scientist"

Notes go in `notes/week-01-wikidata.md`. Capture: which queries were intuitive, which were surprising, what tripped you up.

### Exercise 1.2 — Hand-written FOAF graph *(1 hour)*

In a `.ttl` file, model yourself and three of your projects. Use:

- `foaf:Person` for the human
- A custom namespace (e.g. `https://sensemaking-ai.com/ns/`) for the projects
- `schema:` properties where they fit (`schema:codeRepository`, `schema:dateCreated`, `schema:description`)

Load into Fuseki. Write three SELECT queries that retrieve different cross-sections of the data. Commit the file as `exercises/1-2-foaf-graph.ttl` and the queries as `exercises/1-2-queries/`.

### Exercise 1.3 — Resume Graph Explorer RDF slice *(3-4 hours)* — **primary project**

See [Primary project hook](#primary-project-hook-resume-graph-explorer-rdf-slice) below.

### Exercise 1.4 — Naruto Graph Turtle slice *(2-3 hours)*

Take one arc from the [Naruto Network Graph](https://docs.barbhs.com/naruto-network-graph/) — Chunin Exams is the most self-contained — and convert ~20 character nodes plus their canonical relationships into Turtle.

Use:
- `schema:Person` (or a subclass) for characters
- Custom namespace for ninja-specific concepts (ranks, jutsu, villages)
- `schema:TVEpisode` for arc episodes

Load into Fuseki. Write three SPARQL queries that match queries already run in Neo4j on the same data. Compare query ergonomics — where does each language pull ahead?

Commit as `exercises/1-4-naruto-slice/` with `data.ttl`, `queries/*.rq`, and a `notes.md` capturing the comparison.

---

## Synthesis pages & reference

The published HTML companions to the reading — synthesis essays in the author's voice, plus the back-pocket reference you keep open while working. (Best viewed on the live site, [curriculum.barbhs.com](https://curriculum.barbhs.com/map.html).)

**Submodule 1.1 — RDF as a data model**

| Page | What it is |
|---|---|
| [1.1 — RDF vs. LPG](./submodules/1-1-rdf-vs-lpg.html) | Synthesis essay: why you'd reach for RDF over a property graph, illustrated with resume data. |
| [1.1 workbook — Naruto](./submodules/1-1-workbook-naruto.html) | Hands-on workbook: SELECT, ASK, CONSTRUCT on the Naruto graph. |
| [1.1 workbook — Greek mythology](./submodules/1-1-workbook-mythology.html) | The same workbook on the mythology domain. |
| [Reading companion (PDF)](./submodules/1-1-reading-companion.pdf) | Eases you into the denser Allemang and DuCharme chapters. |

**Submodule 1.2 — SPARQL basics**

| Page | What it is |
|---|---|
| [1.2 — SPARQL query forms](./submodules/1-2-sparql-basics.html) | Synthesis essay: the four query forms, querying Wikidata and local Fuseki. |
| [1.2 workbook — Naruto](./submodules/1-2-workbook-naruto.html) | Five query patterns beyond the basics: DESCRIBE, UNION, property paths, FILTER NOT EXISTS, VALUES. |
| [1.2 workbook — Greek mythology](./submodules/1-2-workbook-mythology.html) | The same five patterns on Greek mythology data. |

**Submodule 1.3 — Vocabulary landscape**

| Page | What it is |
|---|---|
| [1.3 — Vocabulary landscape](./submodules/1-3-vocabulary-landscape.html) | Synthesis essay: FOAF, Dublin Core, SKOS, schema.org — reuse before defining. |
| [1.3 workbook — Resume Graph](./submodules/1-3-workbook-resume.html) | Primary project workbook: build a resume RDF slice with ESCO/SKOS interop. |

**Reference**

| Page | What it is |
|---|---|
| [Module 1 cheat sheet](../../reference/cheatsheets/module-1-cheatsheet.html) | Back-pocket Turtle + SPARQL syntax. Keep it open the whole module. |
| [Glossary](../../glossary.html) · [Curriculum map](../../map.html) | Term definitions, and how all the pieces fit together. |

---

## Primary project hook: Resume Graph Explorer RDF slice

The Resume Graph anchors this module specifically because of ESCO/SKOS — that's where RDF's interoperability story has actual teeth and where the comparison with property graphs is sharpest.

### Goal

Take a small but representative subset of the Resume Graph Explorer Neo4j data (one resume, ~30-50 nodes) and produce a parallel Turtle version with side-by-side queries.

### Steps

1. Pick one resume with rich structure (multiple jobs, education, ESCO-linked skills). Your own is fine.
2. Export the relevant Neo4j subgraph as Cypher CREATE statements. Save to `artifacts/resume-graph/cypher/resume-001.cypher`.
3. Hand-write the equivalent in Turtle as `artifacts/resume-graph/ttl/resume-001.ttl`, reusing:
   - `foaf:Person` for the resume subject
   - `schema:Organization` for employers
   - `schema:DateTime` for dates
   - `skos:Concept` for skills with ESCO concept IRIs
   - Custom `sensemaking:` namespace for resume-specific structure
4. Load both into their respective stores (Neo4j and Fuseki).
5. Write the same three queries in both Cypher and SPARQL:
   - All jobs in chronological order
   - All skills associated with a job, with ESCO codes
   - All transitions between consecutive jobs

### What you'll feel

Cypher will be more ergonomic for the chronological query — Neo4j was built for path traversal. SPARQL will surprise you on the ESCO query because SKOS is *already RDF*; your ESCO links are first-class triples instead of foreign keys you have to join through.

---

## Pain points to surface

Sit with these tensions as you work through the module. Each shows up in the publishable blog post:

- **Why four serializations for the same data?** RDF/XML, N-Triples, Turtle, JSON-LD. Each exists because none is good enough for everything. You'll use Turtle for almost everything.
- **The URI tax.** RDF is more verbose than Cypher because every term is *globally* identifiable. That precision pays off in some contexts (data integration, regulatory environments) and is pure overhead in others.
- **Blank nodes.** RDF allows unnamed nodes. They're useful but break graph identity across systems. Two blank nodes from different sources can't be reliably compared.
- **Open-world assumption.** "Not stated" doesn't mean "false." This is the hardest mental shift coming from SQL or property graphs. Module 3 deals with this in depth; start noticing it now.

---

## Publishable deliverables

| Artifact | Where | Audience |
|---|---|---|
| Blog post: *"LPG vs RDF for resume graphs: a side-by-side"* | sensemaking-ai.com | Pragmatic engineers |
| Naruto Turtle slice committed publicly | this repo | Followers of the public learning |
| LinkedIn post linking to the blog | LinkedIn | Broader network |
| Two weekly progress LinkedIn updates | LinkedIn | Network at large |

---

## Synthesis notes

One paragraph per week, in your own words, capturing what landed and what didn't. These become source material for the blog post and for the Digital Twin's knowledge base.

- [ ] `notes/week-01.md`
- [ ] `notes/week-02.md`
- [ ] `notes/week-03.md`

---

## Checklist

### Reading
- [ ] Allemang Ch 1-3
- [ ] W3C RDF 1.1 Primer
- [ ] W3C Turtle spec (skim)
- [ ] DuCharme Ch 1-2

### Exercises
- [ ] 1.1 Wikidata orientation
- [ ] 1.2 FOAF graph
- [ ] 1.3 Resume Graph RDF slice (primary)
- [ ] 1.4 Naruto Graph Turtle slice

### Notes
- [ ] Week 1
- [ ] Week 2
- [ ] Week 3

### Deliverables
- [ ] Blog post drafted
- [ ] Blog post published
- [ ] LinkedIn post linking to blog
- [ ] Weekly LinkedIn updates × 2
- [ ] End-of-module reflection in `REFLECTIONS.md`

---

## When you're done

Take the 30-second test out loud: explain to a working engineer why someone would choose RDF over a labeled property graph (or vice versa). Record yourself if it helps. If the answer feels confident and concrete — with specific examples, not abstractions — the foundations have landed. Move to Module 2.

If the answer feels vague, redo Exercise 1.3 before moving on. The comparison work is where the conceptual difference clicks; rushing past it makes Module 2's modeling work harder.

---

## Module navigation

⬅ [Back to repo](../../README.md) · ➡ [Module 2 — Modeling](../02-modeling/module-02-README.html)
