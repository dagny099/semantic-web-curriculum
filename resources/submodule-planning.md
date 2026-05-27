# Sub-module planning — Sensemaking Semantic Web curriculum

> Planning doc for the original teaching content that will live alongside the
> existing module READMEs. Eleven candidate sub-modules across four modules,
> with web-search-grounded notes on what already exists and where original
> content adds value, three detailed outlines, and a rollout plan.

**Author:** Planning conversation, May 2026
**Status:** Plan — not yet content. No HTML produced. No prose drafted.

---

## Contents

- [Read of the brief](#read-of-the-brief)
- [Conventions for the sub-module pages](#conventions-for-the-sub-module-pages)
- [Sub-module breakdown across the four modules](#sub-module-breakdown-across-the-four-modules)
- [Module 1 detail and web-search findings](#module-1-detail-and-web-search-findings)
- [Module 2 detail and web-search findings](#module-2-detail-and-web-search-findings)
- [Module 3 detail and web-search findings](#module-3-detail-and-web-search-findings)
- [Module 4 detail and web-search findings](#module-4-detail-and-web-search-findings)
- [Three detailed outlines](#three-detailed-outlines)
- [Rollout plan](#rollout-plan)
- [Open questions](#open-questions)

---

## Read of the brief

The curriculum already has good operational scaffolding — syllabus, module READMEs, resource files, repo conventions. What it does not yet have is original teaching content in the curriculum's voice. The plan below proposes 11 sub-modules, 2–3 per module, that synthesize the canonical references rather than duplicate them, ground every page in a project that already exists, and surface the pain perspective the curriculum is honest about.

Three constraints shape the plan:

1. **The curriculum is being worked at the same time the content is being developed.** Sub-modules for Module 3 should not be drafted from secondhand summary. Plan them now, draft them as the curriculum reaches them.
2. **Five projects are available as worked-example anchors.** Resume Graph Explorer (Neo4j with ESCO/SKOS), Naruto Network Graph (87 characters, 3 arcs, hand-coded canonical relationships), Digital Twin ChromaDB (the pure-RAG version), Digital Twin Neo4j (the GraphRAG version in beta, with explicit hybrid scoring and an evaluation suite), and the memorial graph (not yet documented here). The Digital Twin GraphRAG version is the most consequential anchor — it means several Module 4 sub-modules can be grounded in working, deployed code rather than a future capstone.
3. **The canonical references are good.** Allemang/Hendler/Gandon, DuCharme, Hogan et al., the W3C specs. The sub-modules should not retell what these say. They should be the pages that synthesize across the canon, ground the abstractions in the curriculum's projects, and surface the pain points the textbooks tend to elide.

---

## Conventions for the sub-module pages

Each sub-module page should follow the same skeleton so the body of work hangs together:

1. **One-paragraph framing.** What the page is for. What it assumes the reader already knows.
2. **The conceptual move.** The single idea that, if it lands, makes the rest of the page easier.
3. **Walkthrough on a real example from the curriculum's projects.** Code, data, queries — not toy snippets.
4. **The pain perspective.** The honest tradeoffs the canonical references tend to underplay.
5. **Curated external resources.** Annotated, not link-dumped — what each is good for and where it falls short.
6. **What to do next.** The exercise or commit that operationalizes the page in the reader's own work.

Word count target: 1,800–2,500 words. Visuals: one diagram or comparison table per page minimum. Code samples: real, runnable, sourced from the projects. Interactive widgets: only where they teach something the prose can't (the RDF-vs-LPG comparison and the four-reification comparison are the strongest candidates).

---

## Sub-module breakdown across the four modules

| # | Sub-module | Module | Worked example | Pain point |
|---|---|---|---|---|
| 1.1 | RDF vs LPG side-by-side | Foundations | Same resume in Cypher and Turtle; ESCO/SKOS as the punchline | The URI tax — verbosity as the cost of global identity |
| 1.2 | Reading and writing Turtle fluently | Foundations | Naruto Chunin Exams `.ttl` walked line by line | Blank nodes break graph identity; four serializations exist because none is good enough |
| 1.3 | SPARQL: thinking in triple patterns | Foundations | Three questions in SPARQL, Cypher, and SQL side by side | The looseness that makes SPARQL powerful also makes silent-failure queries easy |
| 2.1 | RDFS, OWL, and knowing when to stop | Modeling | Does NinjaRank need OWL DL? Walk through what RDFS, RL, DL each buy | Most production ontologies use EL or QL; the DL temptation costs scalability |
| 2.2 | Reuse before defining | Modeling | The Naruto REUSE.md; Digital Twin's 167 entity types as an emergent vocabulary | Reuse improves interop and inflates dependency surface; no clean rule, only judgment |
| 2.3 | Modeling judgment: classes, instances, properties, time | Modeling | The Naruto rank-change problem; time-indexed situations | The redos are the work; when "true" is unwieldy |
| 3.1 | Open-world reasoning: the mental shift | Reasoning | A Naruto query that returns surprising results because of OWA; SHACL closes the loop | The shift from "this is broken" to "this is honest" is the ontologist inflection |
| 3.2 | The four reification approaches | Reasoning | Itachi's contested motivations expressed all four ways | Verbosity multiplies; tooling support varies; the right choice depends on what's downstream |
| 3.3 | Where OWL reasoners beat LLMs (and where they lose) | Reasoning | Resume Graph skill inference: formal rules vs LLM prompt; honest agreement/disagreement table | Hybrid approaches require knowing what each can prove; both fail in characteristic ways |
| 4.1 | Choosing and deploying a triplestore | Shipping | Oxigraph on EC2 alongside Uptime Kuma; the actual `sparql.barbhs.com` deployment | No Postgres-equivalent; the deployment market is small and rough |
| 4.2 | Hybrid retrieval: when graph augmentation helps RAG | Shipping | The Digital Twin GraphRAG eval — vector-only vs hybrid with the existing 0.85 / 0.08 / 0.05 / 0.02 scoring | Hybrid isn't free; the wins are real but narrower than the marketing claims |

Eleven sub-modules. Within the 8–12 target. The Module 4 sub-modules are unusually well-grounded because the Digital Twin Neo4j version is already deployed and instrumented — these pages can show real numbers, not hypothetical ones.

---

## Module 1 detail and web-search findings

### 1.1 RDF vs LPG side-by-side

**Canonical references:** Allemang Ch 1–3 (the framing chapters). Hogan et al. §3 for the broader data-model landscape.

**The conceptual move:** RDF and LPG model the same kinds of facts using different primitives. RDF makes predicates global URIs; LPG makes relationships local labels with their own properties. The consequences cascade — RDF wins on cross-system interoperability and reasoning; LPG wins on developer ergonomics and path-traversal performance. Neither is a strict superset; the choice is real.

**Worked example:** One resume modeled both ways. In Cypher, `(p:Person)-[r:WORKED_AT {startDate: ...}]->(c:Company)`. In Turtle, the same fact requires either an `Event` class or RDF-star to attach the date. Then the ESCO query — in Cypher you join through a foreign-key-style `ESCO_CODE` property; in SPARQL you follow `skos:broader` and `skos:related` directly into the existing ESCO graph as first-class triples. The ESCO query is where RDF's interop story has actual teeth.

**Pain point:** The URI tax. Compare the line count for the same data in both. RDF is more verbose because every term is globally identifiable. That precision is overhead in some contexts and essential in others. The page should make the reader feel both — annoyance at the verbosity, then the unlock of joining an external vocabulary without writing glue code.

**Web-search findings:**

The existing comparisons fall into three camps. Vendor pieces from Neo4j and similar lean toward "property graphs are easier" — useful for understanding the case against RDF but not honest about where RDF wins. Counter-pieces from semantic-web partisans lean the other way. The most balanced recent treatment is the [arXiv paper by Hartig et al.](https://arxiv.org/pdf/2204.06277) on user-study comparison of edge-labelled and property graphs — worth citing as the academic anchor. Kurt Cagle's [RDF 1.2 vs Neo4j/OpenCypher](https://ontologist.substack.com/p/rdf-12-vs-neo4jopencypher) is the most up-to-date practitioner take but is opinionated and should be cited, not paraphrased. Michael DeBellis's [Semantic Web vs Property Graphs](https://www.michaeldebellis.com/post/owlvspropgraphs) is balanced and concrete; worth linking. The gap in existing content: nobody walks through the same domain in both stacks with side-by-side queries on real data including ESCO. That's the contribution.

No interactive widget is needed for this page. A two-column diagram showing the same data in both representations, plus a query-comparison table, is enough.

### 1.2 Reading and writing Turtle fluently

**Canonical references:** W3C RDF 1.1 Primer; W3C Turtle spec (skim sections 1–3); Allemang Ch 2.

**The conceptual move:** Turtle is RDF wearing comfortable clothing. Every Turtle file is a set of triples; the shorthand syntax (`;`, `,`, `a`, prefixes) just makes them readable. Understanding the anatomy of a Turtle file means understanding how to construct any RDF data.

**Worked example:** The Naruto Chunin Exams `.ttl` slice walked through line by line. Prefix block first — why these prefixes, where they come from, why the order matters. Then a single character (Naruto) modeled in full, showing `a foaf:Person`, `schema:memberOf :Konoha`, `naruto:rank :Genin`, with the `;` and `,` patterns. Then the language-tagged literal (`"Naruto Uzumaki"@en`), the datatype literal (`"1999-09-21"^^xsd:date`), and one blank node showing where the anonymity is useful and where it leaks identity across files.

**Pain point:** Two named pains. First, blank nodes break graph identity across systems — useful for transient grouping, dangerous for entities you'll need to reference later. Second, four serializations exist because none is good enough for everything. Show the same Naruto fact in N-Triples (verbose, debuggable), JSON-LD (web-developer-friendly, hard to read at scale), RDF/XML (legacy, painful), and Turtle (the working choice). The reader should leave knowing why Turtle won the curriculum's allegiance and what the alternatives are good for.

**Web-search findings:**

[RDF Playground](http://rdfplayground.dcc.uchile.cl/) is a real find — a web-based tool that takes Turtle, visualizes it as a graph, runs SPARQL queries against it, runs OWL 2 RL reasoning, and validates with SHACL. Embedding or linking RDF Playground at the bottom of the page gives readers a sandbox without setup. The associated [WWW 2023 paper](https://dl.acm.org/doi/fullHtml/10.1145/3543873.3587325) describes the design intent. Otherwise: the W3C Primer is canonical, and Maxime Lefrançois's [Writing Web data in RDF](https://www.emse.fr/~zimmermann/Teaching/SemWeb/Practice/WriteRDF/) tutorial is a solid alternative explainer. The gap in existing content: nobody walks through a pop-culture domain in Turtle in a way that lets the reader feel why the shorthand earns its keep over many entities. Naruto fills that gap.

Interactive widget candidate: a small embedded Turtle editor that renders the parsed triples below. This is what RDF Playground already does — link to it rather than rebuild.

### 1.3 SPARQL: thinking in triple patterns

**Canonical references:** DuCharme Ch 1–2; W3C SPARQL 1.1 Query (reference). Apache Jena's [Basic Patterns tutorial](https://jena.apache.org/tutorials/sparql_basic_patterns.html) for the canonical worked walkthrough.

**The conceptual move:** SQL describes operations on tables. SPARQL describes shapes the data must take. A SPARQL query is a graph pattern with variables in any of the three positions; the engine finds every binding of those variables that satisfies the pattern. This is closer to logic programming than to relational queries — and the shift in mental model is the page's whole job.

**Worked example:** Three questions, three queries each, three engines. (1) "All books by Adrian Tchaikovsky" — Wikidata SPARQL, Cypher (if we had a books KG), SQL (if we had a relational books table). (2) "Skills that Barbara has demonstrated for more than two years" — Resume Graph in SPARQL and Cypher. (3) "All characters who fought Naruto in any arc" — Naruto graph in SPARQL and Cypher. The point is the conceptual move from "describe operations on rows" to "describe shapes of relationships."

**Pain point:** SPARQL's openness is its strength and its trap. Because the data model is open-world, a query that returns zero results doesn't tell you whether your pattern is wrong or whether the data simply doesn't contain what you asked for. SQL would have thrown an error or returned `NULL`; SPARQL silently returns the empty set. This is the failure mode the page should name explicitly so the reader stops being surprised by it.

**Web-search findings:**

The Veronahe Substack piece [SPARQL for SQL Developers](https://veronahe.substack.com/p/sparql-for-sql-developers-a-translation) is a useful translation guide but reads as LLM-assisted and shouldn't be the lead reference. The [Apache Jena Basic Patterns tutorial](https://jena.apache.org/tutorials/sparql_basic_patterns.html) is the canonical worked example and should be linked. The Stardog [Learn SPARQL in Studio](https://docs.stardog.com/getting-started-series/getting-started-4) page is good for the "triple pattern as building block" framing. The gap in existing content: nobody walks the same three questions through SPARQL, Cypher, and SQL side by side. That's the contribution. Skip the Cypher comparison on a question Cypher can't answer well — the ESCO question is the obvious one — and the asymmetry teaches more than parity would.

No interactive widget. The three-by-three query grid is enough.

---

## Module 2 detail and web-search findings

### 2.1 RDFS, OWL, and knowing when to stop

**Canonical references:** Allemang Ch 6–8; W3C OWL 2 Primer; W3C OWL 2 Profiles document; Krötzsch's "OWL 2 Profiles: An Introduction to Lightweight Ontology Languages" chapter (the academic anchor).

**The conceptual move:** RDFS gives you typed nodes and typed edges. OWL adds class definitions, property characteristics, and equivalences. The five OWL profiles exist because the full OWL DL gets computationally expensive — EL, QL, and RL trade expressivity for tractability. Most production ontologies live in EL or QL; tutorials live in DL. Knowing which layer your problem actually needs is the modeling skill.

**Worked example:** The Naruto ontology decision. Does `NinjaRank` need OWL DL? Walk through it three times — RDFS-only (just subclasses), OWL 2 RL (with property characteristics like `senseiOf` being inverse of `studentOf`), OWL 2 DL (with disjoint classes and qualified cardinality restrictions). Show what each layer infers automatically; show what each layer costs at query time. The reader should leave with the heuristic: start at RDFS, escalate only when you have a query that needs the inference the next layer adds.

**Pain point:** Tractability tradeoffs. The temptation to over-formalize is real and seductive. Adding `owl:TransitiveProperty` to `partOf` looks free until your queries time out on a large graph because the reasoner is computing transitive closure. The page should make the costs concrete with timings.

**Web-search findings:**

The [W3C OWL 2 Profiles document](https://www.w3.org/TR/owl2-profiles/) is the canonical reference but reads as a spec — not a teaching document. The Krötzsch chapter on [OWL 2 Profiles: An Introduction to Lightweight Ontology Languages](https://link.springer.com/chapter/10.1007/978-3-642-33158-9_4) is the best academic treatment but is dense. The [OWL 2 New Features and Rationale](https://www.w3.org/TR/owl2-new-features/) document has a usefully terse section on profile selection — worth excerpting. The gap: nobody walks a single ontology through escalating layers on a concrete domain showing what changes at each step. The Naruto rank hierarchy is unusually well-suited because the categorical structure is clean.

No widget. A profile-comparison table and a "what gets inferred at each layer" diagram do the work.

### 2.2 Reuse before defining

**Canonical references:** Allemang Ch 5 (vocabulary integration); the W3C [Principles of Good Practice for Managing RDF Vocabularies](https://www.w3.org/2006/07/SWD/Vocab/principles); Heath & Bizer's *Linked Data* book for the principles framing.

**The conceptual move:** Defining a new term is technically free and operationally expensive. Every custom term is a future maintenance burden, breaks interoperability, and signals to other ontologists that you weren't paying attention. The discipline is to evaluate `foaf:`, `schema:`, `skos:`, `dcterms:`, `prov:`, `org:`, and `time:` before reaching for the custom namespace — and to document every reuse decision so future-you can audit the choices.

**Worked example:** The Naruto ontology REUSE.md walkthrough. `schema:Person` for Character — why this over `foaf:Person` (richer subclass structure, better tooling for `Person → Organization` relationships). `schema:Organization` for Village. Why `dcterms:source` for assertion sources but a custom `naruto:revealedIn` for canon-revelation events (no standard term for "the work in which a fact was revealed within a narrative"). And the Digital Twin's 167 entity nodes as a parallel case — Skills, Methods, Technologies, Concepts emerged organically and are essentially an undocumented vocabulary; what would a REUSE.md for the Digital Twin look like?

**Pain point:** Reuse improves interop and inflates dependency surface. If `schema.org` deprecates a class, your ontology breaks. If FOAF goes unmaintained (it has been, slowly), your ontology inherits the staleness. The page should name this honestly and give a heuristic — reuse liberally for well-established stable terms (Dublin Core, FOAF, schema.org, PROV-O); be cautious about newer or domain-specific vocabularies where long-term stability is unclear.

**Web-search findings:**

The most useful existing piece is Kurt Cagle's [What Do You Need to Create a Useful Ontology?](https://ontologist.substack.com/p/what-do-you-need-to-create-a-useful) — it covers the reuse discipline well and is recent. The W3C [Principles of Good Practice for Managing RDF Vocabularies](https://www.w3.org/2006/07/SWD/Vocab/principles) is the formal anchor but old. The [SIOC reusing-vocabularies document](https://www.w3.org/submissions/2007/SUBM-sioc-related-20070612/) is a good example of what a REUSE.md looks like in practice for an ontology with real reuse. The gap: nobody has a worked decision-tree for "given this candidate term, which existing vocabulary should I check, in what order, and what's a good reason to reject each." That's the contribution — a decision flow grounded in the Naruto and Digital Twin cases.

Widget candidate: a small decision-tree visualization (clickable, not just static) of "should I reuse or define?" — but only if it teaches something the prose can't. Otherwise a flow diagram is enough.

### 2.3 Modeling judgment: classes, instances, properties, time

**Canonical references:** Allemang Ch 7–8; the Ontology Design Patterns portal (TimeIndexedSituation, NaryRelation patterns); FIBO as a reference exemplar for what mature modeling looks like.

**The conceptual move:** The hardest decisions in ontology design aren't formal — they're judgment calls about what to model as a class versus an instance versus a property. "Software Engineer" can be a class (whose instances are individual engineers), an instance (of `JobTitle`), or a property value (someone's `hasRole`). Each choice constrains what you can ask later. The page is about how to make the choice deliberately and how to recover when you got it wrong.

**Worked example:** The Naruto rank-change problem. Naruto starts as a Genin and (eventually) becomes Hokage. How do you model that? Option 1: rank is a property whose value changes — but then you lose history. Option 2: rank is a class hierarchy — but instances can't change class without being re-declared. Option 3: time-indexed situation — `:Naruto :hasRankAt [:atTime :ChuninExamsArc ; :rankValue :Genin]`. Each option is correct for some downstream query and wrong for others. The page walks the actual redo trail.

**Pain point:** Modeling fights itself. The redos are the work, not a sign of failure. The page should make this normal — show the failed first attempt at the Naruto rank hierarchy, what query broke it, what the second attempt looked like, why the third attempt finally worked. Most ontology engineering pages hide the redo trail; this one shouldn't.

**Web-search findings:**

The Ontology Design Patterns portal at [ontologydesignpatterns.org](http://ontologydesignpatterns.org/) is the canonical reference but the site is hard to navigate. The specific patterns to surface are `TimeIndexedSituation` and `N-aryRelation`. [FIBO's modeling documentation](https://spec.edmcouncil.org/fibo/) is the production exemplar — pointing readers there for "what mature modeling looks like" is high-value even though FIBO is overwhelming on first contact. The Pizza Tutorial gets cited too often; the Naruto domain has the same teaching properties without the eye-roll factor. The gap: real public ontology pages rarely show the redos. This one will.

No widget. A versioned diff of the Naruto rank hierarchy (v1 → v2 → v3) is the visual.

---

## Module 3 detail and web-search findings

These three sub-modules should be planned now and drafted later — the curriculum's own Module 3 should be roughly half-complete before original teaching material on it can be written without secondhand summary.

### 3.1 Open-world reasoning: the mental shift

**Canonical references:** Allemang Ch 9–10 (especially the OWA framing); Hogan §6; W3C SHACL spec for the closed-world counterpoint.

**The conceptual move:** "Not stated" does not mean "false." A SPARQL query that asks "how many characters have no listed children" returns zero — not because every character has children, but because the open-world model doesn't license the inference from absence. SHACL gives you closed-world constraints when application logic needs them; the rest of the time you live with openness and design queries accordingly.

**Worked example:** A Naruto query that returns surprising results. The exact query — "characters with no jutsu" — should be the punchline, with the explanation walked through carefully. Then SHACL closing the loop: declaring a shape that says "every Ninja must have at least one Jutsu" and showing the validation report on the data, which is the closed-world question SPARQL refused to answer.

**Pain point:** The shift from "this is broken" to "this is honest" is the genuine ontologist inflection point. The page should name it and not over-promise that it's an easy shift. Many engineers never make it.

**Web-search findings to do later.** Defer search until the sub-module is drafted.

### 3.2 The four reification approaches: choosing intentionally

**Canonical references:** Allemang Ch 11–12; W3C [RDF-star Use Cases and Requirements](https://w3c.github.io/rdf-star/UCR/rdf-star-ucr.html); the Ontotext [GraphDB Users Ask: Is RDF-Star The Best Choice For Reification?](https://www.ontotext.com/blog/graphdb-users-ask-is-rdf-star-best-choice-for-reification/) piece.

**The conceptual move:** Reification is the problem of talking about a triple — attaching provenance, time, confidence, source. Four approaches exist because none is dominant: classical RDF reification (verbose, universally supported, slow), n-ary relations (clean modeling, awkward queries), named graphs (great for grouping, weak semantics for individual triple metadata), RDF-star (the newest, most ergonomic, not universally supported). The page makes the choice intentional rather than default.

**Worked example:** Itachi's contested motivations expressed all four ways, with the SPARQL query for each. PROV-O for source attribution. A decision matrix at the end mapping requirements (universal support, inference compatibility, query ergonomics, storage cost) to recommended approach.

**Pain point:** Verbosity multiplies. Tooling support varies. The right choice depends on what you need downstream — inference, performance, interop. The page should make the tradeoffs concrete with code, not abstractions.

**Web-search findings preview:** Ontotext's piece is the best single existing reference and is recent. The W3C RDF-star UCR is the canonical use-case catalog. The [Easy and complex: new perspectives for metadata modeling using RDF-star and Named Graphs](https://www.researchgate.net/publication/365849862) paper by Knapp and Kahl is worth citing for the academic anchor. The gap: nobody has worked one example all four ways end-to-end including the SPARQL retrieval. That's the contribution.

Widget candidate: a tabbed code viewer that shows the same fact in all four reification styles with synchronized highlighting of the assertion vs the metadata. This is the strongest widget candidate in the whole curriculum.

### 3.3 Where OWL reasoners beat LLMs (and where they lose)

**Canonical references:** Hogan §6 for formal reasoning; the GraphRAG paper (Edge et al., 2024) for the LLM-augmented retrieval baseline; Juan Sequeda's data.world benchmark work on LLM accuracy with and without KG augmentation; the recent [RAG vs GraphRAG: A Systematic Evaluation](https://arxiv.org/html/2502.11371v3) paper.

**The conceptual move:** Formal reasoning is deterministic, explainable, and brittle. LLM reasoning is flexible, fast on prose, and confidently wrong in predictable ways. The page makes the comparison concrete with a real task — skill inference from resumes — and shows where each approach is the right tool and where each fails.

**Worked example:** Resume Graph skill inference. Five formal rules expressed as SPARQL CONSTRUCT queries (held a role > 2 years in ESCO category X → demonstrated cluster X; held roles in multiple companies in same cluster → industry experience). Five LLM prompts asking the same questions. Side-by-side agreement/disagreement table across 10 profiles. Honest documentation of where formal rules surfaced inferences the LLM missed, where the LLM caught implicit skills the rules couldn't reach, and where both were wrong.

**Pain point:** Hybrid approaches require knowing what each can prove. Most published comparisons cherry-pick wins for one side. This page should resist that — the honest evaluation is the differentiating artifact.

**Web-search findings to do later.** Defer until drafting.

---

## Module 4 detail and web-search findings

### 4.1 Choosing and deploying a triplestore

**Canonical references:** the curriculum's own [`tools.md`](../resources/tools.md); vendor documentation for Oxigraph, Fuseki, GraphDB; the [Apache Jena documentation](https://jena.apache.org/) for the academic-standard option.

**The conceptual move:** Triplestores are not Postgres. There is no default. The choice depends on what your application actually needs — reasoning support, query throughput, ops simplicity, ecosystem. Five viable options exist, each with rough edges. The page walks the decision and the actual deployment.

**Worked example:** The deployment of Oxigraph on EC2 alongside Uptime Kuma. Config files, systemd unit, nginx proxy with CORS, monitoring hookup. Documenting what surprised — what worked first try and what required debugging. The actual `sparql.barbhs.com` deployment as the artifact.

**Pain point:** No Postgres-equivalent. The deployment market is small and rough. Knowing the landscape and being willing to choose carefully is a senior skill in this space.

**Web-search findings:** Light research only — the curriculum already covers tools.md comprehensively. Worth citing the [Oxigraph GitHub](https://github.com/oxigraph/oxigraph) release notes for the current state and the [Apache Jena Fuseki documentation](https://jena.apache.org/documentation/fuseki2/) for the alternative.

No widget. A decision matrix and the actual config files.

### 4.2 Hybrid retrieval: when graph augmentation helps RAG (and when it doesn't)

This sub-module is unusually well-grounded because the Digital Twin Neo4j version is already deployed with an explicit hybrid scoring formula and an evaluation harness. The page can show real numbers.

**Canonical references:** Edge et al. (2024) — [Microsoft GraphRAG paper](https://arxiv.org/abs/2404.16130); Sarmah et al. (2024) — [HybridRAG paper](https://arxiv.org/abs/2408.04948); the 2026 [RAG vs GraphRAG systematic evaluation](https://arxiv.org/html/2502.11371v3) paper.

**The conceptual move:** Vector retrieval finds semantically similar text. Graph traversal finds structurally related entities. Hybrid combines them. The wins come on questions that genuinely require multi-hop structured reasoning — the losses come on questions where vector similarity already had the right answer and the graph adds noise. Knowing which is which is the practitioner skill.

**Worked example:** The Digital Twin GraphRAG eval. The actual hybrid scoring formula — vector similarity (0.85) plus project link bonus (0.08) plus entity mention bonus (0.05) plus length bonus (0.02). Twenty evaluation questions across multi-hop categories. Side-by-side results from the existing ChromaDB pure-RAG and Neo4j GraphRAG implementations. Honest categorization — where hybrid won, where vector-only won, where both failed in interesting ways.

**Pain point:** Hybrid isn't free. Ingestion is more complex (entity extraction adds an LLM call per chunk). Latency increases. The wins are real but narrower than the marketing claims. The HybridRAG paper itself notes lower context precision because the combined context introduces noise — the page should cite this and reproduce the finding on the Digital Twin's actual data.

**Web-search findings:** Strong existing literature, all recent. The HybridRAG paper (Sarmah et al., 2024) is the closest published comparison to the Digital Twin architecture. The 2026 systematic evaluation paper has the most rigorous methodology. Sequeda's benchmark work is the practitioner-flavored counterpart. The gap: no published evaluation walks a single application through ChromaDB pure-RAG and Neo4j GraphRAG with a public scoring formula and honest documentation of where hybrid loses. That's the contribution — and it's already partially built.

Widget candidate: an interactive query explorer that lets the reader type a question and see (a) what ChromaDB retrieves, (b) what Neo4j GraphRAG retrieves, (c) the scored difference. If the Digital Twin admin interface already does this, the page can embed or link to a public sanitized version.

---

## Three detailed outlines

The three sub-modules below are the highest-impact candidates to draft first.

### Detailed outline: 1.1 RDF vs LPG side-by-side

**Word count target:** 2,200 words.

**Section structure:**

1. **Why this comparison matters** (~150 words). The single most-asked question when someone with Neo4j experience encounters RDF. Sets up the rest of the page.
2. **The two data models, side by side** (~350 words). Triple model vs node-plus-property-plus-edge model. The fundamental primitives. A simple example (Alice knows Bob) in both, then the same example with metadata on the relationship (Alice knows Bob since 2020) to show where the models diverge.
3. **The same resume in both stacks** (~500 words). Walk through one real resume modeled in Cypher and Turtle. Show the line count difference. Show the prefix block discipline in Turtle. Show how date properties work in each.
4. **Three queries, three answers** (~400 words). The chronological-jobs query (Cypher wins). The skills-with-ESCO-codes query (SPARQL wins — by a lot, this is the punchline). The consecutive-job-transitions query (a wash, but for instructive reasons).
5. **The URI tax** (~250 words). Why RDF is verbose. What it buys. When you want the tax and when you resent it.
6. **The choice in practice** (~250 words). Heuristics: if your application is path-heavy and contained, LPG. If your data needs to integrate with external vocabularies (ESCO, FIBO, schema.org for SEO), RDF. If you're being honest, you'll have applications where both make sense and the choice is about team skill and operational profile.
7. **What to do next** (~150 words). Exercise: pick one of your own datasets and write the same three queries in both. Notice which felt natural.
8. **Curated resources** (~150 words). 4–5 annotated links with what each is good for.

**Diagrams:**

- The two data models side by side as a labeled comparison (Alice/Bob example in triples and in nodes-edges).
- A query-comparison table: each of the three queries in Cypher and SPARQL, with the "winner" annotated.
- Optional: a small Sankey-style diagram showing how the ESCO query in SPARQL just follows links into the existing ESCO graph, vs the Cypher version that has to materialize the ESCO data in Neo4j first.

**Code samples:**

- One resume in Turtle (~30 lines).
- The same resume as Cypher CREATE statements (~25 lines).
- Three SPARQL queries with results.
- Three Cypher queries with results.

**Interactive widget:** None. The visual comparison table does the work.

**Pain point voice:** The page should make the reader feel the verbosity of RDF, then feel the unlock of ESCO interop, in that order. Don't apologize for the verbosity. Don't oversell the interop.

---

### Detailed outline: 2.2 Reuse before defining

**Word count target:** 2,000 words.

**Section structure:**

1. **Why reuse is the discipline** (~200 words). The cost of every custom term. Maintenance, interoperability, the signal it sends. The frame: reuse is the default; defining is the exception that requires justification.
2. **The vocabularies worth knowing on first contact** (~400 words). Brief profile of each — `foaf:` (people, social), `schema:` (general-purpose, SEO-anchored), `skos:` (concept schemes, taxonomies), `dcterms:` (bibliographic metadata), `prov:` (provenance), `org:` (organizational structures), `time:` (temporal). What each is for, what each is bad at, current maintenance state.
3. **The decision flow** (~350 words). Given a candidate term I want to model, what's the order of operations? (1) Search the major reusable vocabularies. (2) Check ontology search engines (LOV, Linked Open Vocabularies). (3) Check domain-specific vocabularies if applicable. (4) Only then define a new term. With an explicit checklist.
4. **The Naruto REUSE.md walkthrough** (~400 words). Concrete decisions. `schema:Person` for Character (why not `foaf:Person` — better tooling, richer subclass structure). `schema:Organization` for Village. `dcterms:source` for canon-source attribution. The custom decisions: `naruto:Jutsu`, `naruto:Arc`, `naruto:senseiOf`. The rationale for each custom term — what existed and why it didn't fit.
5. **The Digital Twin's emerging vocabulary** (~300 words). The 167 canonical entity nodes (Skills, Methods, Technologies, Concepts) as a case study in *implicit* vocabulary that should probably become explicit. What would a REUSE.md for the Digital Twin look like? Where does it map to ESCO/SKOS? Where would it need custom terms?
6. **The interop-vs-stability tradeoff** (~200 words). Reuse improves interop. It also inflates dependency surface. FOAF maintenance is unclear. Schema.org changes faster than it admits. The page should be honest that reuse isn't always free.
7. **What to do next** (~150 words). Exercise: write a REUSE.md for one of your own ontologies, or for the Digital Twin entity types. Commit it.

**Diagrams:**

- A decision-tree flow diagram of "should I reuse or define?" — five or six branching decision points.
- A mapping table: Naruto custom terms → external vocabulary near-matches (or "no near-match").
- Optional: a Venn-style diagram of what `foaf:`, `schema:`, and `dcterms:` overlap on for the Person class case.

**Code samples:**

- An excerpt of the Naruto REUSE.md showing the decision log format.
- A small Turtle snippet showing the difference between `naruto:Character a schema:Person` (reuse) and `naruto:Character a naruto:Character` (custom-only, the wrong default).
- A SPARQL query that benefits from the schema.org reuse — querying across Naruto and external schema.org data without glue code.

**Interactive widget:** Optional decision-tree widget that lets the reader walk a candidate term through the decision flow with their own answers. Only build if the flow has more than five decision points; otherwise a static diagram is enough.

**Pain point voice:** Honest about reuse costs. Don't oversell. The page should leave the reader equipped to evaluate vocabularies, not deferring to authority.

---

### Detailed outline: 4.2 Hybrid retrieval: when graph augmentation helps RAG

**Word count target:** 2,500 words. Longer because it's the case-study sub-module and includes eval results.

**Section structure:**

1. **The hybrid retrieval landscape** (~300 words). Pure vector RAG. GraphRAG. HybridRAG. Where each pattern came from, what claims each makes. The Microsoft GraphRAG paper, HybridRAG (Sarmah et al.), and the 2026 systematic eval. Set up the rest of the page as an honest evaluation rather than another endorsement.
2. **The Digital Twin GraphRAG architecture** (~400 words). The actual hybrid scoring formula in production. Vector similarity at 0.85. Project-link bonus at 0.08. Entity-mention bonus at 0.05. Section-length bonus at 0.02. Why this weighting — why vector dominates and graph signals are tiebreakers. The 167-entity vocabulary and the `MENTIONS` and `DESCRIBED_IN` relationship types. Tier gating for the public/personal/inner_circle sensitivity layers.
3. **The evaluation harness** (~250 words). Twenty multi-hop questions across category types. What "multi-hop" means in this context. The evaluation metrics — faithfulness, answer relevancy, context precision, context recall. How the side-by-side ChromaDB-vs-Neo4j comparison is wired.
4. **Where hybrid won** (~400 words). Three case-study questions with both retrieval traces shown. The pattern: questions that genuinely require structured multi-entity reasoning. "What projects has Barbara worked on that involve both NLP and infrastructure deployment?" — the graph traversal surfaces project-entity links the vector retrieval missed.
5. **Where vector-only won** (~400 words). Three case-study questions where pure vector retrieval beat hybrid. The pattern: questions about prose content where the graph signals added noise rather than signal. "Describe Barbara's working philosophy" — vector found the philosophy document section directly; graph traversal pulled in adjacent project mentions that diluted the context.
6. **Where both failed** (~250 words). Two cases. Document the failure modes honestly. Don't claim a fix you don't have.
7. **What this means for client work** (~250 words). The consulting framing — not every application needs GraphRAG. The questions that benefit are specific. The cost (ingestion complexity, latency, ops surface) is real. Knowing when to recommend hybrid vs vector-only is the skill.
8. **What to do next** (~150 words). Pointer to the Digital Twin GraphRAG repo, the eval harness, and the public side-by-side admin tool if it gets sanitized for external view.
9. **Curated resources** (~200 words). Annotated links to the GraphRAG paper, HybridRAG paper, systematic eval paper, Sequeda's work, and the Digital Twin Neo4j README.

**Diagrams:**

- Architecture diagram showing the dual-pipeline ingestion (ChromaDB and Neo4j) and the hybrid scoring at retrieval time.
- A side-by-side trace diagram for one "hybrid won" case showing which sections each pipeline retrieved.
- A results-summary chart showing the 20 questions broken into win/loss/tie categories for the two approaches.

**Code samples:**

- The exact hybrid scoring SQL or Cypher (from the Digital Twin codebase).
- One example multi-hop SPARQL or Cypher graph-traversal query showing what the graph signal actually does.
- An excerpt of the eval harness configuration.

**Interactive widget:** The strongest widget candidate in the curriculum. An embedded query explorer where the reader types a question, sees the two retrieval traces, and sees the scored difference. If the Digital Twin admin interface already does this and can be sanitized for public access, this is the page that uses it. If not, a static walkthrough of three example queries is sufficient.

**Pain point voice:** Resist hybrid evangelism. The page is honest about narrow wins, real costs, and the cases where vector-only was the right answer. That honesty is the consulting positioning.

---

## Rollout plan

Eleven sub-modules at the page sizes above is roughly 22,000–25,000 words of original content. That's substantial — drafting all of it at production quality is a quarter of work on top of the curriculum itself. The rollout below respects that.

### Phase 1 — Now through end of Module 1 (Weeks 1–3 of curriculum)

Draft and publish two sub-modules. The reading and projects for Module 1 are the most directly grounded.

- **1.1 RDF vs LPG side-by-side.** Highest leverage. Gates everything else. Drafted alongside or before the existing Module 1 blog post on the same topic.
- **1.2 Reading and writing Turtle fluently.** Concrete, low-research, high-utility. The Naruto Chunin Exams slice from Exercise 1.4 is the artifact.

### Phase 2 — End of Module 1 through Module 2 (Weeks 3–6)

Draft three more. The Module 2 sub-modules can be drafted while modeling the Naruto ontology because the redos generate the teaching material.

- **1.3 SPARQL: thinking in triple patterns.** Finishes the Module 1 set.
- **2.1 RDFS, OWL, and knowing when to stop.** Drafted while making the actual profile choice for the Naruto ontology.
- **2.2 Reuse before defining.** Drafted alongside the Naruto REUSE.md, which is needed anyway. The Digital Twin extension section can be written separately.

### Phase 3 — Module 2 through early Module 3 (Weeks 6–8)

Draft 2.3 and plan 3.1–3.3 in detail.

- **2.3 Modeling judgment: classes, instances, properties, time.** Drafted when the redo trail on the Naruto ontology is complete enough to teach from.
- **3.1, 3.2, 3.3** detailed outlines (not full drafts).

### Phase 4 — Module 3 (Weeks 7–9)

Draft the three Module 3 sub-modules. These need real working understanding, so they should not be drafted before the curriculum's own Module 3 work begins.

- **3.1 Open-world reasoning.** Draft when the SHACL work is partway through.
- **3.2 The four reification approaches.** Draft during or after Exercise 3.2 (all four reification approaches). This is the strongest interactive-widget candidate.
- **3.3 Where OWL reasoners beat LLMs.** Draft after the skill-inference Jupyter notebook is complete. This is the blog-post-as-page; arguably the highest-impact sub-module for consulting positioning.

### Phase 5 — Module 4 (Weeks 10–12)

Draft 4.1 and 4.2 alongside the capstone work. 4.2 is unusually well-grounded because the Digital Twin GraphRAG version is already deployed.

- **4.1 Choosing and deploying a triplestore.** Draft during Exercise 4.1.
- **4.2 Hybrid retrieval.** Draft during the capstone eval. Use the actual Digital Twin numbers.

### Sequencing diagram (textual)

```
Curriculum  M1 ====M1=====| M2 ====M2=====| M3 ====M3=====| M4 ====M4=====|
            Wk 1   2   3    4    5    6    7    8    9    10   11   12

Sub-modules:
  1.1 ====|drafted by end of Wk 2
  1.2     ==|drafted by end of Wk 3
  1.3        ===|drafted by end of Wk 4
  2.1            ===|drafted by end of Wk 5
  2.2                ===|drafted by end of Wk 6
  2.3                    ====|drafted by end of Wk 7
  3.1                          ===|drafted during Wk 8
  3.2                              ====|drafted during Wk 9
  3.3                                  =====|drafted at end of M3
  4.1                                       ===|drafted during Wk 10
  4.2                                            =====|drafted during capstone
```

The pace averages one sub-module per week. Slower than that is fine; faster is probably unrealistic given the curriculum work itself is the primary deliverable.

### Stopping rules

- If sub-module drafting starts to slow curriculum progress more than 25%, stop drafting and let curriculum work catch up. The curriculum is the primary asset; the teaching pages are secondary value.
- If a sub-module reaches a third draft and still doesn't land, ship the rough version with a "rough draft, will revisit" banner. Don't let perfection block publication.
- 3.3 and 4.2 are the highest-leverage sub-modules for consulting positioning. If only six get drafted by end of curriculum, those two should be in the six.

---

## Open questions

A handful of decisions and inputs would tighten the plan. These don't block Phase 1, but answers will affect Phases 2–5.

1. **The memorial graph.** What it is, what data it contains, what its existing artifacts look like. The plan has no worked examples drawn from it — if it has rich reification or alignment material, it could be the anchor for 3.1 or 3.2 instead of (or alongside) Naruto.

2. **The "TwinKit" framing.** The syllabus and Module 4 README call the framework "TwinKit Semantic v2.0." The deployed Digital Twin Neo4j README presents the system under "Digital Twin: Barbara Hidalgo-Sotelo" — the framework name isn't surfaced publicly yet. Worth deciding before drafting 4.2: does the page introduce TwinKit as the framework and Digital Twin as its first user, or treat the Digital Twin as the leading artifact with no separate framework brand?

3. **Public vs sanitized eval data for 4.2.** The Digital Twin admin interface has a side-by-side ChromaDB-vs-Neo4j comparison tool. Can a sanitized public version be exposed? If yes, 4.2 gets the strongest interactive widget in the curriculum. If no, the page works as static traces.

4. **The "anchoring projects" balance.** The plan leans on Naruto for Modules 1–3 and Digital Twin for Module 4. Resume Graph anchors only 1.1 and 3.3. If Resume Graph should carry more weight (it has the strongest ESCO/SKOS interop story and the most direct consulting transfer), 2.3 and 4.2 could pivot to use it instead. Worth deciding before Phase 2.

5. **Voice spot-checks.** Some of the language in this plan ("the conceptual move," "the redos are the work," "honest about narrow wins") is an attempt at the curriculum's voice. Before drafting sub-module 1.1, worth a voice-and-conventions spot check — read aloud, mark where the voice is right and where it slips. A small voice guide for the sub-modules specifically (one page, a few do's and don'ts plus a couple of paragraph examples) would tighten everything that follows.

---

## What this plan is not

- It is not the content. No HTML, no extensive prose, no finished pages.
- It is not a commitment. Sub-modules can be cut or reordered as the curriculum work clarifies what's worth teaching.
- It is not exhaustive on web research. Heavier searches for Modules 3 and 4 should happen at drafting time, not now.
- It is not the right level of detail for the eight sub-modules outside the three detailed outlines. Drafting any of those will require its own outlining pass.

## What this plan is

- A working list of eleven sub-modules with concrete worked examples, canonical references, and pain-point angles for each.
- Web-search-grounded notes on what already exists and where original content adds value.
- Three detailed outlines for the highest-impact sub-modules to draft first.
- A rollout plan with honest sequencing.
- A short list of open questions whose answers would tighten Phases 2–5.
