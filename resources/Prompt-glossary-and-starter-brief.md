# Brief for glossary + starter template repo development

I'm building a 12-week self-directed semantic web curriculum ("Sensemaking Semantic Web") published openly under my consulting brand Sensemaking AI. The curriculum has four modules:

1. Foundations (RDF, Turtle, basic SPARQL)
2. Modeling (RDFS, OWL, ontology design)
3. Reasoning at the edge (inference, reification, SHACL)
4. Shipping (SPARQL UPDATE, deployment, LLM + KG)

The full syllabus, module READMEs, homebase HTML, and two early supporting artifacts (a Module 1 reading-companion deck and a Module 1 cheat sheet HTML page) are already built. They establish a visual and editorial system the new artifacts should match.

In a previous planning conversation, four candidate "back-pocket reference" supporting materials emerged as worth building (alongside the canonical readings, exercises, and synthesis pages):

1. **Cheat sheet** (already built — see attached `module-1-cheatsheet.html`)
2. **Glossary page** ← build this
3. **Common errors and how they look** (deferred until reader feedback accumulates)
4. **Starter template repo** ← build this

This chat is for building #2 and #4.

---

## What I want from this chat

Two distinct deliverables that share a visual system with the cheat sheet but solve different problems.

### Deliverable 1: Glossary page

A single self-contained HTML page (one file, no build step, CSS inline) that serves as the curriculum's definitional reference. It is the page a reader opens when they hit a term they're unsure about — "ontology," "punning," "reification," "open-world assumption" — and want a working definition in my voice rather than a Wikipedia paragraph.

What makes this glossary distinct from existing ones (Wikipedia, W3C glossaries, vendor docs):

- **The cog-sci frame earns its place.** When "schema" or "concept" or "type" has been overloaded across philosophy, knowledge engineering, and ML, the glossary names the disputes and resolves them for the curriculum's purposes. The cog-sci framing of "schemas as cognitive structures that get formalized as ontologies" is a thread that genuinely runs through my background.
- **Cross-references over isolation.** Each entry should link to related terms. The point is to let a reader follow a thread, not just look up one word.
- **Honest about contested terms.** Where "ontology" or "knowledge graph" has multiple legitimate definitions, the entry names that and explains what the curriculum means by it.
- **Voice consistency.** The entries are written in the curriculum's voice — declarative, contrastive, comfortable surfacing tradeoffs. Not encyclopedic neutrality.

Coverage target: roughly 50–80 entries, scoped to Modules 1–2 first (Foundations and Modeling), with placeholder structure for terms that will be added when Modules 3 and 4 come online. Don't try to define every reification approach in detail now — leave room for the glossary to grow.

Structural requirements:

- Alphabetical with section jump-letters (A–Z navigation strip)
- Per-entry: term, one-line gloss, longer definition (2–4 sentences usually, more when contested), "see also" cross-links to other entries
- Visual indicator for entries with multiple legitimate definitions, where the curriculum is taking a position
- Search/filter is **not required** (CSS-only solutions for filtering 50–80 entries on one page are over-engineering — Ctrl-F is fine)
- Print-friendly stylesheet (same as the cheat sheet — readers will print it)
- Matches the existing visual system: deep teal masthead, cream surface, coral accents, EB Garamond + IBM Plex Sans + IBM Plex Mono

### Deliverable 2: Starter template repo

A complete GitHub-ready starter repo (multiple files, real directory structure, runnable end-to-end) that someone following the curriculum can fork on day one and immediately have a working semantic web project skeleton. The implicit message is "this is how a senior practitioner structures day one of a knowledge graph project" — consulting positioning baked into the artifact itself.

What it should include:

