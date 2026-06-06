# Module 3 — Reasoning at the edge ★

> Inference, reification, vocabulary alignment, SHACL validation. The conceptually hardest segment of the curriculum.

**Weeks:** 7-9
**Effort:** ~7-9 hours per week
**New ground:** Heavy — most material is genuinely new

★ This is the module where pacing matters most. Front-load the reading in Week 7 so Weeks 8-9 have time for the harder project work. If the syllabus is going to slip, this is where it will. Build a one-week buffer if you can.

---

## What you'll come away with

By the end of this module, you can:

- Run an OWL reasoner against an ontology and predict (most of) what it will infer
- Choose intentionally among the four reification approaches (classical, n-ary, named graphs, RDF-star) based on requirements
- Use SHACL to express closed-world constraints over an open-world data model
- Align overlapping vocabularies with the right level of equivalence (`owl:sameAs` vs `skos:exactMatch` vs `skos:closeMatch`)
- Articulate where formal reasoning beats LLM reasoning and where it loses — useful both technically and as consulting positioning

The **conceptual test** for this module: can you explain the four reification approaches, give an example use case for each, and defend the tradeoffs? If yes, reasoning landed.

---

## Required reading

| Source | Chapters / sections | Time |
|---|---|---|
| Allemang, Hendler & Gandon — *Semantic Web for the Working Ontologist* | Ch 9-13 | ~10 hours |
| [W3C SHACL spec](https://www.w3.org/TR/shacl/) | Abstract + §5 (Core Constraint Components) | ~2 hours |
| Hogan et al. — *Knowledge Graphs* | Section 6 (deductive knowledge) | ~3 hours |

Allemang Ch 9-13 is dense. Don't try to read all five chapters in one sitting — split across Week 7 and Week 8. The SHACL spec is reference material; read the abstract carefully, then skim §5 to know what constraint components exist.

## Optional deeper reading

- [*Validating RDF Data*](http://book.validatingrdf.com/) — Labra Gayo et al., 2018, open access. The book on SHACL and ShEx. Worth keeping open as a reference while you work.
- [W3C OWL 2 Profiles](https://www.w3.org/TR/owl2-profiles/) — defines DL, EL, QL, RL. Read each profile's introduction to know what gets traded.
- [W3C PROV-O](https://www.w3.org/TR/prov-o/) — the provenance ontology, needed for the reification project.
- DuCharme — Chapter 5 (advanced SPARQL features including `CONSTRUCT` for inference materialization).

---

## Exercises

### Exercise 3.1 — Watch a reasoner work *(1 hour)*

In Protégé, load your Naruto ontology from Module 2 (or the Pizza ontology if Naruto stalled). Activate the HermiT reasoner (Reasoner → Start reasoner). Then:

1. Declare `senseiOf` as a sub-property of `colleagueOf`.
2. Declare `colleagueOf` as `owl:SymmetricProperty`.
3. Add an assertion: `senseiOf(Jiraiya, Naruto)`.
4. Run the reasoner. Observe what gets inferred (Jiraiya is now a `colleagueOf` Naruto; symmetry means Naruto is also a `colleagueOf` Jiraiya).
5. Now declare something contradictory and watch the reasoner complain.

Notes go in `notes/week-07-reasoner.md`. Capture: which inferences were obvious, which were surprising, what the reasoner told you about contradiction.

### Exercise 3.2 — All four reification approaches *(3 hours)*

Pick one fact you'd want to attribute — for example, *"Itachi killed his clan under orders from Konoha leadership, revealed in manga chapter 401."* Express this fact in all four reification styles:

1. **Classical RDF reification** — `rdf:Statement` with `rdf:subject`, `rdf:predicate`, `rdf:object` plus annotation properties
2. **N-ary relation** — turn the killing event into an `Event` class instance with multiple properties
3. **Named graphs** — put the assertion in a named graph with metadata triples about the graph
4. **RDF-star** — annotate the triple directly using `<<>>` syntax

Save as four separate `.ttl` files in `exercises/3-2-reification/`. For each, write a SPARQL query that retrieves the fact along with its source (manga chapter). Compare verbosity, ergonomics, and how naturally each style queries.

This exercise is the foundation for the reification project below. Do it before starting Exercise 3.3.

### Exercise 3.3 — Naruto reification project *(8-10 hours)* — **primary project A**

See [Project hook A](#project-hook-a-reification-in-the-naruto-graph) below.

### Exercise 3.4 — Resume skill inference *(6-8 hours)* — **primary project B**

See [Project hook B](#project-hook-b-skill-inference-in-resume-graph-explorer) below.

Both projects are listed as primary because they exercise different reasoning skills. If you have to pick one due to time, **A** is the more memorable artifact; **B** has more direct consulting transfer value.

---

## Project hook A: Reification in the Naruto graph

The Naruto domain is unusually well-suited to reification work because so much of the canon is contested, fan-theorized, or revealed retroactively across the series. Different sources (manga vs. anime, databook vs. movie, fan-canon vs. official) disagree about character backstories, relationships, and motivations. Every assertion deserves a source.

### Goal

Take a slice of your Naruto ontology and add full provenance to every assertion: who claims this, in what source, when revealed, with what confidence.

### Steps

1. Pick a subset rich with contested or retroactively-revealed material. Itachi's true motivations (revealed late in the series, contradicting earlier appearances) is a perfect example — pick ~20-30 assertions across a few characters with this property.

2. Express each fact using one reification style. Recommend **named graphs + PROV-O** because PROV-O is a W3C standard and named graphs are well-supported across triplestores. If your stack supports RDF-star (Jena, Oxigraph, GraphDB do), RDF-star is also acceptable and produces more readable Turtle.

3. Annotate with:
   - `dcterms:source` — manga volume/chapter, anime episode, databook reference, fan wiki URL
   - `dcterms:date` — when revealed in the series timeline
   - `sensemaking:confidence` — custom property, values like `canonical-strong`, `canonical-disputed`, `anime-only`, `databook-only`, `fan-theory`

4. Write SPARQL queries that:
   - Retrieve only manga-canonical facts above confidence threshold
   - Identify facts that are anime-only (filler) vs. manga-canonical
   - Find characters whose backstory was retroactively changed (assertions with conflicting sources)
   - Build a "reliability timeline" for a single character (Itachi is the canonical example)

5. Publish to `artifacts/naruto-reification/` with:
   - `data.ttl` (or `data.trig` if named graphs)
   - `queries/` — the SPARQL above
   - `README.md` — design decisions, reification approach chosen, why

6. **Reflect (500 words):** would Neo4j with edge properties have been easier? Where does RDF win? Where does it lose? Save as `REFLECTION.md` in the artifact folder. This becomes blog post material.

---

## Project hook B: Skill inference in Resume Graph Explorer

Use OWL property characteristics + SPARQL CONSTRUCT queries to infer skills that aren't explicitly stated.

### Goal

Build a Jupyter notebook that demonstrates skill inference end-to-end: take real resume data, apply formal reasoning rules, surface inferred skills that weren't on the resume, and compare against what an LLM would surface on the same input.

### Example rules

- If a person held a `Role` whose ESCO concept has `skos:related` to skill X, infer that person has *some exposure* to X.
- If a person held a role for more than two years, escalate the exposure to *demonstrated*.
- If two skills are both required by many of a person's roles, mark them as *core competencies*.
- If a person held roles in two different companies in the same ESCO occupation cluster, mark them as *industry-experienced* in that cluster.

### Steps

1. Take 5-10 resume profiles from Resume Graph Explorer, converted to RDF using the ontology from Module 1.
2. Express the inference rules as SPARQL CONSTRUCT queries that produce new triples (`sensemaking:hasInferredSkill`, `sensemaking:hasCompetency`, etc.).
3. Apply the rules to each profile. Capture the inferred skills.
4. For each profile, also run an LLM prompt that asks the same question: *"What skills would you infer from this resume that aren't explicitly listed?"*
5. Compare the two approaches:
   - Where do formal rules and LLM inference agree?
   - Where do they disagree?
   - Where is each one *wrong*?
   - What does each get fundamentally right that the other can't?

6. Publish to `artifacts/skill-inference/` as a Jupyter notebook with the comparison results.

This is the project that connects directly to your existing `narrative synthesizer` work. The honest comparison between formal reasoning and LLM reasoning is the kind of consulting-positioning artifact that opens doors.

---

## Pain points to surface

These are the tensions to name in the blog posts and synthesis notes:

- **Open-world reasoning bugs.** "Person X has no listed children" does not mean "Person X has zero children." This causes real bugs in applications written by developers who didn't learn the distinction. Either layer SHACL on top to enforce closed-world for application logic, or accept the openness and design queries accordingly. There's no third option that hides the choice from you.

- **`owl:sameAs` is a hammer.** If you assert `:Dagny owl:sameAs :Barbara`, the reasoner treats them as the same entity for *all* properties. Properties meaningful only for the consulting persona merge with properties meaningful only for the personal persona. Use `skos:exactMatch` or domain-specific equivalence when you mean "these refer to the same thing without collapsing all attributes."

- **Inference materialization tradeoffs.** Compute inferred triples once and store them (fast queries, stale on update)? Or compute at query time (always fresh, slow)? Both are wrong sometimes. Knowing which lever to pull is a senior skill.

- **Reification verbosity is a real cost.** Source attribution multiplies storage and complicates every query. This is one of the most-cited reasons people pick LPG over RDF. Neo4j lets you put properties on edges natively, with no reification gymnastics.

- **The "open world" you'll learn to want.** After all these complaints, you'll have moments where open-world reasoning is exactly right — you genuinely don't know whether a fact holds and you want the system to behave that way. Treat this as the elegance the model is offering, not a bug. The shift from "this is broken" to "this is honest" is the inflection point of becoming a real ontologist.

---

## Publishable deliverables

| Artifact | Where | Audience |
|---|---|---|
| Reified Naruto KG with provenance | this repo (`modules/03-reasoning/artifacts/naruto-reification/`) | Followers, technical peers |
| Skill inference Jupyter notebook | this repo + HuggingFace | Recruiters, technical peers |
| Blog post: *"Where OWL reasoners beat (and lose to) LLM reasoning"* | sensemaking-ai.com | Hiring managers, consulting prospects |
| Accessible companion: *"Reifying the Naruto-verse: what fan canon teaches about contested knowledge"* | barbhs.com | Broader audience, anime + tech curious |
| LinkedIn posts linking each | LinkedIn | Broader network |
| Two weekly progress LinkedIn updates per week | LinkedIn | Network at large |

This module is the highest-leverage one for content. The OWL-vs-LLM blog post in particular is positioning gold — write it carefully.

---

## Synthesis notes

One paragraph per week, in your own words. Module 3 notes especially matter because the conceptual material is the densest of the curriculum.

- [ ] `notes/week-07.md`
- [ ] `notes/week-08.md`
- [ ] `notes/week-09.md`

---

## Checklist

### Reading
- [ ] Allemang Ch 9-13
- [ ] W3C SHACL spec (abstract + §5)
- [ ] Hogan et al. Section 6
- [ ] W3C PROV-O spec (for reification project)

### Exercises
- [ ] 3.1 Watch a reasoner work
- [ ] 3.2 All four reification approaches
- [ ] 3.3 Naruto reification project (primary A)
- [ ] 3.4 Skill inference notebook (primary B)

### Notes
- [ ] Week 7
- [ ] Week 8
- [ ] Week 9

### Deliverables
- [ ] Reified Naruto KG with provenance, committed
- [ ] Skill inference notebook published
- [ ] Blog post: OWL vs LLM reasoning (sensemaking-ai.com)
- [ ] Companion post: Naruto-verse reification (barbhs.com)
- [ ] LinkedIn posts linking both
- [ ] Weekly LinkedIn updates × 6
- [ ] End-of-module reflection in `REFLECTIONS.md`

---

## When you're done

Take the conceptual test: can you explain the four reification approaches, give a use case for each, and defend the tradeoffs? If yes, reasoning landed. Move to Module 4.

If the four reification approaches still feel interchangeable, do Exercise 3.2 again before moving on. The four approaches each exist because they solve different problems — if they feel the same, you've missed something important and Module 4's deployment work will be harder.

If only one of Project A or Project B got done, that's fine — pick up the other in Module 4 as you have time. Don't extend Module 3 indefinitely waiting for both.

---

## Module navigation

⬅ [Module 2 — Modeling](../02-modeling/module-02-README.html) · [Back to repo](../../README.md) · ➡ [Module 4 — Shipping](../04-shipping/module-04-README.html)
