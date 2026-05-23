# Tools

> Software I'll install and use across the Sensemaking Semantic Web curriculum. Organized by role, with install notes, when each is useful, and a comparison of triplestore options.

**Last updated:** Pre-launch, 5/23/26 · Companion files: [reading-list.md](./reading-list.md) · [public-kgs.md](./public-kgs.md)

---

## Contents

- [Triplestores: comparison and recommendation](#triplestores-comparison-and-recommendation)
- [Ontology editor](#ontology-editor)
- [Programmatic RDF in Python](#programmatic-rdf-in-python)
- [Ontology visualization](#ontology-visualization)
- [Reasoners](#reasoners)
- [What to install when](#what-to-install-when)

---

## Triplestores: comparison and recommendation

A triplestore is a database for RDF — the semantic web equivalent of Postgres or Neo4j. Unlike those, the triplestore market is sparse: no Postgres-equivalent default exists. We're choosing among 5-7 viable options, each with rough edges.

### Comparison

| Triplestore | Type | License | Strength | Trade-off |
|---|---|---|---|---|
| **Apache Jena + Fuseki** | Open source | Apache 2.0 | The "standard" academic option. Java-based. Good SPARQL coverage. Active community. | Verbose ops. Java JVM dependency. Setup feels heavier than it should. |
| **Oxigraph** | Open source | Apache 2.0 / MIT | Lightweight Rust binary. Simple ops. Fast. Good SPARQL 1.1 coverage including UPDATE. | Smaller community than Jena. Newer; fewer Stack Overflow answers. |
| **GraphDB Free** | Commercial w/ free tier | Proprietary | Excellent reasoning support. Polished UI. Used by many production deployments. | Free tier has data-size limits. Closed source. |
| **Stardog** | Commercial w/ free tier | Proprietary | Strong reasoning, virtualization, polished tooling. | Free tier increasingly restricted. Closed source. |
| **Virtuoso** | Open source + commercial | GPL / proprietary | Powerful, mature. Powers DBpedia. | Feels ancient. Documentation is hard going. |
| **Blazegraph** | Open source | GPL | Powers Wikidata Query Service. Strong scaling. | Development stalled after Amazon acquired the team. |

### Recommendation for this curriculum

**Use Fuseki for local development** (Module 1 onward). It's the option that matches almost every tutorial we'll encounter, so when I hit issues, the existing answers will apply.

**Use Oxigraph for the deployed production triplestore** (Module 4 capstone). The single-binary Rust deployment is dramatically simpler than running a JVM. Once I'm past learning, I'll want ops simplicity.

Install Fuseki for the pre-week and try Oxigraph in Module 4.

### Apache Jena + Fuseki — install notes

**Requirements:** Java 11+ (Java 17 recommended).

```bash
# macOS, via Homebrew
brew install openjdk@17
brew install apache-jena-fuseki

# Linux, manual
# Download from https://jena.apache.org/download/
# Extract, then:
cd apache-jena-fuseki-X.X.X
./fuseki-server
```

Default port: `3030`. Browse to [`http://localhost:3030`](http://localhost:3030) to see the admin UI. Create a new dataset (in-memory is fine for the curriculum), load Turtle files, run SPARQL queries.

For persistent storage: use TDB2 backend instead of memory.

**Documentation:** [jena.apache.org](https://jena.apache.org/)

### Oxigraph — install notes

**Requirements:** None for the binary; Rust toolchain if building from source.

```bash
# macOS / Linux, via cargo
cargo install oxigraph_server

# Or download the binary from GitHub releases:
# https://github.com/oxigraph/oxigraph/releases

# Run
oxigraph_server --location /path/to/data --bind 0.0.0.0:7878
```

Default port: `7878`. Exposes a SPARQL endpoint at `/query` and `/update`.

**Documentation:** [github.com/oxigraph/oxigraph](https://github.com/oxigraph/oxigraph)

### GraphDB Free — install notes

Download from [ontotext.com/products/graphdb](https://www.ontotext.com/products/graphdb/). Requires registration. Desktop installer for macOS/Windows; deb/rpm/tar.gz for Linux. Web UI on port 7200 by default.

Worth installing if we want to see what a polished commercial triplestore experience looks like, or if I reach the reasoning-heavy parts of Module 3 and want better OWL inference support than Jena offers out of the box.

---

## Ontology editor

### Protégé

Stanford's open-source ontology editor. The de facto standard for OWL ontology design. Has been the standard for ~20 years; the UI shows its age but the functionality is comprehensive.

**Install:** Download from [protege.stanford.edu](https://protege.stanford.edu/). Desktop versions for macOS, Windows, Linux. Also a web version (WebProtégé) for collaborative editing, though desktop is what I'll use here.

**When to reach for it:**
- Module 2: building the Naruto ontology. The class hierarchy editor, property editors, and HermiT reasoner integration are all far easier than editing Turtle by hand for ontology design work.
- Module 3: watching a reasoner work. Protégé's Reasoner menu is the easiest place to see inference happen interactively.

**Practical tip:** Save in Turtle format (right-click the file → "Save as" → "Turtle"). The default RDF/XML serialization is unreadable.

---

## Programmatic RDF in Python

### rdflib

The standard Python library for RDF. Lets us build graphs in code, parse Turtle/JSON-LD/etc., run SPARQL queries against in-memory graphs, and serialize to various formats.

**Install:** `pip install rdflib` (also: `pip install rdflib-jsonld` for JSON-LD support).

**When to reach for it:**
- Module 3: skill inference notebook — programmatic SPARQL CONSTRUCT queries with conditional logic that's awkward in pure SPARQL.
- Module 4: TwinKit ingestion pipeline — parsing markdown into RDF triples, validating with SHACL via [pySHACL](https://github.com/RDFLib/pySHACL).

**Documentation:** [rdflib.readthedocs.io](https://rdflib.readthedocs.io/)

**Related libraries:**
- [pySHACL](https://github.com/RDFLib/pySHACL) — SHACL validation in Python
- [SPARQLWrapper](https://github.com/RDFLib/sparqlwrapper) — Python client for remote SPARQL endpoints (Wikidata, DBpedia)
- [owlrl](https://github.com/RDFLib/OWL-RL) — OWL 2 RL reasoning in Python

---

## Ontology visualization

### WebVOWL

Web-based visualization for OWL ontologies. Drag-and-drop our Turtle file in and get a node-link diagram with classes, properties, and instances. Excellent for screenshots in blog posts and README diagrams.

**Use:** [vowl.visualdataweb.org/webvowl.html](http://vowl.visualdataweb.org/webvowl.html)

No install required. Just upload the Turtle file or paste an ontology URL.

**Where it shows up in the curriculum:**
- Module 2: Naruto ontology — generate WebVOWL screenshots for the repo's `docs/` directory
- Module 4: TwinKit capstone — embed an interactive WebVOWL view in the Naruto KG Explorer demo

---

## Reasoners

### HermiT

The default OWL reasoner that ships with Protégé. Reasonably fast, supports OWL 2 DL fully. I won't typically install this separately — I'll use it through Protégé.

**When to reach for it:** Module 3, Exercise 3.1 — watching a reasoner work interactively in Protégé.

### Pellet (now openllet)

Alternative OWL reasoner, also DL. More aggressive incremental reasoning support than HermiT. Open source.

### ELK

Specialized reasoner for OWL 2 EL profile. Dramatically faster than HermiT or Pellet for large ontologies that fit within EL. Worth knowing about even if I don't use it — clients with large vocabularies will care about EL performance.

---

## What to install when

### Pre-week (this weekend)

- [ ] Apache Jena + Fuseki
- [ ] Protégé

Two installs. Verify both run. Don't try to do anything substantive with them yet.

### Module 1 (Weeks 1-3)

Using Fuseki and Protégé from pre-week. Add:

- [ ] rdflib (Python `pip install`)

### Module 2 (Weeks 4-6)

Spending most of the time in Protégé. Optionally:

- [ ] GraphDB Free — to compare against Jena for reasoning. Optional.

### Module 3 (Weeks 7-9)

- [ ] pySHACL (Python `pip install`)
- [ ] SPARQLWrapper (Python `pip install`) — for federated queries to Wikidata

### Module 4 (Weeks 10-12)

- [ ] Oxigraph (for EC2 deployment)
- [ ] Any LLM SDK I'm already using for TwinKit (OpenAI, Anthropic, LiteLLM)

---

## What this curriculum does *not* use

Tools I might expect to see but won't, with brief reasons:

- **Neo4j as the primary tool** — already in use elsewhere; this curriculum is about the *complement* to Neo4j, not a replacement. Module 1 explicitly compares the two.
- **AllegroGraph** — commercial; the free tier is limited enough that practical work runs into limits quickly.
- **Apache TinkerPop / Gremlin** — property-graph traversal language; not RDF. Out of scope.
- **Stardog Designer** — Stardog's GUI ontology editor. Nice but Protégé is the canonical tool and what most documentation references.

---

## Navigation

[Syllabus](../SYLLABUS.md) · [README](../README.md) · Resources: [reading-list.md](./reading-list.md) · [public-kgs.md](./public-kgs.md)
