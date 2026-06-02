# CLAUDE.md

Guidance for Claude (and other AI assistants) working in this repository.

## What this project is

A 12-week self-directed semantic web curriculum being worked through in public. The repo contains a syllabus, weekly progress, exercises, ontologies, queries, notes, and published artifacts. Both the **technical content** (Turtle, SPARQL, OWL, demos) and the **written content** (READMEs, blog posts, LinkedIn posts, synthesis notes) live here.

When in doubt about scope or direction, read [SYLLABUS.md](./SYLLABUS.md) first, then [PROGRESS.md](./PROGRESS.md) to see where the work currently is.

## Author & brand context

This is published under **Sensemaking AI**, an independent AI/ML consulting practice. Sensemaking AI is run solo by **Barbara Hidalgo-Sotelo** (Dagny). The curriculum is her work, published openly under her consulting brand.

This means:

- **Never write "we"** in a way that implies a team. Use "I" for personal reflection, "the curriculum" or "this project" for third-person, or "Sensemaking AI publishes" when referring to the brand context.
- **Never invent or imply credentials Dagny hasn't earned.** She has an MIT PhD in cognitive science and active certifications (Azure AI Engineer Associate, CDMP, AWS CCP). She does NOT (yet) have a KGC certificate or formal semantic-web credential — that's part of why this curriculum exists.
- **Don't hide that this is one person's learning.** That honesty is the point.

## Voice & tone

Dagny's professional voice is:

- **Curious, cog-sci flavored** — comfortable invoking schemas, meaning-making, cognitive frames
- **Pragmatic** — favors "things people actually use" over theory for its own sake
- **Slightly playful** — comfortable with quirky domains (beehive monitoring, Naruto, 14 years of personal workout data)
- **Honest about complexity** — willing to surface tradeoffs and pain points rather than selling

Her brand headline: *"Exploring messy data, intelligent systems, and what it means to make meaning — through the lens of a cognitive scientist who builds things people actually use."*

When drafting content:

- **Sentence case** for headers (always)
- **No mid-sentence bolding** of nouns or concepts
- **No corporate-speak.** Avoid "leverage," "stakeholder," "synergy," "robust," "best-in-class."
- **Active voice.** "I built X" not "X was built."
- **Concrete > abstract.** "ESCO has ~3,000 occupation concepts mapped via SKOS" beats "comprehensive occupational taxonomies."
- **Surface the pain.** When discussing a technology, name what's hard about it, not just what's good.

## File and directory conventions

```
sensemaking-ai/semantic-web-curriculum/
├── README.md              # Repo front door
├── SYLLABUS.md            # The full 12-week curriculum
├── PROGRESS.md            # Live tracker, updated weekly
├── REFLECTIONS.md         # Cross-module reflections, added over time
├── CLAUDE.md              # This file
├── modules/
│   └── 0N-name/
│       ├── README.md      # Module overview (follows Module 1's template)
│       ├── submodules/    # Learning materials for each submodule (HTML workbooks, PDFs)
│       ├── exercises/     # Numbered exercise files
│       ├── notes/         # week-NN.md synthesis notes
│       └── artifacts/     # Published or in-progress work
└── resources/
    ├── reading-list.md
    ├── tools.md
    └── public-kgs.md
```

**Submodules vs. exercises — these are not the same thing.** Each module contains roughly 3 submodules, each covering a major topic area (approximately one week of content). Submodules are the conceptual groupings; exercises are the hands-on tasks. A single submodule may have 1-2 associated exercises, or none if it is reading-heavy. Submodule materials (interactive workbooks, reading companions, synthesis HTMLs) live in `submodules/` and are named `M-S-topic-name.ext` where M = module number and S = submodule number (e.g. `1-2-sparql-basics.html`). See SYLLABUS.md for the topic each submodule covers.

**Module READMEs follow the Module 1 template exactly.** Same sections, same order: scope → reading → exercises → primary project → pain points → deliverables → notes → checklist → "when you're done" test → navigation footer. When asked to create or update a module README, mirror Module 1's structure.

## Naming conventions