- **`README.md`** — purpose, what's included, how to use, link back to the curriculum
- **`data/`** — one starter Turtle file using the curriculum's standard prefix block, with a small worked example (Naruto-flavored is fine — 5–10 characters with relationships)
- **`queries/`** — 3–5 numbered SPARQL queries answering different question types (one SELECT, one CONSTRUCT, one ASK, one with FILTER, one with aggregation)
- **`shapes/`** — one starter SHACL shape (placeholder for Module 3, but worth seeding the directory structure now)
- **`docs/`** — a `getting-started.md` walking through Fuseki setup and how to load the data and run a query end-to-end
- **`.gitignore`** — sensible defaults for a semantic-web project (Fuseki TDB directories, OS junk, IDE files)
- **`LICENSE`** — MIT for code, with a note that the example content is CC BY 4.0 (matching the main curriculum repo)
- **`fuseki/`** — a config snippet or assembler file for loading the data on a fresh Fuseki install
- One small, well-commented Python script using `rdflib` that loads the data, runs one query, and prints results — demonstrates programmatic access alongside the Fuseki UI path

What the starter template is NOT:

- Not a tutorial. A reader who clones it should understand it from the README + comments, not need a separate course.
- Not Naruto-specific. The example data is Naruto-flavored to match the curriculum, but the structure should work for any domain. Comments in the Turtle file should make this explicit.
- Not opinionated about which triplestore beyond Fuseki for development. Module 4 introduces Oxigraph for deployment; the starter doesn't need to anticipate that.

For this deliverable, produce the file contents and a clear directory tree. Don't try to actually create a GitHub repo — just produce the files I can drop into one.

---

## What I don't want from this chat

- Don't reproduce the cheat sheet — the glossary is a different artifact serving a different reader need.
- Don't over-engineer either deliverable. The cheat sheet works because it's restrained and scannable. Apply the same discipline.
- Don't add JavaScript filtering, search bars, dark-mode toggles, or other features that look impressive but don't earn their place.
- Don't write glossary entries by paraphrasing Wikipedia. If an entry is just a Wikipedia paraphrase, it shouldn't exist — point at the Wikipedia article and skip the redundant entry.
- Don't generate placeholder entries marked "TODO." If a term isn't ready to define, leave it out — the glossary grows with the curriculum.
- Don't claim the starter template uses libraries or tools I haven't confirmed are available (Fuseki and rdflib are confirmed; anything else, ask).

---

## Voice and conventions

**Brand context.** Sensemaking AI is an independent AI/ML consulting practice run solo by Barbara Hidalgo-Sotelo (Dagny). Cognitive scientist (MIT PhD), Azure AI Engineer Associate, CDMP, AWS CCP — but NOT a KGC-certified ontologist (which is part of why this curriculum exists). Never write "we" implying a team. Use "I" for personal reflection, "the curriculum" or "this project" for third-person.

**Editorial voice.** Declarative, contrastive, honest about complexity, cog-sci-flavored where it earns its place, no italics for emphasis (the voice does the work), no corporate-speak. Avoid "leverage," "stakeholder," "synergy," "robust," "comprehensive," "best-in-class."

**Sentence case for headers always.** No mid-sentence bolding of nouns.

**Active voice.** "Use this prefix block" not "this prefix block should be used."

**Concrete > abstract.** Examples drawn from the curriculum's anchoring projects (Naruto Network Graph, Resume Graph Explorer) where they fit naturally. Don't force them.

---

## Visual system

The existing cheat sheet (attached) establishes the system. Match it:

- **Palette:** `--teal-deep: #0B4F4A`, `--teal-mid: #1E8076`, `--teal-light: #C6E2DD`, `--coral: #D85A30`, `--coral-tint: #FAEAE2`, `--charcoal: #1F2A2E`, `--slate: #5A6671`, `--cream: #FAF7F2`, `--code-bg: #F2EDE3`, `--rule: #D8D2C6`
- **Typography:** EB Garamond italic for headers (display), IBM Plex Sans for body, IBM Plex Mono for code. Google Fonts CDN.
- **Masthead:** dark teal background, brand label in small caps, italic serif title, coral accent rule
- **Section labels:** small-caps coral above each section heading, numbered (`01 · PREFIXES` style)
- **Code blocks:** cream background, teal-mid left border, IBM Plex Mono
- **Callouts:** coral-tint background with coral left border for "Pitfall" / "Note" / "Mental shift"
- **Print stylesheet:** required, must produce a clean printable version with the masthead reduced to a plain header
- **Hairline rules** between sections, not heavy borders
- **No drop shadows, no gradients, no animation beyond hover-color shifts**

For the starter repo, "matches the visual system" means: README and docs use the same writing voice and a complementary markdown structure (clear hierarchy, code blocks well-fenced, no decorative emoji). No HTML needed in the repo itself.

