# Reading list

> The annotated bibliography for the Sensemaking Semantic Web curriculum. Books, papers, W3C specs, and active practitioner voices. Organized by role, with one or two sentences of context per entry.

**Last updated:** Pre-launch, 5/23/26 · Companion files: [tools.md](./tools.md) · [public-kgs.md](./public-kgs.md)

---

## Contents

- [Required books](#required-books)
- [Open-access books](#open-access-books)
- [W3C specifications](#w3c-specifications)
- [Key papers](#key-papers)
- [Practitioner voices](#practitioner-voices)
- [Reading order by module](#reading-order-by-module)

---

## Required books

The curriculum repeatedly points to these. Acquire at least the first one before Module 1.

### Allemang, Hendler & Gandon — *Semantic Web for the Working Ontologist* (3rd ed., ACM Books, 2020)

The canonical practitioner text. Allemang has spent two decades helping enterprises deploy this stack; the book is shaped by what he's seen go wrong. The 3rd edition was substantially updated for the modern KG era.

- Companion site: [workingontologist.org](https://workingontologist.org/)
- Datasets and queries: [data.world/swwo](https://data.world/swwo)

If I only buy one book, I may buy this one.

### DuCharme — *Learning SPARQL* (2nd ed., O'Reilly, 2013)

Slightly older but the conceptual content has not aged. DuCharme writes with unusual clarity for a technical book. The companion site provides every example as downloadable files so I can practice in my own SPARQL client.

- Examples & sample data: [learningsparql.com](https://www.learningsparql.com/)
- Author's active blog (still excellent): [bobdc.com/blog](https://www.bobdc.com/blog/)

The blog is worth following independently — DuCharme posts thoughtful pieces on SPARQL patterns and the LLM + KG intersection.

---

## Open-access books

These are free, high-quality, and worth bookmarking even if not exactly read cover-to-cover.

### Hogan, Blomqvist, Cochez, d'Amato et al. — *Knowledge Graphs* (Synthesis Lectures, Springer, 2021)

Eighteen of the world's top KG researchers, single coherent treatment. Excellent companion to Allemang because it covers property graphs and embedding-based methods alongside the semantic web stack — giving us a unified vocabulary across both traditions.

- HTML book: [kgbook.org](https://kgbook.org/)
- arXiv version: [arxiv.org/abs/2003.02320](https://arxiv.org/abs/2003.02320)

Used for Module 1 (sections 3-4), Module 2 (section 5), Module 3 (section 6), and optionally Module 4 (sections 7-10).

### Heath & Bizer — *Linked Data: Evolving the Web into a Global Data Space*

Shorter than the others. The four Linked Data principles, URI design considerations, and the history of how the linked-data vision developed. Read once for context; I may not return to it constantly.

- Full online version: [linkeddatabook.com/editions/1.0](http://linkeddatabook.com/editions/1.0/)

### Labra Gayo, Prud'hommeaux, Boneva & Kontokostas — *Validating RDF Data* (2018)

The open-access book on SHACL and ShEx. Useful when Module 3's SHACL work gets serious. Both validation languages are covered; SHACL is what the curriculum uses.

- Online: [book.validatingrdf.com](http://book.validatingrdf.com/)

---

## W3C specifications

The W3C specs are surprisingly readable — don't skip them just because they're specs. The Primers are deliberately written for newcomers; the spec documents themselves are reference material.

### RDF foundations

- [RDF 1.1 Primer](https://www.w3.org/TR/rdf11-primer/) — read in Module 1
- [RDF 1.1 Concepts](https://www.w3.org/TR/rdf11-concepts/) — reference
- [Turtle](https://www.w3.org/TR/turtle/) — skim Module 1, reference thereafter
- [JSON-LD 1.1](https://www.w3.org/TR/json-ld11/) — for when I need web-developer-friendly RDF

### Querying

- [SPARQL 1.1 Query](https://www.w3.org/TR/sparql11-query/) — the main query spec
- [SPARQL 1.1 Update](https://www.w3.org/TR/sparql11-update/) — Module 4
- [SPARQL 1.1 Federation](https://www.w3.org/TR/sparql11-federated-query/) — Module 4

### Schemas and ontologies

- [RDF Schema (RDFS)](https://www.w3.org/TR/rdf-schema/) — Module 1
- [OWL 2 Primer](https://www.w3.org/TR/owl2-primer/) — Module 2 required reading
- [OWL 2 Overview](https://www.w3.org/TR/owl2-overview/) — orientation across the spec set
- [OWL 2 Profiles](https://www.w3.org/TR/owl2-profiles/) — defines DL, EL, QL, RL; optional in Module 3

### Constraints and provenance

- [SHACL](https://www.w3.org/TR/shacl/) — Module 3 required reading (abstract + Core Constraint Components at minimum)
- [PROV-O](https://www.w3.org/TR/prov-o/) — provenance ontology; Module 3 reification work

### Vocabularies I'll reuse

- [SKOS Primer](https://www.w3.org/TR/skos-primer/) — concept schemes; how ESCO is structured
- [SKOS Reference](https://www.w3.org/TR/skos-reference/)
- [schema.org](https://schema.org/) — used throughout; not technically W3C but adjacent

---

## Key papers

Worth reading for context on the modern KG + LLM intersection.

### Edge, Trinh, Cheng, Bradley, Chao, Mody, Truitt, Larson — *From Local to Global: A Graph RAG Approach to Query-Focused Summarization* (Microsoft, 2024)

The canonical reference for the GraphRAG pattern: build a knowledge graph from text, summarize communities, use both for retrieval. Important reading before Module 4's capstone.

- arXiv: [arxiv.org/abs/2404.16130](https://arxiv.org/abs/2404.16130)
- Project page: [microsoft.com/en-us/research/project/graphrag](https://www.microsoft.com/en-us/research/project/graphrag/)
- Code: [github.com/microsoft/graphrag](https://github.com/microsoft/graphrag)

### Berners-Lee — Linked Data design note

The original four-rule articulation of Linked Data principles from 2006. One page. Worth reading once for historical context.

- [w3.org/DesignIssues/LinkedData](https://www.w3.org/DesignIssues/LinkedData.html)

### Berners-Lee, Hendler & Lassila — *The Semantic Web* (Scientific American, May 2001)

The original vision article. Now mostly of historical interest, but useful for understanding the gap between what was promised and what materialized. Helps to sound senior when discussing why the field hasn't conquered the web the way it was supposed to.

---

## Practitioner voices

The semantic web field is small enough that following a handful of practitioners gives good coverage of what's happening.

### Bob DuCharme

Author of *Learning SPARQL*. Active blog with consistently thoughtful posts on SPARQL patterns, KG + LLM integration, and the practical mechanics of working with this stack.

- [bobdc.com/blog](https://www.bobdc.com/blog/)

### Dean Allemang

Co-author of *Semantic Web for the Working Ontologist*. Co-maintains the Financial Industry Business Ontology (FIBO). Writes on LinkedIn and at [workingontologist.org](https://workingontologist.org/).

### Juan Sequeda

Chief Scientist at data.world. Writes accessibly about the LLM + KG intersection. Particularly interesting work on benchmarking LLM accuracy with vs. without knowledge graph augmentation.

- Look for him on LinkedIn and the data.world blog
- The "data.world Chatbot Q&A benchmark" is worth searching for

### Kurt Cagle

Opinionated, prolific, occasionally Forbes. Useful for the take-the-temperature-of-the-field perspective.

---

## Reading order by module

### Pre-week

- Hogan et al. — sections 1-2 (vocabulary calibration only; don't try to read the whole thing)

### Module 1 — Foundations

**Required:**
- Allemang et al. — Chapters 1-3
- W3C RDF 1.1 Primer
- W3C Turtle spec (skim §1-3)
- DuCharme — Chapters 1-2

**Optional:**
- Hogan et al. — Sections 3-4
- Berners-Lee Linked Data design note

### Module 2 — Modeling

**Required:**
- Allemang et al. — Chapters 6-8
- W3C OWL 2 Primer
- Hogan et al. — Section 5

**Optional:**
- Ontology Design Patterns portal (selected patterns)
- Pizza Tutorial (do once)
- DuCharme — Chapters 3-4

### Module 3 — Reasoning at the edge ★

**Required:**
- Allemang et al. — Chapters 9-13
- W3C SHACL spec — abstract + Core Constraint Components
- Hogan et al. — Section 6

**Optional:**
- *Validating RDF Data* (Labra Gayo et al.) — open access
- W3C OWL 2 Profiles
- DuCharme — Chapter 5

### Module 4 — Shipping

**Required:**
- Allemang et al. — Chapters 14-15
- DuCharme — Chapters 5-6
- Microsoft GraphRAG paper (Edge et al., 2024)
- W3C SPARQL 1.1 Update spec

**Optional:**
- Microsoft GraphRAG project page + GitHub
- Juan Sequeda's writing
- Hogan et al. — Sections 7-10

---

## Navigation

[Syllabus](../SYLLABUS.md) · [README](../README.md) · Resources: [tools.md](./tools.md) · [public-kgs.md](./public-kgs.md)