| Type | Pattern | Example |
|---|---|---|
| Turtle data files | lowercase, hyphens, version if applicable | `resume-001.ttl`, `naruto-ontology-1.0.0.ttl` |
| SPARQL queries | numbered + descriptive | `q01-all-jobs-chronological.rq` |
| Notes | week-based | `week-01.md`, `week-02.md` |
| Blog post drafts | dated slug | `2026-06-22-lpg-vs-rdf-resume-graphs.md` |
| Diagrams | lowercase, hyphens | `module-2-class-hierarchy.svg` |
| Ontology namespaces | one per project | `https://sensemaking-ai.com/ns/naruto#` |
| Submodule materials | `M-S-topic-name.ext` | `1-2-sparql-basics.html`, `1-1-reading-companion.pdf` |

## Turtle / RDF conventions

- **Always Turtle** unless format-specific work requires N-Triples or JSON-LD.
- **Standard prefix block at the top of every file:**
  ```turtle
  @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
  @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
  @prefix owl: <http://www.w3.org/2002/07/owl#> .
  @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
  @prefix dcterms: <http://purl.org/dc/terms/> .
  @prefix foaf: <http://xmlns.com/foaf/0.1/> .
  @prefix schema: <https://schema.org/> .
  @prefix skos: <http://www.w3.org/2004/02/skos/core#> .
  ```
  Add project-specific prefixes after these.
- **Reuse before defining.** Always check if `foaf:`, `schema:`, `skos:`, `dcterms:`, or `prov:` has an appropriate term before creating a new one in the custom namespace.
- **Comment headers** on every Turtle file: title, purpose, date, author, license.
- **Validate with SHACL** where shapes exist for the data.

## SPARQL conventions

- **Always include PREFIX declarations** matching the project's standard prefix block.
- **SPARQL keywords in uppercase** (`SELECT`, `WHERE`, `FILTER`, `OPTIONAL`).
- **One query per `.rq` file** unless the file is explicitly a multi-query examples document.
- **Comment block at the top of each query** describing the question being asked.
- **Match query style to DuCharme's examples** when in doubt — that's the canonical reference.

## Module-by-module content guidance

### When working on Module 1 (Foundations)
- Primary project: Resume Graph Explorer RDF slice (because ESCO/SKOS is real semantic web interop)
- Secondary: Naruto Graph Turtle slice
- Keep examples runnable on Wikidata when possible (no setup friction)
- **Submodule 1.1** — RDF as a data model: triples, URIs, literals, serialization formats, RDF vs LPG *(materials exist)*
- **Submodule 1.2** — SPARQL basics: SELECT, ASK, CONSTRUCT, DESCRIBE; querying Wikidata and local Fuseki
- **Submodule 1.3** — Vocabulary landscape and primary project: FOAF, Dublin Core, SKOS, schema.org; Resume Graph RDF slice

### When working on Module 2 (Modeling)
- Primary project: Naruto ontology v1.0
- The Naruto domain is the *primary* canvas because its categorical structure (ranks, villages, jutsu, arcs) is unusually rich
- Optional secondary: career narrative ontology for Resume Graph
- All ontologies must include REUSE.md documenting which external vocabularies are used
- **Submodule 2.1** — RDFS: subclass, subproperty, domain, range; class hierarchy basics
- **Submodule 2.2** — OWL: classes, individuals, object/datatype properties, restrictions, OWL profiles
- **Submodule 2.3** — Ontology design practice: Protégé workflow, design decisions, Naruto ontology primary project

