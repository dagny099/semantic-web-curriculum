# Public knowledge graphs and SPARQL endpoints

> Public datasets, SPARQL endpoints, and reusable vocabularies referenced throughout the curriculum. Most of these I'll query rather than download.

**Last updated:** Pre-launch, 5/23/26 · Companion files: [reading-list.md](./reading-list.md) · [tools.md](./tools.md)

---

## Contents

- [Public SPARQL endpoints](#public-sparql-endpoints)
- [Reusable vocabularies](#reusable-vocabularies)
- [Linked Open Data Cloud](#linked-open-data-cloud)
- [Domain-specific knowledge graphs](#domain-specific-knowledge-graphs)
- [Practice query collections](#practice-query-collections)

---

## Public SPARQL endpoints

### Wikidata Query Service

The largest publicly-queryable knowledge graph. Crowd-curated; contains structured data about millions of entities — people, places, books, films, scientific concepts.

- Endpoint: [query.wikidata.org](https://query.wikidata.org/)
- SPARQL endpoint URL (for federation): `https://query.wikidata.org/sparql`
- Documentation: [wikidata.org/wiki/Wikidata:SPARQL_query_service](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service)

**Why it matters:** Wikidata is where to go to practice SPARQL on real data. The query helper UI is forgiving — start by reading and modifying example queries before writing from scratch.

**Used in:** Module 1 Exercise 1.1; Module 4 federation experiments.

**Practical tips:**
- Wikidata uses Q-numbers (`Q42` is Douglas Adams) and P-numbers (`P31` is "instance of"). Use the search box in the helper UI to find them.
- Add `SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }` to get readable labels.
- Wikidata is busy; complex queries can time out. Start narrow.

### DBpedia

Structured data extracted from Wikipedia. Predates Wikidata; still useful for English-language Wikipedia-anchored queries. Less curated than Wikidata but sometimes faster.

- Endpoint: [dbpedia.org/sparql](https://dbpedia.org/sparql)
- Documentation: [wiki.dbpedia.org](https://www.dbpedia.org/resources/sparql/)

### Bio2RDF

Life sciences linked data. Aggregates many biomedical sources (UniProt, KEGG, etc.) into a single SPARQL-queryable graph. Useful as an example of a successful domain-specific semantic web deployment.

- Endpoint and docs: [bio2rdf.org](https://bio2rdf.org/)

### LinkedGeoData

Geographic data from OpenStreetMap, available as Linked Data with a SPARQL endpoint.

- Endpoint: [linkedgeodata.org/sparql](http://linkedgeodata.org/sparql)

---

## Reusable vocabularies

When building an ontology, *reuse* before you define. These are the vocabularies the curriculum points to repeatedly.

### schema.org

Originally a SEO vocabulary backed by Google, Bing, Yahoo, and Yandex; now a general-purpose vocabulary for describing things on the web. Has classes for almost every common entity type: `Person`, `Organization`, `Event`, `Book`, `TVEpisode`, etc.

- Browse: [schema.org](https://schema.org/)
- For RDF use: namespace `https://schema.org/` (note: prefix `schema:` is conventional)

**Used in:** Modules 1, 2, 4 — used throughout for `Person`, `Organization`, `Event`, `DateTime`, `TVEpisode`.

### FOAF (Friend of a Friend)

The classic vocabulary for describing people and their connections. Older than schema.org but still standard for many use cases.

- Spec: [xmlns.com/foaf/spec](http://xmlns.com/foaf/spec/)
- Namespace: `http://xmlns.com/foaf/0.1/` (prefix `foaf:`)

**Used in:** Module 1 — `foaf:Person`, `foaf:knows`.

### Dublin Core

Bibliographic and resource description metadata: title, creator, date, publisher, source, etc. The vocabulary to reach for when describing *things about* a thing.

- Spec: [dublincore.org/specifications/dublin-core/dcmi-terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/)
- Namespace: `http://purl.org/dc/terms/` (prefix `dcterms:`)

**Used in:** Module 3 reification work — `dcterms:source`, `dcterms:date`.

### SKOS (Simple Knowledge Organization System)

The W3C vocabulary for *concept schemes* — controlled vocabularies, taxonomies, thesauri. The right choice when you have a hierarchy of concepts that isn't a strict class hierarchy.

- Primer: [w3.org/TR/skos-primer](https://www.w3.org/TR/skos-primer/)
- Reference: [w3.org/TR/skos-reference](https://www.w3.org/TR/skos-reference/)
- Namespace: `http://www.w3.org/2004/02/skos/core#` (prefix `skos:`)

**Used in:** Module 1 (ESCO skills), Module 3 (alignment via `skos:exactMatch`, `skos:closeMatch`).

### PROV-O

The W3C provenance ontology. For describing who, when, where, and how an assertion came to exist.

- Spec: [w3.org/TR/prov-o](https://www.w3.org/TR/prov-o/)
- Namespace: `http://www.w3.org/ns/prov#` (prefix `prov:`)

**Used in:** Module 3 reification project (Naruto provenance for contested canon).

### OWL Time

The W3C ontology for temporal concepts: instants, intervals, before/after relationships, durations.

- Spec: [w3.org/TR/owl-time](https://www.w3.org/TR/owl-time/)
- Namespace: `http://www.w3.org/2006/time#` (prefix `time:`)

**Used in:** Module 2 modeling — when modeling characters whose ninja rank changes across arcs.

---

## Linked Open Data Cloud

A visualization of how public RDF datasets link to each other. Useful for orientation: at a glance, we'll see the structure of the linked-data ecosystem and which datasets are central (Wikidata, DBpedia, schema.org).

- Diagram: [lod-cloud.net](https://lod-cloud.net/)

Worth bookmarking. Don't try to read it linearly; treat it as a map for when one needs to find a dataset in a particular domain.

---

## Domain-specific knowledge graphs

### ESCO (European Skills, Competences, Qualifications and Occupations)

A multilingual classification of occupations and skills published as Linked Open Data. Used in my Resume Graph Explorer project.

- Main site: [esco.ec.europa.eu](https://esco.ec.europa.eu/)
- SPARQL access: via download — ESCO is published as RDF for local loading rather than as a public SPARQL endpoint
- Why this matters: ESCO concepts are `skos:Concept` instances. When I connect a `Role` to an ESCO skill, I'm connecting to a node that already has `skos:broader`, `skos:related`, multilingual labels, and structured occupational hierarchies. This is where RDF's interop story shines.

**Used in:** Module 1 (Resume Graph RDF slice), Module 3 (skill inference).

### FIBO (Financial Industry Business Ontology)

Dean Allemang co-maintains FIBO. It's an example of a serious, production-grade enterprise ontology — useful to browse for the rigor of its modeling and the discipline of its documentation.

- Main: [spec.edmcouncil.org/fibo](https://spec.edmcouncil.org/fibo/)
- Browse one module's documentation in Module 2.

### UMLS (Unified Medical Language System)

The medical semantic web's anchor. Aggregates ~200 biomedical vocabularies. Requires registration to access. Mentioned here as context for the life sciences as the most successful semantic web deployment domain.

- Main: [nlm.nih.gov/research/umls](https://www.nlm.nih.gov/research/umls/index.html)

### Getty Vocabularies

Art and architecture vocabularies as Linked Open Data. The Art and Architecture Thesaurus (AAT), Union List of Artist Names (ULAN), Thesaurus of Geographic Names (TGN).

- Main: [vocab.getty.edu](http://vocab.getty.edu/)
- SPARQL: [vocab.getty.edu/sparql](http://vocab.getty.edu/sparql)

### GeoNames

Geographic database with SPARQL access via various mirrors.

- Main: [geonames.org](http://www.geonames.org/)
- RDF dumps: [geonames.org/ontology](http://www.geonames.org/ontology/documentation.html)

---

## Practice query collections

When I want to learn SPARQL by reading rather than writing, these are the best sources of high-quality example queries.

### Wikidata Examples gallery

Hundreds of example queries spanning every domain Wikidata covers. Each is well-commented and explains the SPARQL technique it demonstrates.

- [wikidata.org/wiki/Wikidata:SPARQL_query_service/queries/examples](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/queries/examples)

Starting points particularly useful for this curriculum:
- "Books and authors" patterns — relevant to bibliographic modeling
- "Genealogy" patterns — relevant to family relationships in the Naruto graph
- "People grouped by occupation" — relevant to Resume Graph patterns

### DuCharme's *Learning SPARQL* examples

Every example from the book is available as downloadable Turtle and SPARQL files. Run them locally in Fuseki.

- [learningsparql.com](https://www.learningsparql.com/)

### Allemang *Working Ontologist* datasets

The companion datasets and queries for the textbook. Hosted on data.world.

- [data.world/swwo](https://data.world/swwo)

---

## A note on endpoint reliability

Public SPARQL endpoints come and go. Wikidata is reliable; DBpedia is usually reliable; smaller endpoints sometimes go offline. If I build something that depends on a public endpoint, plan for it to fail occasionally.

The Module 4 federation experiment surfaces this explicitly: federated queries are powerful and slow, and production systems typically materialize external data locally on a refresh schedule rather than relying on live federation.

---

## Navigation

[Syllabus](../SYLLABUS.md) · [README](../README.md) · Resources: [reading-list.md](./reading-list.md) · [tools.md](./tools.md)