---

## Coverage guide for the glossary

A non-exhaustive list of terms that earn entries at Module 1–2 level. Use this as a starting point — add others if obvious, omit any that feel forced.

**Core data model:** RDF, triple, subject, predicate, object, URI, IRI, blank node, literal, language tag, datatype, named graph, quad, graph

**Serialization:** Turtle, N-Triples, RDF/XML, JSON-LD, TriG

**Querying:** SPARQL, triple pattern, graph pattern, SELECT, ASK, CONSTRUCT, DESCRIBE, basic graph pattern, FILTER, OPTIONAL, UNION, property path, federated query, endpoint

**Vocabularies and ontologies:** vocabulary, ontology, schema, taxonomy, controlled vocabulary, concept scheme, knowledge graph, linked data, FOAF, schema.org, SKOS, Dublin Core, PROV-O

**RDFS / OWL:** class, instance, property, domain, range, subClassOf, subPropertyOf, OWL, OWL Full, OWL DL, OWL EL, OWL QL, OWL RL, reasoner, inference, materialization, equivalent class, restriction, cardinality, transitive property, symmetric property, inverse property, sameAs, equivalentClass, disjointWith

**Concepts and tensions:** open-world assumption, closed-world assumption, unique name assumption, monotonic reasoning, punning, reification, n-ary relation, time-indexed situation, semantic web, knowledge graph (LPG vs RDF flavor — yes, contested)

**Cog-sci adjacent (these earn their place):** schema (cognitive), concept (philosophical), category, frame, ontology (philosophical) — short entries that name the discipline gap and resolve it for the curriculum

For Modules 3 and 4, leave structural placeholders only: don't define SHACL, GraphRAG, federation, etc. yet. The glossary grows with the curriculum.

---

## Files to attach to this chat

**Required attachments** (the new chat won't have useful context without these):

1. `module-1-cheatsheet.html` — the visual system reference. The new artifacts should look like they belong with this.
2. `CLAUDE.md` — repo conventions, brand voice, naming patterns.
3. `module-01-README.md` and `module-02-README.md` — coverage scope for the glossary's initial entries.
4. `SYLLABUS.md` — the broader arc, so the glossary placeholders for Modules 3–4 are seeded in the right direction.
5. `tools.md` — the starter template references Fuseki by default; make sure the new chat knows the install path the curriculum recommends.
6. This brief itself, as the primary instruction set.

**Helpful but not required:**

7. `reading-list.md` — useful if the new chat wants to point glossary entries at canonical references.
8. `public-kgs.md` — useful for the vocabulary entries (FOAF, SKOS, etc.).
9. The Module 1.1 reading companion deck — for matching editorial tone in entry definitions.

**Skip these:**

- The original planning doc — the new chat doesn't need the meta-planning context; it needs the brief and the existing artifact to match.
- The Digital Twin READMEs — not relevant to Modules 1–2 glossary entries.
- The Naruto Network Graph docs — keep examples lightweight; the new chat doesn't need deep Naruto canon to write a good glossary entry.

---

## Build order

Prefer to build the glossary first. It's the higher-leverage artifact (more readers will hit it, it grows over time) and building it sharpens the voice for the starter repo's README. If only one gets done in the chat, the glossary is the one.

If both get built, the starter repo should reference the glossary's URL in its README (placeholder OK if not deployed yet) — "if you hit a term you don't recognize, the curriculum's glossary at <URL> probably has it."

---

## What success looks like

**For the glossary:** a reader at any point in Modules 1–2 can hit Ctrl-F, find any term they're unsure about, read a definition that sounds like it was written by someone who has thought about the field rather than someone who summarized it, and follow the cross-references to deepen their understanding. The "ontology" entry alone should make a working semantic-web practitioner nod and a cog sci PhD smile.

**For the starter repo:** a developer who's done Module 1 reading can clone the repo, follow `docs/getting-started.md`, and have a Fuseki instance loaded with the example data and one query returning results within 15 minutes. They can then strip out the Naruto example, add their own domain, and have a working project structure to grow into. The starter is opinionated enough to be useful and minimal enough to not be cosplay.