### When working on Module 3 (Reasoning)
- Primary project A: Naruto reification (Itachi's revealed-late backstory is the canonical teaching example for contested provenance)
- Primary project B: Resume skill inference (where OWL property characteristics shine)
- This is the hardest module; pacing materials should be calmer, more deliberate
- **Submodule 3.1** — Inferencing: RDFS and OWL reasoning, running HermiT in Protégé
- **Submodule 3.2** — Reification: four approaches (classical, n-ary, named graphs, RDF-star), PROV-O; Naruto project
- **Submodule 3.3** — SHACL and vocabulary alignment: constraint shapes, owl:sameAs vs skos:exactMatch; Resume skill inference

### When working on Module 4 (Shipping)
- Capstone unifies TwinKit Semantic v2.0 framework + Naruto Knowledge Graph as demo dataset
- Deploys to either HuggingFace Spaces or Dagny's existing EC2 infrastructure (alongside Uptime Kuma)
- Eval honesty matters — document where hybrid retrieval is *worse* than vector-only, not just where it's better
- **Submodule 4.1** — SPARQL UPDATE: INSERT, DELETE, CONSTRUCT-into-graph, transactional considerations
- **Submodule 4.2** — Federation and deployment: SERVICE keyword, triplestore options, versioning, EC2 setup
- **Submodule 4.3** — LLM + KG integration: GraphRAG patterns, hybrid retrieval, TwinKit Semantic capstone

## Publishing workflow

Three platforms with distinct roles:

| Platform | Role | Voice |
|---|---|---|
| **GitHub (this repo)** | Canonical record; commits dated; the "official" version | Direct, technical, structured |
| **LinkedIn** | Twice-weekly broadcast; one short insight + one artifact post per week | Concise, hooks first, white space heavy |
| **sensemaking-ai.com** | End-of-module long-form analysis | Cog-sci flavored, deeper, voicier |
| **barbhs.com** | Occasional musings and explorations | Most personal; the working notebook |

When drafting content, ask which platform it's destined for and match voice accordingly. A LinkedIn post and a sensemaking-ai.com essay covering the same material should read differently.

## PROGRESS.md update protocol

Update PROGRESS.md weekly. Always:

1. **Add a new activity log entry at the top** (most recent first — never append to the bottom).
2. **Check off completed checkboxes** in the relevant module section.
3. **Update the "Currently" and "Last updated" fields** at the top.
4. **If an artifact shipped this week,** add it to the "Artifacts produced" section with a link.
5. **If something stalled,** add a note to "Pauses and detours" — honesty beats fake-perfect progress.

Don't rewrite or remove old entries. The cumulative log is the value.

## What this project does NOT do

- **Does not claim a credential not earned.** No KGC badge, no W3C affiliation, no "certified" anything except what's documented in Dagny's public credentials.
- **Does not use AI-generated content without disclosure.** Claude (or other AI) assistance is normal and welcome; this CLAUDE.md exists because of it. But content drafted with AI should not be presented as written from scratch alone. Generally, the artifacts here are AI-assisted but Dagny-authored — i.e., she reviews, edits, and stands behind every published piece.
- **Does not gloss over the technology's pain points.** Every module surfaces what's hard about the semantic web stack. That honesty is a core feature.
- **Does not pretend to be a team.** Solo practitioner, publishing openly under brand. The brand framing is honest positioning, not corporate cosplay.
- **Does not delete the redos.** When an ontology design fails and gets replaced, document the failure rather than overwriting silently. The wrong turns are part of the published value.

## Useful context links

When working on technical content, these are the canonical references:

- Allemang, Hendler & Gandon — *Semantic Web for the Working Ontologist* (3rd ed.) — [workingontologist.org](https://workingontologist.org/)
- DuCharme — *Learning SPARQL* — [learningsparql.com](https://www.learningsparql.com/) · [bobdc.com](https://www.bobdc.com/blog/)
- Hogan et al. — *Knowledge Graphs* (open access) — [kgbook.org](https://kgbook.org/)
- W3C specs — see [resources/reading-list.md](./resources/reading-list.md)
- Naruto Network Graph (existing project) — [docs.barbhs.com/naruto-network-graph](https://docs.barbhs.com/naruto-network-graph/)

When working on the Naruto domain specifically, defer to existing project conventions documented in the Naruto Network Graph repo. Character names, arc names, and relationship types should match what's already canonical in that project.

## When you (Claude) are unsure

Three fallbacks, in order:

1. **Match existing patterns in the repo.** If Module 1's README has a structure, follow it for Module 2.
2. **Ask before inventing conventions.** New decisions get explicitly approved by Dagny, not auto-applied from defaults.
3. **Err on the side of less.** Cleaner, shorter, more direct beats comprehensive but bloated. This is a learning artifact, not a textbook.
