# Module 4 — Shipping

> SPARQL UPDATE, federation, deployment, LLM + KG integration. The capstone that pulls everything together into a deployed system.

**Weeks:** 10-12
**Effort:** ~8-10 hours per week (heaviest module by hours)
**New ground:** Mixed — deployment patterns are new; the LLM+KG integration builds on existing TwinKit work

---

## What you'll come away with

By the end of this module, you can:

- Write SPARQL UPDATE queries with awareness of transactional limits
- Deploy a triplestore to production infrastructure (alongside your existing EC2 services)
- Build hybrid retrieval that combines vector similarity with graph traversal
- Honestly evaluate where graph augmentation helps RAG and where it doesn't
- Articulate the practical considerations of running a knowledge graph in an enterprise context

The **deployment test** for this module: is the Naruto KG Explorer publicly accessible and queryable by anyone with a browser? Would you confidently take on a 4-week paid consulting engagement to advise a team on adopting knowledge graphs? Yes/no on both is your credential test for the whole curriculum.

---

## Required reading

| Source | Chapters / sections | Time |
|---|---|---|
| Allemang, Hendler & Gandon — *Semantic Web for the Working Ontologist* | Ch 14-15 | ~4 hours |
| DuCharme — *Learning SPARQL* | Ch 5-6 (UPDATE, federation, applications) | ~3 hours |
| [Microsoft GraphRAG paper](https://arxiv.org/abs/2404.16130) | Edge et al., 2024 — full paper | ~2 hours |
| [W3C SPARQL 1.1 Update spec](https://www.w3.org/TR/sparql11-update/) | Reference | ~1 hour |

The GraphRAG paper is the most important new reading. Read it carefully — the capstone architecture borrows directly from its hybrid retrieval pattern, and your case study will compare against it.

## Optional deeper reading

- [Microsoft GraphRAG project page](https://www.microsoft.com/en-us/research/project/graphrag/) and [GitHub](https://github.com/microsoft/graphrag) — see the working code, not just the paper.
- Juan Sequeda on the LLM + KG intersection — search LinkedIn and the data.world blog. His benchmark work on LLM accuracy with/without KG augmentation is especially relevant.
- Hogan et al. — Sections 7-10 (inductive knowledge, creation, quality, refinement). Worth skimming for the production-deployment considerations.
- [DuCharme's blog](https://www.bobdc.com/blog/) — recent posts on KG + LLM integration are directly applicable.

---

## Exercises

### Exercise 4.1 — Deploy a triplestore on EC2 *(3-4 hours)*

You already run EC2 infrastructure for your portfolio (Uptime Kuma, the apps registry, systemd + nginx pattern). Add a triplestore alongside.

**Recommended choice: Oxigraph** for first deployment (single Rust binary, simple ops). If you want the more standard option, Fuseki works but requires a JVM and verbose systemd config.

Steps:
1. Install Oxigraph from the GitHub releases page or via `cargo install`.
2. Add a systemd service for it (model after your existing service files).
3. Configure nginx to proxy a subdomain (e.g., `sparql.barbhs.com`) to the Oxigraph port with appropriate CORS headers for browser access.
4. Add the service to Uptime Kuma monitoring.
5. Document the deployment in `docs/triplestore-deployment.md` — this becomes part of the portfolio infrastructure case study.

Notes go in `notes/week-10-deployment.md`. Capture: what surprised you about the install, how the ops profile compares to your existing services.

### Exercise 4.2 — Federation experiment *(2 hours)*

From your deployed triplestore, run a federated query against Wikidata using `SERVICE`. Try retrieving information about a public figure (use your father's published patents as a real example, or Adrian Tchaikovsky's books — anything in Wikidata with structured metadata) and join with local data.

Note:
- The latency of federated queries (usually 2-10x slower than local)
- The failure modes when Wikidata is slow or rate-limits
- What happens to your query if Wikidata returns an unexpected schema change

Document findings in `notes/week-10-federation.md`. This becomes context for the "federation is powerful and slow" point in your case study.

### Exercise 4.3 — TwinKit Semantic v2.0 *(12-15 hours)* — **capstone**

See [Capstone](#capstone-twinkit-semantic-v20--naruto-knowledge-graph-as-demo) below.

---

## Capstone: TwinKit Semantic v2.0 + Naruto Knowledge Graph as demo

The capstone pulls everything together. Your `TwinKit` framework currently builds RAG-powered digital twins using ChromaDB. Add a semantic layer: an ontology describing the structure of a knowledge domain, with a SPARQL endpoint for graph queries, and hybrid retrieval that combines vector similarity with graph traversal.

### Two birds, one stone strategy

**TwinKit Semantic** is the framework — useful for consulting positioning, applicable to any domain.

**Naruto Knowledge Graph** (your ontology from Module 2 + reified assertions from Module 3) is the demonstration dataset — public-friendly, clickable, shareable.

One unified architecture supporting both. The Naruto demo is what people click on; the framework is what the case study describes.

### Steps

1. **Use your deployed triplestore** from Exercise 4.1 to host the production data.

2. **Load `naruto-ontology-1.0.0.ttl`** (from Module 2) as the demonstration domain ontology. Load Module 3 reified assertions as data. Verify it queries correctly.

3. **Build a parallel ingestion pipeline.** Existing TwinKit ingests markdown into ChromaDB. Add a parallel pipeline that produces RDF triples from the same source, using:
   - Regex-based extraction for structured fields (dates, names from known patterns)
   - LLM-assisted extraction for entities and relationships in prose (use LiteLLM since TwinKit already supports it)

4. **Expose a SPARQL endpoint.** Public, read-only, CORS configured. Document in the deployment notes.

5. **Build a public Naruto KG Explorer demo.** A simple Gradio (your existing comfort zone) or D3.js app where users can:
   - Ask natural-language questions (e.g., *"Who are Itachi's known masters?"*)
   - See SPARQL queries generated and results returned
   - Explore character networks with the ontology layered over the co-appearance graph
   - View the WebVOWL ontology visualization inline

6. **Augment retrieval (the technically rigorous part).** Add a graph-traversal step to the RAG pipeline:
   - Given a user query, identify entities mentioned (LLM call)
   - Run a SPARQL query to find related entities through the ontology (1-2 hops)
   - Bias ChromaDB retrieval toward chunks mentioning those entities
   - Compose the final context window from both sources

   This is the hybrid pattern Microsoft GraphRAG and others have shown to outperform pure vector retrieval on multi-hop questions.

7. **Eval before and after — honestly.** Pick 20 questions where the answer requires multi-hop reasoning (e.g., *"Which characters across all three arcs share a sensei lineage with Naruto?"*). Measure:
   - Baseline (vector only)
   - Hybrid (vector + graph)
   - Score on accuracy, relevance, latency

   Document results honestly, including cases where the hybrid is *worse*. Cases where graph augmentation helps and where it doesn't are equally interesting findings.

8. **Write the case study.** *"Hybrid semantic + vector retrieval: an honest evaluation, using Naruto."* Architecture diagram, eval results, code links, deployment notes. The Naruto domain makes the case study more accessible and shareable than a corporate example would.

9. **Update TwinKit README.** Position: *"Build RAG-powered digital twins with optional semantic layer."* Show the architecture diagram. Link to the case study and the live Naruto demo. Tag v2.0 release.

### What you'll feel

The deployment work is mostly muscle memory if you've shipped to EC2 before — modest cognitive load, high satisfaction when it works. The ingestion pipeline is where it gets interesting: LLM-assisted extraction is fragile in subtle ways, and you'll discover that the Naruto domain has edge cases (transliterated names, fan-translated terms) that didn't matter for the co-appearance graph but matter now.

The eval phase is where intellectual honesty matters most. The temptation will be to cherry-pick the cases where hybrid wins. Resist it — the honest evaluation is the differentiating artifact, and any client who'd hire you will respect it more than a polished but unbalanced case study.

---

## Pain points to surface

These are the deployment-and-production realities to name in the case study:

- **SPARQL UPDATE is not transactional in the SQL sense.** Most triplestores offer ACID at graph or statement level, but cross-graph multi-statement transactions are inconsistently supported. Plan accordingly.

- **Ontology versioning is unsolved.** Semver doesn't map cleanly. Adding a class is "minor"; adding a required restriction is "breaking." The OWL community uses `owl:versionInfo`, `owl:priorVersion`, `owl:backwardCompatibleWith` — but tooling for "what changed between two versions" is weak. Your professional opinion here will be valuable to clients.

- **Federation is powerful and slow.** `SERVICE` queries across multiple endpoints are powerful in theory; in practice, latency and inconsistent endpoint reliability make federated queries fragile. Most production systems materialize external data locally and refresh on a schedule. Knowing this saves clients real money.

- **The deployment market is small.** No Postgres-equivalent ubiquity. You're choosing among 5-7 viable triplestores, each with rough edges. The lack of a default is a real cost.

- **The semantic web's marketing problem.** The 2001 vision didn't materialize as sold. Successes have been narrower than advertised — life sciences (UMLS), finance (FIBO), government, schema.org for SEO, Wikidata. Knowing this history makes you sound senior. The LLM moment is causing a renaissance, but the renaissance is *graph-shaped*, not necessarily *RDF-shaped* — which puts your position (one foot in LPG, one foot in semantic web) unusually well.

- **Hybrid retrieval isn't always better.** This is the honest finding the case study should surface. Graph augmentation helps when the question genuinely requires multi-hop reasoning over structured relationships. It doesn't help — and sometimes hurts — when the question is about prose content that vector similarity already handles well. Knowing the difference is the consulting skill.

---

## Publishable deliverables

This module produces the highest-impact artifacts of the entire curriculum:

| Artifact | Where | Audience |
|---|---|---|
| TwinKit v2.0 released | GitHub (existing repo, new release) | Open-source community |
| Naruto KG Explorer (deployed) | HuggingFace Spaces or EC2 subdomain | Anyone curious — clickable from anywhere |
| Case study: *"Building a hybrid semantic + vector knowledge twin (with Naruto)"* | barbhs.com | Hiring managers, consulting prospects |
| Portfolio card: TwinKit Semantic with Naruto demo as the visual | barbhs.com homepage | Recruiters, clients |
| Triplestore deployment writeup | this repo + `docs.barbhs.com` | Infrastructure-curious peers |
| LinkedIn post: capstone announcement with eval results as the hook | LinkedIn | Network at large |
| Conference talk submission for 2027 venue (Connected Data World, SEMANTiCS, or AI/ML with RAG track) | external | Field-level visibility |
| Two weekly progress LinkedIn updates per week | LinkedIn | Network at large |

Every artifact in this list is durable — they keep paying off long after the curriculum ends.

---

## Synthesis notes

One paragraph per week. The last week's note doubles as material for the final reflection.

- [ ] `notes/week-10.md`
- [ ] `notes/week-11.md`
- [ ] `notes/week-12.md`

---

## Checklist

### Reading
- [ ] Allemang Ch 14-15
- [ ] DuCharme Ch 5-6
- [ ] Microsoft GraphRAG paper
- [ ] W3C SPARQL 1.1 Update spec

### Exercises
- [ ] 4.1 Triplestore deployed on EC2
- [ ] 4.2 Federation experiment against Wikidata
- [ ] 4.3 TwinKit Semantic v2.0 capstone

### Notes
- [ ] Week 10
- [ ] Week 11
- [ ] Week 12

### Deliverables
- [ ] TwinKit v2.0 released on GitHub
- [ ] Naruto KG Explorer deployed and publicly accessible
- [ ] Case study published on barbhs.com
- [ ] Portfolio card added
- [ ] Triplestore deployment writeup
- [ ] LinkedIn capstone announcement
- [ ] Conference talk abstract drafted (for future submission)
- [ ] Weekly LinkedIn updates × 6
- [ ] Final reflection added to `REFLECTIONS.md`

---

## When you're done

Take the deployment test:
1. Is the Naruto KG Explorer deployed and queryable by anyone with a browser?
2. Would you confidently take on a 4-week paid consulting engagement to advise a team on adopting knowledge graphs?

Yes/no on both is your credential test for the entire 12-week curriculum.

If yes to both: write the final reflection. The curriculum is complete. Schedule a celebration. Update your LinkedIn About section. Send the case study to anyone you've been talking to about consulting work.

If yes to deployment but not yet to the consulting engagement question: that's a normal endpoint. The credential test is genuinely high — many people complete the work but don't feel ready to charge for it yet. Continue working in the field; the confidence usually arrives within 1-3 months of additional applied work.

If the Naruto KG Explorer didn't deploy, document the blocker honestly in `REFLECTIONS.md`. A failed deployment with a documented reason is still a credible artifact — *"I built the framework but hit X infrastructure constraint"* is a senior engineer's voice, not a beginner's.

---

## Final navigation

⬅ [Module 3 — Reasoning](../03-reasoning/) · [Back to repo](../../README.md) · ➡ [Reflections](../../REFLECTIONS.md)
