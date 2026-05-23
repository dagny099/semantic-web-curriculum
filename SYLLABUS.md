# Syllabus

> The full 12-week curriculum. This is the canonical reference document — modules, exercises, deliverables, and the honest pain perspective on each segment of the semantic web stack.

**Author:** Barbara Hidalgo-Sotelo (Sensemaking AI)
**Last updated:** Pre-launch, 5/23/26
**Companion files:** [`README.md`](./README.md) · [`PROGRESS.md`](./PROGRESS.md) · [`CLAUDE.md`](./CLAUDE.md)

---

## Contents

- [How this curriculum works](#how-this-curriculum-works)
- [The arc, at a glance](#the-arc-at-a-glance)
- [Core resources](#core-resources) — see also [`resources/reading-list.md`](./resources/reading-list.md)
- [Pre-week setup](#pre-week-setup) — see also [`resources/tools.md`](./resources/tools.md)
- [Module 1 — Foundations](#module-1--foundations-weeks-1-3) — full README at [`modules/01-foundations/`](./modules/01-foundations/)
- [Module 2 — Modeling](#module-2--build-with-modeling-weeks-4-6) — full README at [`modules/02-modeling/`](./modules/02-modeling/)
- [Module 3 — Reasoning](#module-3--reasoning-at-the-edge--weeks-7-9) — full README at [`modules/03-reasoning/`](./modules/03-reasoning/)
- [Module 4 — Shipping](#module-4--shipping-semantic-systems-weeks-10-12) — full README at [`modules/04-shipping/`](./modules/04-shipping/)
- [Weekly rhythm](#weekly-rhythm)
- [Progress tracking & public learning rhythm](#progress-tracking--public-learning-rhythm)
- [Motivation infrastructure](#motivation-infrastructure)
- [Publishing plan](#publishing-plan)
- [When to stop or pause](#when-to-stop-or-pause)
- [Closing note on positioning](#closing-note-on-positioning)

---

## How this curriculum works

This is a four-module self-paced curriculum. The default rhythm is **12 weeks at ~5-7 hours per week**, but the modules are independent units: I can compress to 8 weeks, expand to 20, or pause between modules without losing momentum.

Each module has the same shape:

1. **What I'll actually learn** — the conceptual content, condensed
2. **Required reading** — 1-3 primary sources, with links
3. **Optional deeper reading** — for when a topic catches me
4. **Hands-on exercises** — small enough to fit in a weekend
5. **The pain perspective** — honest critique of the technology
6. **Project hook** — concrete work on Resume Graph Explorer or the Naruto Network Graph
7. **Publishable artifact** — the deliverable that goes on barbhs.com, sensemaking-ai.com, GitHub, or LinkedIn

Two existing projects provide the through-line:

- **[Naruto Network Graph](https://docs.barbhs.com/naruto-network-graph/)** is the primary canvas. 87 characters, 3 narrative arcs, 36 hand-coded canonical relationships layered over subtitle-based co-appearance edges. Pop-culture domains are standard in ontology pedagogy (Pizza is the canonical Protégé tutorial) for exactly this reason: rich categorical structure plus contested fan canon makes for excellent modeling exercises.
- **Resume Graph Explorer** anchors Module 1 specifically. Its existing ESCO/SKOS integration is genuine semantic-web interop — that's where the case for RDF over a property graph is sharpest. Returns in Module 3 as a venue for skill inference.

## The arc, at a glance

| Module | Theme | Weeks | New ground | Primary project hook |
|---|---|---|---|---|
| 1 | Foundations: RDF, Turtle, basic SPARQL | 1-3 | Light | Resume Graph Explorer (RDF slice with ESCO/SKOS) + Naruto Graph slice |
| 2 | Modeling: RDFS, OWL, ontology design | 4-6 | Medium | Naruto ontology (rich domain) |
| 3 | Reasoning at the edge: inference, reification, SHACL | 7-9 | Heavy ★ | Naruto reification + Resume skill inference |
| 4 | Shipping: SPARQL UPDATE, deployment, LLM+KG | 10-12 | Mixed | TwinKit Semantic v2.0 with Naruto KG as demo |

★ Module 3 is the hardest. Plan to slow down there.

---

## Core resources

The full annotated bibliography lives in [`resources/reading-list.md`](./resources/reading-list.md). Tools and software install notes are in [`resources/tools.md`](./resources/tools.md). Public knowledge graphs and SPARQL endpoints are in [`resources/public-kgs.md`](./resources/public-kgs.md).

The four references the curriculum points to repeatedly:

- **Allemang, Hendler & Gandon** — *Semantic Web for the Working Ontologist* (3rd ed., 2020). [workingontologist.org](https://workingontologist.org/) · [data.world/swwo](https://data.world/swwo)
- **DuCharme** — *Learning SPARQL* (2nd ed., 2013). [learningsparql.com](https://www.learningsparql.com/) · [bobdc.com/blog](https://www.bobdc.com/blog/)
- **Hogan et al.** — *Knowledge Graphs* (2021), open access. [kgbook.org](https://kgbook.org/)
- **W3C specifications** — RDF 1.1, Turtle, SPARQL 1.1, OWL 2, SHACL, SKOS, PROV-O. See [`resources/reading-list.md`](./resources/reading-list.md) for the full bookmark set.

---

## Pre-week setup

Roughly 2-3 hours before Module 1 begins:

1. **Install Apache Jena + Fuseki** locally. Verify Fuseki runs on `localhost:3030`. See [`resources/tools.md`](./resources/tools.md) for install notes.
2. **Install Protégé** and open it once.
3. **Create this repo** with the directory structure shown in [`README.md`](./README.md#repository-structure).
4. **Bookmark the W3C primers** listed in [`resources/reading-list.md`](./resources/reading-list.md).
5. **Acquire** Allemang/Hendler/Gandon (Kindle or print). Just have it.
6. **Skim** Hogan et al. introduction (kgbook.org sections 1-2). Vocabulary calibration only.

---

## Module 1 — Foundations (Weeks 1-3)

> Full module README: [`modules/01-foundations/`](./modules/01-foundations/)

**Goal:** Read and write Turtle fluently, run basic SPARQL queries against multiple endpoints (local + Wikidata), and articulate clearly why RDF differs from JSON or property graphs.

### What I'll actually learn

The conceptual core of RDF: knowledge as triples `(subject, predicate, object)` where subjects and predicates are URIs and objects are URIs or literals. The four serialization formats and when each is used. The basic SPARQL query forms: SELECT, ASK, CONSTRUCT, DESCRIBE. The vocabulary landscape: FOAF, Dublin Core, SKOS, schema.org.

I'll also learn the conceptual difference between RDF and labeled property graphs (LPG) — Neo4j, my existing tool — which is the most practically important comparison I can make as a consultant.

### Required reading

- Allemang et al. — Chapters 1-3 (RDF foundations, RDFS)
- [W3C RDF 1.1 Primer](https://www.w3.org/TR/rdf11-primer/)
- [W3C Turtle spec](https://www.w3.org/TR/turtle/) (skim, then reference)
- DuCharme — Chapters 1-2

### Optional deeper reading

- Hogan et al. — Sections 3-4 (data models, querying): [kgbook.org](https://kgbook.org/)
- Tim Berners-Lee — [Linked Data design note](https://www.w3.org/DesignIssues/LinkedData.html)

### Hands-on exercises

**Exercise 1.1 — Wikidata orientation (1 hour)**
Use the [Wikidata Query Service](https://query.wikidata.org/) helper UI:

- All books written by Adrian Tchaikovsky
- All people who studied at MIT with a Wikipedia article
- All ESCO occupations whose label contains "data scientist"

**Exercise 1.2 — Hand-write a tiny graph (1 hour)**
A `.ttl` file modeling myself and three projects using FOAF + custom namespace. Load into Fuseki. Three SELECT queries.

**Exercise 1.3 — Resume Graph Explorer slice (3-4 hours)** *(primary project)*

**Exercise 1.4 — Naruto Graph Turtle slice (2-3 hours)**
One arc (Chunin Exams) from the [Naruto Network Graph](https://docs.barbhs.com/naruto-network-graph/), ~20 character nodes plus canonical relationships in Turtle. Three SPARQL queries matching ones already run in Neo4j. Compare ergonomics.

### The pain perspective

- **Why four serializations?** RDF/XML, N-Triples, Turtle, JSON-LD. Each exists because none is good enough for everything.
- **The URI tax.** Compare `(Alice)-[KNOWS]->(Bob)` in Cypher to the equivalent Turtle. More verbose, but every term is *globally* identifiable. Both are correct for their context — the consultant skill is knowing which context the client is actually in.
- **Blank nodes** are useful but break graph identity across systems.
- **Open-world assumption.** "Not stated" doesn't mean "false." Module 3 deals with this in depth; start noticing it now.

### Primary project hook: Resume Graph Explorer RDF slice

Take a representative subset of my Neo4j Resume Graph (one resume, ~30-50 nodes) and produce a parallel Turtle version with side-by-side queries.

Steps:
1. Pick one resume with rich structure (multiple jobs, education, ESCO-linked skills).
2. Export the Neo4j subgraph as Cypher CREATE statements.
3. Hand-write the equivalent in Turtle using `foaf:Person`, `schema:Organization`, `schema:DateTime`, `skos:Concept` for skills, custom `sensemaking:` namespace for resume-specific structure.
4. Load into both Neo4j and Fuseki.
5. Write three queries in both Cypher and SPARQL: chronological jobs, skills with ESCO codes, consecutive-job transitions.

Cypher will be more ergonomic for chronological traversal. SPARQL will surprise my on the ESCO query because SKOS is already RDF.

### Publishable artifact

Blog post on sensemaking-ai.com: *"LPG vs. RDF for resume graphs: a side-by-side."* The first piece in a "Pragmatic semantic web" series.

---

## Module 2 — Build with modeling (Weeks 4-6)

> Full module README: [`modules/02-modeling/`](./modules/02-modeling/)

**Goal:** Design and publish a small OWL ontology with documented design decisions and SHACL constraints. This is where modeling *judgment* develops — the central professional skill in this field.

### What I'll actually learn

The shift from "RDF is a data format" to "ontology is a design discipline." OWL classes, individuals, object properties, datatype properties, restrictions, equivalence. The five OWL profiles (DL, EL, QL, RL, Full) and why they exist. Modeling decisions: define new vs. reuse, class vs. instance, time and events, n-ary relationships.

### Required reading

- Allemang et al. — Chapters 6-8 (RDFS Plus, basic OWL, modeling patterns)
- [W3C OWL 2 Primer](https://www.w3.org/TR/owl2-primer/)
- Hogan et al. — Section 5 (schema, identity, context)

### Optional deeper reading

- [Ontology Design Patterns portal](http://ontologydesignpatterns.org/) — read patterns for `Information Realization`, `Time-Indexed Situation`, `N-ary Relation`
- [Pizza Tutorial](https://www.michaelcdebellis.com/post/new_protege_pizza_tutorial) — classic Protégé tutorial, worth doing once
- DuCharme — Chapters 3-4

### Hands-on exercises

**Exercise 2.1 — Protégé pizza walkthrough (2-3 hours)**
The standard first ontology. Muscle memory with Protégé.

**Exercise 2.2 — Read an enterprise ontology (1 hour)**
Browse the [Financial Industry Business Ontology (FIBO)](https://spec.edmcouncil.org/fibo/). Read one module's documentation. Notice the rigor.

**Exercise 2.3 — Build a Naruto ontology (8-12 hours)** *(primary project)*

### The pain perspective

- **OWL profiles confusion.** OWL Full is undecidable; DL, EL, QL, RL each trade expressive power for computational guarantees.
- **Punning.** Sometimes I'll want something to be both a class and an instance. OWL 2 allows it. Useful and confusing.
- **The transitivity trap.** Transitive, symmetric, inverse declarations cascade through reasoning. Performance gets pathological quickly.
- **Reusing vs. defining.** No clean rule. Only judgment.
- **Open-world reasoning bites.** I'll write a query that returns surprising results because the reasoner inferred a class membership I may not have expected.

### Project hook: A Naruto ontology

Design and publish `naruto-ontology-1.0.0.ttl` — an OWL ontology that formalizes the structure of the Naruto universe on top of the co-appearance graph I've already built.

The Naruto domain has unusually rich categorical structure: subclass hierarchy in ninja ranks, multiple relationship types (sensei-of, member-of-team, member-of-village, has-jutsu, rival-of, family-of), temporal events (arcs, episodes), and contested fan-canonical material that creates real ontology design tradeoffs.

Steps:

1. **Decide scope.** Focus on what my existing graph covers — three S-tier arcs, 87 characters. Core classes:
   - `Character` (subclass of `schema:Person`)
   - `Ninja` (subclass of `Character`)
   - `NinjaRank` (subclasses `Genin`, `Chunin`, `Jonin`, `Kage`)
   - `Village` (subclass of `schema:Organization`)
   - `Team` (subclass of `schema:Organization`)
   - `Jutsu` (custom)
   - `Arc` (subclass of `schema:Event` or `schema:CreativeWork`)
   - `Episode` (reuse `schema:TVEpisode`)
   - Object properties: `senseiOf`, `studentOf`, `memberOfTeam`, `memberOfVillage`, `hasJutsu`, `rivalOf`, `familyOf`

2. **Reuse where possible.** `schema:` for everything that has a schema.org equivalent. Document in `REUSE.md`.

3. **Define what's new carefully.** Jutsu and NinjaRank are clear. Characters whose rank changes across arcs is where time-indexed situations come in.

4. **Add restrictions carefully.** A `Ninja` must have ≥1 `memberOfVillage`. A `Team` must have ≥1 `memberOfTeam`. Resist more until I have data to validate against.

5. **Express constraints in SHACL.** Closed-world by default. Write shapes for `Ninja`, `Team`, `Arc`.

6. **Validate against real data.** Convert my existing Chunin Exams arc subset. Iterate.

7. **Publish.** Push to this repo under `modules/02-modeling/naruto-ontology/` with README, REUSE.md, example data, example queries, WebVOWL screenshots.

**Optional secondary project: career narrative ontology.** Stretch goal. `CareerTransition` as a class with `fromRole`, `toRole`, `transitionType`. Consulting-positioning gold.

### Publishable artifacts

- Naruto ontology in the curriculum repo
- Blog post on sensemaking-ai.com: *"Designing an anime ontology in public: the small modeling decisions that compound"*
- LinkedIn post linking the blog
- Optional Twitter/Mastodon thread with WebVOWL hook image for Naruto + tech audience

---

## Module 3 — Reasoning at the edge ★ (Weeks 7-9)

> Full module README: [`modules/03-reasoning/`](./modules/03-reasoning/)

This is the segment where most of the material is genuinely new ground. Plan accordingly — front-load the reading in the first week.

### What I'll actually learn

**Inferencing.** Reasoners take my ontology plus data and derive new triples. RDFS reasoning is simple (subclass/subproperty inheritance). OWL reasoning is powerful and slower. Rule languages too (SWRL, SHACL Advanced).

**Reification.** Four ways to talk *about* statements:
1. Classical RDF reification — verbose; every statement becomes four triples
2. N-ary relations — turn the binary relation into a class
3. Named graphs — put related statements in a named container
4. RDF-star — newer syntax; not universally supported

**Bridging vocabularies (alignment).** `owl:sameAs`, `owl:equivalentClass`, `skos:exactMatch`, `skos:closeMatch`. *Not* interchangeable — wrong choice cascades through reasoning dangerously.

### Required reading

- Allemang et al. — Chapters 9-13
- [W3C SHACL spec](https://www.w3.org/TR/shacl/) — abstract + Core Constraint Components
- Hogan et al. — Section 6 (deductive knowledge)

### Optional deeper reading

- [*Validating RDF Data*](http://book.validatingrdf.com/) (Labra Gayo et al., 2018) — open access on SHACL and ShEx
- [W3C OWL 2 Profiles](https://www.w3.org/TR/owl2-profiles/) — definitions of DL, EL, QL, RL
- DuCharme — Chapter 5

### Hands-on exercises

**Exercise 3.1 — Watch a reasoner work (1 hour)**
In Protégé with HermiT, declare `mentor` as sub-property of `colleague`, make `colleague` symmetric, add an instance. Run reasoner. Observe inferences.

**Exercise 3.2 — All four reification approaches (3 hours)**
Same fact in all four styles. SPARQL query for each that retrieves the fact with its source. Compare verbosity.

**Exercise 3.3 — Naruto reification (8-10 hours)** *(primary project A)*

**Exercise 3.4 — Skill inference (6-8 hours)** *(primary project B)*

### The pain perspective

- **Open-world reasoning bugs.** "No listed children" ≠ "zero children." Causes real bugs in applications written by developers who didn't learn this distinction.
- **`owl:sameAs` is a hammer.** Collapses all properties. Use `skos:exactMatch` when you mean "same referent without merging attributes."
- **Inference materialization tradeoffs.** Compute once and store (fast, stale) vs. compute at query time (fresh, slow). Both are wrong sometimes.
- **Reification verbosity is a real cost.** Multiplies storage and complicates queries. One of the most-cited reasons people pick LPG.
- **The "open world" I'll learn to want.** The inflection point of becoming a real ontologist is when "this is broken" shifts to "this is honest."

### Project hook A: Reification in the Naruto graph

The Naruto domain is unusually well-suited to reification work — so much canon is contested, fan-theorized, or revealed retroactively across the series. Different sources (manga vs. anime, databook vs. movie, fan-canon vs. official) disagree.

Goal: take a slice of my Naruto ontology and add full provenance — who claims this, in what source, when revealed, with what confidence.

Steps:
1. Pick a subset rich with contested or retroactively-revealed material. Itachi's true motivations (revealed late, contradicting earlier appearances) is a perfect example. ~20-30 assertions.
2. Express each fact using named graphs + [PROV-O](https://www.w3.org/TR/prov-o/) for source attribution.
3. Annotate with `dcterms:source` (manga vol/chapter, anime episode), `dcterms:date`, custom `sensemaking:confidence` (canon-strength).
4. SPARQL queries that:
   - Retrieve only manga-canonical facts above confidence threshold
   - Identify anime-only (filler) vs. manga-canonical facts
   - Find characters whose backstory was retroactively changed
5. Reflect (500 words): would Neo4j with edge properties have been easier? Where does RDF win? Where does it lose?

### Project hook B: Skill inference in Resume Graph Explorer

Use OWL property characteristics + SPARQL CONSTRUCT to infer skills not explicitly stated.

Example rules:
- If a person held a `Role` whose ESCO concept `skos:related` skill X, infer exposure to X.
- If a role was held >2 years, escalate exposure to "demonstrated."
- If two skills are both required by many of a person's roles, mark as "core competencies."

This is exploratory reasoning — connects directly to what my `narrative synthesizer` does heuristically with LLMs. The interesting question: where is formal reasoning better than LLM reasoning, and where is it worse?

### Publishable artifacts

- Jupyter notebook in `modules/03-reasoning/notebooks/` demonstrating skill inference
- Blog post: *"Where OWL reasoners beat (and lose to) LLM reasoning"* — highest-leverage essay I can write immediately
- Accessible companion post (barbhs.com): *"Reifying the Naruto-verse: what fan canon teaches us about modeling contested knowledge"*
- LinkedIn posts linking each

---

## Module 4 — Shipping semantic systems (Weeks 10-12)

> Full module README: [`modules/04-shipping/`](./modules/04-shipping/)

**Goal:** Deploy a production-style semantic system. Understand SPARQL UPDATE, federation, versioning, deployment patterns, and the modern LLM-augmented retrieval landscape.

### What I'll actually learn

**SPARQL UPDATE.** INSERT, DELETE, CONSTRUCT-into-graph. Transactional considerations.

**Federation.** SPARQL's `SERVICE` keyword across endpoints. Powerful, slow, fragile in production.

**Deployment patterns.** Triplestore options (see [`resources/tools.md`](./resources/tools.md)), backup, versioning, scaling, monitoring.

**LLM + KG integration.** The current frontier. Graph-RAG patterns: entity-centric retrieval, community summarization (Microsoft GraphRAG), hybrid vector + graph retrieval.

### Required reading

- Allemang et al. — Chapters 14-15
- DuCharme — Chapters 5-6 (UPDATE, federation, applications)
- [Microsoft GraphRAG paper](https://arxiv.org/abs/2404.16130) (Edge et al., 2024) — *"From Local to Global: A Graph RAG Approach to Query-Focused Summarization"*
- [W3C SPARQL 1.1 Update](https://www.w3.org/TR/sparql11-update/)

### Optional deeper reading

- [Microsoft GraphRAG project page](https://www.microsoft.com/en-us/research/project/graphrag/) and [GitHub](https://github.com/microsoft/graphrag)
- Juan Sequeda's writing on KGs in the LLM era (LinkedIn + data.world blog)
- Hogan et al. — Sections 7-10 (inductive, creation, quality, refinement)

### Hands-on exercises

**Exercise 4.1 — Deploy a triplestore on EC2 (3-4 hours)**
Add Oxigraph or Fuseki alongside my existing Uptime Kuma infrastructure. Document in `docs/triplestore-deployment.md`.

**Exercise 4.2 — Federation experiment (2 hours)**
Local Fuseki + Wikidata via `SERVICE`. Note latency and failure modes.

**Exercise 4.3 — TwinKit Semantic v2.0 (12-15 hours)** *(capstone)*

### The pain perspective

- **SPARQL UPDATE is not transactional in the SQL sense.** Most triplestores offer ACID at graph or statement level, but cross-graph multi-statement transactions are inconsistently supported.
- **Ontology versioning is unsolved.** Semver doesn't quite map. Adding a class is "minor"; adding a required restriction is "breaking." Tooling for diff is weak.
- **Federation is powerful and slow.** Most production systems materialize external data locally and refresh on a schedule.
- **The deployment market is small.** No Postgres-equivalent. I'm choosing among 5-7 viable triplestores, each with rough edges.
- **The semantic web's marketing problem.** The 2001 vision didn't materialize as sold. Successes have been narrower (life sciences, finance, government, schema.org for SEO, Wikidata). The LLM moment is causing a renaissance, but the renaissance is *graph-shaped*, not necessarily *RDF-shaped* — which puts my position (one foot in LPG, one foot in semantic web) unusually well.

### Capstone: TwinKit Semantic v2.0 + Naruto Knowledge Graph as demo

My `TwinKit` framework currently builds RAG-powered digital twins using ChromaDB. Add a semantic layer: an ontology, a SPARQL endpoint, and hybrid retrieval combining vector similarity with graph traversal.

**Two birds, one stone.** TwinKit Semantic is the framework. The Naruto Knowledge Graph (my ontology from Module 2 + reified assertions from Module 3) is the demonstration dataset.

Steps:

1. **Deploy a triplestore.** Oxigraph or Fuseki.
2. **Use `naruto-ontology-1.0.0.ttl`** from Module 2 as the demonstration domain ontology. Load Module 3 reified assertions.
3. **Build a parallel ingestion pipeline** alongside ChromaDB ingestion. Regex-based extraction for structured fields, LLM-assisted extraction for entities in prose.
4. **Expose a SPARQL endpoint.** Public, read-only, CORS configured.
5. **Build a public Naruto KG Explorer demo.** Gradio or D3.js app. Natural-language questions, generated SPARQL visible, character network exploration with ontology layered over co-appearance.
6. **Augment retrieval.** Graph-traversal step in RAG: SPARQL query finds related entities, then biases ChromaDB retrieval toward chunks mentioning those entities.
7. **Eval before and after.** 20 multi-hop questions. Measure vector-only vs. hybrid. Document where hybrid is *worse*, not just where it's better.
8. **Write the case study.** *"Hybrid semantic + vector retrieval: an honest evaluation, using Naruto."* Architecture, results, code, deployment notes.
9. **Update TwinKit README.** Position: "Build RAG-powered digital twins with optional semantic layer."

### Publishable artifacts

- TwinKit v2.0 released on GitHub with semantic layer documented
- Naruto KG Explorer deployed publicly (HuggingFace Spaces or EC2)
- Case study on barbhs.com: *"Building a hybrid semantic + vector knowledge twin (with Naruto)"*
- Portfolio card: "TwinKit Semantic" with Naruto demo as its visual
- LinkedIn post: capstone announcement with eval results as the hook
- Conference talk submission for 2027 venue if it lands

---

## Weekly rhythm

Total weekly commitment averages **5-7 hours**, weighted by phase:

- **One weekday evening, ~90 min** — required reading
- **One weekend block, 2-3 hours** — project work
- **One weekday lunch, ~30 min** — synthesis notes
- **Buffer, ~1 hour distributed** — exercises, blog drafts, exploration

The synthesis notes ritual is the most important habit. Without it, the material doesn't consolidate. With it, the notes become source material for the Digital Twin's knowledge base, blog posts, and Toastmasters speeches.

---

## Progress tracking & public learning rhythm

Live tracker in [`PROGRESS.md`](./PROGRESS.md). Updated weekly. Anyone landing on the repo sees, at a glance, where the work is.

Synthesis notes (one paragraph per week in my own words) live in `modules/0X-name/notes/week-NN.md`.

**Publishing rhythm.** Plan in advance, not weekly. 24 posts over 12 weeks; improvising by Module 3 will start to slip. Template:

- **Monday LinkedIn post:** progress + one insight from the week's reading
- **Friday LinkedIn post:** an artifact or a question — link to whatever new lives in the repo
- **End of each module:** longer-form blog post on sensemaking-ai.com or barbhs.com
- **Quarterly:** a "what I learned" reflection in `REFLECTIONS.md`

Three checkpoints worth marking publicly:

- **End of Module 1.** Can I explain in 30 seconds why someone would choose RDF over LPG? Post about it.
- **End of Module 2.** Is the Naruto ontology v1.0 published? Announce the release.
- **End of Module 4.** Is the Naruto KG Explorer deployed and working? Yes/no is my credential test.

---

## Motivation infrastructure

I don't need motivation tactics; I need structure that makes momentum the path of least resistance.

**The Digital Twin doubles as my accountability partner.** Weekly notes feed its knowledge base. By Module 2, the twin should answer "what is Barb learning about semantic web?" coherently. By Module 4, it should explain reification with examples from Naruto Network graph. Recursive use of the technology — the system I'm building is also learning what I'm learning.

**Toastmasters bridges the speech work.** Each blog post can become a 5-7 minute speech, in English or Spanish. Translation reveals which vocabulary I understand vs. recite.

**Publishable artifacts are the actual deliverables.** No extra publication step beyond the curriculum work. The blog post IS the deliverable.

**The portfolio compounds.** By the end: 4-6 new portfolio artifacts, 1-2 published ontologies, an upgraded Digital Twin, and a case study at the LLM+KG intersection.

---

## Publishing plan

| Module end | Artifact | Where | Audience |
|---|---|---|---|
| 1 | Blog post: LPG vs RDF side-by-side (with ESCO punchline) | sensemaking-ai.com | Pragmatic engineers |
| 1 | Naruto graph Turtle slice committed publicly | curriculum repo | Followers of the public learning |
| 2 | Naruto ontology v1.0 | curriculum repo + GitHub release | Ontologists + anime fans |
| 2 | Blog post: ontology design in public | sensemaking-ai.com | Practitioners |
| 3 | Reified Naruto KG with provenance | curriculum repo | Followers + technical peers |
| 3 | Notebook + blog: skill inference (Resume) | huggingface + barbhs.com | Recruiters + peers |
| 3 | LinkedIn post: OWL vs LLM reasoning | LinkedIn | Broader network |
| 4 | TwinKit v2.0 release | GitHub | Open-source community |
| 4 | Naruto KG Explorer (deployed demo) | HF Spaces or EC2 | Anyone curious |
| 4 | Case study: hybrid semantic+vector twin | barbhs.com | Hiring managers + clients |
| 4 | LinkedIn post: capstone announcement | LinkedIn | Network at large |

Eleven publishable artifacts in 12 weeks.

---

## When to stop or pause

Honest stopping conditions:

- **A serious client engagement or job offer.** Take the job. The curriculum waits.
- **Module 2 modeling project stalls past 2 weeks.** Pause. Write up "lessons from a stalled ontology project" as a credible artifact.
- **I’m not enjoying it.** The curriculum is voluntary. Semantic web technology is interesting but not the only path. Dreading the next module is data.

These aren't failure modes. They're "this isn't the right vehicle right now" modes.

---

## Closing note on positioning

After this curriculum, my professional positioning becomes notably specific:

> *Cognitive scientist who builds production AI systems, with working fluency in knowledge representation and live deployments combining vector and graph retrieval — published openly through a 12-week self-directed program with all artifacts on GitHub.*

This is a small population. Most cog sci PhDs who build production systems don't know formal semantics. Most semantic web practitioners don't have a cog sci background. Very few people in either group publish their entire learning process openly.

The Naruto Knowledge Graph Explorer is the public-friendly entry point — accessible to anyone who lands on it, fun enough to share — that opens conversations leading to the more substantive case study work behind it.

I'm not betting on RDF becoming the future of the web. I'm betting on being one of the few people who can speak both the LLM/RAG language and the formal-semantics language fluently — and on that intersection growing in value as graph-augmented LLMs become more mainstream.

The work is the asset. The curriculum repo, the blog posts, and the deployed demos are the receipts.

---

## Navigation

[README](./README.md) · [PROGRESS](./PROGRESS.md) · [CLAUDE.md](./CLAUDE.md) · [REFLECTIONS](./REFLECTIONS.md)

**Modules:** [01 Foundations](./modules/01-foundations/) · [02 Modeling](./modules/02-modeling/) · [03 Reasoning](./modules/03-reasoning/) · [04 Shipping](./modules/04-shipping/)

**Resources:** [Reading list](./resources/reading-list.md) · [Tools](./resources/tools.md) · [Public KGs](./resources/public-kgs.md)
