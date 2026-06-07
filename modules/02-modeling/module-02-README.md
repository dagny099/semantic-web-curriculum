# Module 2 — Modeling

> RDFS, OWL, ontology design. The shift from RDF as data format to ontology as design discipline.

**Weeks:** 4-6
**Effort:** ~6-8 hours per week
**New ground:** Medium — modeling judgment is the central new skill

---

You've probably designed a schema that fought you for months without realizing the fight had already started. A table with too many nulls. A property that turned out to mean three different things. The model seemed fine when you built it; the wrongness compounded quietly.

An ontology is the same problem made visible. Every class boundary, every reuse decision, every constraint you add or skip is a small modeling choice — and those choices compound, into clarity or into pain. What's different here is that the decisions are explicit and inspectable, written in a form you can reason over, share, and change deliberately. Categories are how minds carve the world into workable chunks. Ontology design is doing that carving in the open. Module 2 is where that becomes a skill you can exercise rather than a problem you run into.

## What you'll come away with

By the end of this module, you can:

- Design and publish a small OWL ontology → make class boundaries explicit in a form a reasoner can check
- Choose between reusing and defining terms → borrow from `foaf:`, `schema:`, `skos:` where they fit; define your own where they don't, so the decision is intentional rather than accidental
- Express SHACL constraints → close the open world where your application needs it, without dismantling the open-world semantics underneath
- Know the five OWL profiles → match the profile to what the reasoning problem actually requires and name the tradeoff you're accepting
- Recognize the classic modeling traps → catch transitivity cascades, punning confusion, and `sameAs` collapses before they become load-bearing problems

The **artifact test** for this module: is the Naruto ontology published in this repo with a real README, REUSE.md, SHACL shapes, and example queries that demonstrate value over plain co-appearance edges? If yes, modeling landed.

---

## Required reading

| Source | Chapters / sections | Time |
|---|---|---|
| Allemang, Hendler & Gandon — *Semantic Web for the Working Ontologist* | Ch 6-8 | ~6 hours |
| [W3C OWL 2 Primer](https://www.w3.org/TR/owl2-primer/) | Whole document | ~2 hours |
| Hogan et al. — *Knowledge Graphs* | Section 5 (schema, identity, context) | ~2 hours |

Allemang Ch 6-8 is the heart of this module. The OWL Primer is denser; read it after Allemang has built the conceptual scaffolding.

## Optional deeper reading

- [Ontology Design Patterns (ODP) portal](http://ontologydesignpatterns.org/) — community-maintained catalog of reusable patterns. Read at least `Information Realization`, `Time-Indexed Situation`, and `N-ary Relation`.
- [Pizza Tutorial](https://www.michaelcdebellis.com/post/new_protege_pizza_tutorial) — the canonical first ontology in Protégé. Worth doing once.
- DuCharme — Chapters 3-4 (more SPARQL patterns).

---

## Exercises

### Exercise 2.1 — Protégé pizza walkthrough *(2-3 hours)*

Work through the Pizza Tutorial in Protégé. The point is muscle memory with the tool, not pizza expertise. Build the class hierarchy, add object properties, run the HermiT reasoner, observe what gets inferred.

Notes go in `notes/week-04-protege.md`. Capture: what was easier than expected, what was harder, where the UI fought you.

### Exercise 2.2 — Read an enterprise ontology *(1 hour)*

Browse the [Financial Industry Business Ontology (FIBO)](https://spec.edmcouncil.org/fibo/). Read one module's documentation in detail — `Foundations` or `Business Entities` are good starting points.

Notice the rigor: every class has a defining text, every property has domain and range, alignment with other vocabularies is explicit. This is what production ontology engineering looks like. Your Naruto ontology will be smaller, but should aim for the same kind of discipline.

Capture observations in `notes/week-04-fibo.md`. One paragraph on what surprised you.

### Exercise 2.3 — Build the Naruto ontology *(8-12 hours)* — **primary project**

See [Primary project hook](#primary-project-hook-a-naruto-ontology) below.

---

## Primary project hook: A Naruto ontology

The Naruto domain has unusually rich categorical structure: a clean subclass hierarchy in ninja ranks, multiple relationship types (sensei-of, member-of-team, member-of-village, has-jutsu, rival-of, family-of), temporal events (arcs, episodes), and contested fan-canonical material that creates real ontology design tradeoffs. Pop-culture domains are standard in ontology pedagogy for exactly this reason — they make the modeling decisions interesting.

### Goal

Design and publish `naruto-ontology-1.0.0.ttl` — an OWL ontology that formalizes the Naruto universe on top of the co-appearance graph you've already built.

### Steps

1. **Decide scope.** Don't try to model the whole series. Focus on what the existing [Naruto Network Graph](https://docs.barbhs.com/naruto-network-graph/) covers — three S-tier arcs, 87 characters. Core classes:
   - `Character` (subclass of `schema:Person`)
   - `Ninja` (subclass of `Character`)
   - `NinjaRank` with subclasses `Genin`, `Chunin`, `Jonin`, `Kage` — the cleanest subclass hierarchy in the domain
   - `Village` (subclass of `schema:Organization`)
   - `Team` (subclass of `schema:Organization`)
   - `Jutsu` (custom)
   - `Arc` (subclass of `schema:Event` or `schema:CreativeWork` — design decision)
   - `Episode` (reuse `schema:TVEpisode`)
   - Object properties: `senseiOf`, `studentOf`, `memberOfTeam`, `memberOfVillage`, `hasJutsu`, `rivalOf`, `familyOf`

2. **Reuse where possible.** Use `schema:` for everything that has a schema.org equivalent. Use `foaf:` where it fits. Document each reuse decision in `REUSE.md`. Resist defining custom properties when a standard one fits — every custom term is a future maintenance burden.

3. **Define what's new carefully.** Jutsu and NinjaRank are clear. The design-interesting decisions: how do you handle characters whose rank changes across arcs? (Hint: this is where the time-indexed situation pattern comes in.) How do you handle alliances that shift mid-arc? Make these decisions deliberately and document them.

4. **Add restrictions carefully.** A `Ninja` must have at least one `memberOfVillage`. A `Team` must have at least one `memberOfTeam`. Resist adding more restrictions until you have data to validate against — every premature restriction is a future bug.

5. **Express constraints in SHACL.** This is where the "open-world is annoying for applications" problem gets handled. SHACL is closed-world by default. Write shapes for `Ninja`, `Team`, `Arc` that enforce the structure you need for downstream queries to behave predictably.

6. **Validate against real data.** Convert your Chunin Exams arc subset (from Module 1's Exercise 1.4) to use this ontology. Run SHACL validation. Fix issues. Iterate. Expect to redo the class hierarchy at least twice — this is the work, not a sign of failure.

7. **Publish.** The ontology lives at `artifacts/naruto-ontology/` in this module's folder, with:
   - `naruto-ontology-1.0.0.ttl` — the ontology file
   - `README.md` — design decisions, scope notes, link to WebVOWL screenshots
   - `REUSE.md` — which external vocabularies are used, with rationale
   - `examples/` — example data files using the ontology
   - `queries/` — SPARQL queries that demonstrate value-add over the property graph version
   - `docs/` — WebVOWL screenshots and any other diagrams
   - `shapes/` — SHACL shapes

### Optional secondary project: career narrative ontology

If you finish the Naruto ontology with time to spare, design a small ontology layer for Resume Graph Explorer that captures `CareerTransition` as a class with `fromRole`, `toRole`, `transitionType`. Scope this small — it's a stretch goal, not a requirement. The reason to do it: the career-narrative angle is consulting-positioning gold and gives you a second ontology under your belt.

### What you'll feel

The first hour is exhilarating — ontology design is genuinely creative work, and you have decades of Naruto canon in your head to draw on. The next 20 hours are humbling. You will redo the class hierarchy at least three times. You will discover that what you thought was a clean class is actually a property. You will argue with yourself about whether `Sage Mode` is a `Jutsu` subclass or an instance.

The redos are the point. They're what builds modeling judgment.

---

## Pain points to surface

These are the tensions worth naming in the blog post and surfacing in the synthesis notes:

- **OWL profiles confusion.** OWL Full is undecidable; DL, EL, QL, RL each trade expressive power for computational guarantees. Most production systems use EL or QL because they're tractable. Books and courses lean DL because that's where the interesting logic is. Know all five exist and what each trades.

- **Punning.** Sometimes you want something to be both a class and an instance. "Software Engineer" is an instance of "Job Title" but also a class whose instances are individual software engineers. OWL 2 allows "punning" — using the same URI as both. Useful and confusing.

- **The transitivity trap.** Tempting to declare properties transitive, symmetric, inverse. Each declaration cascades through the reasoner. A transitive `partOf` on a large graph means computing the transitive closure on every query. Performance gets pathological quickly.

- **Reusing vs. defining.** Should you reuse `foaf:knows` or define `sensemaking:professionallyKnows`? Reuse improves interoperability and increases your dependency surface. There's no clean rule — only judgment.

- **Open-world reasoning bites.** RDFS says "if X is in the domain of property P, and Alice has property P with some object, then Alice is an X." It doesn't say "if Alice is not stated to be X, she isn't X." Coming from SQL this is genuinely strange. You'll write a query that returns surprising results because the reasoner inferred a class membership you didn't expect.

---

## Publishable deliverables

| Artifact | Where | Audience |
|---|---|---|
| `naruto-ontology-1.0.0.ttl` + README + REUSE.md + WebVOWL screenshots | this repo (`modules/02-modeling/artifacts/naruto-ontology/`) | Ontologists, anime fans, recruiters |
| Blog post: *"Designing an anime ontology in public: the small modeling decisions that compound"* | sensemaking-ai.com | Practitioners |
| LinkedIn post linking to ontology release with WebVOWL hook image | LinkedIn | Broader network |
| Optional Twitter/Mastodon thread for Naruto + tech audience | external | Cross-community curious |
| Two weekly progress LinkedIn updates per week | LinkedIn | Network at large |

---

## Synthesis notes

One paragraph per week, in your own words. These become source material for the blog post and the Digital Twin's knowledge base.

- [ ] `notes/week-04.md`
- [ ] `notes/week-05.md`
- [ ] `notes/week-06.md`

---

## Checklist

### Reading
- [ ] Allemang Ch 6-8
- [ ] W3C OWL 2 Primer
- [ ] Hogan et al. Section 5

### Exercises
- [ ] 2.1 Protégé pizza walkthrough
- [ ] 2.2 Read one FIBO module
- [ ] 2.3 Naruto ontology v1.0 (primary)

### Notes
- [ ] Week 4
- [ ] Week 5
- [ ] Week 6

### Deliverables
- [ ] `naruto-ontology-1.0.0.ttl` published
- [ ] README + REUSE.md complete
- [ ] WebVOWL visualization captured
- [ ] SHACL shapes validate against real data
- [ ] Example queries demonstrate value-add over LPG version
- [ ] Blog post drafted
- [ ] Blog post published
- [ ] LinkedIn release announcement
- [ ] Weekly LinkedIn updates × 6
- [ ] End-of-module reflection in `REFLECTIONS.md`

---

## When you're done

This module opened with one claim: that modeling decisions compound quietly over time, and the skill here is making those decisions deliberately rather than discovering their consequences late. The test of whether that landed isn't naming the five OWL profiles.

Take the artifact test: is the Naruto ontology published with a real README, validated against real data, and queryable in ways that demonstrate value beyond what the property graph alone offers? If yes, the compounding went the right direction. Move to Module 3.

If the ontology is still in draft state after Week 6, take an extra week before Module 3 — reasoning work depends on having an ontology to reason over. Rushing forward with a half-finished ontology will compound difficulty. Better to slow down here than to struggle in Module 3.

If after 20+ hours the class hierarchy isn't stabilizing, the gap may be bigger than this module can close. Consider writing up "lessons from a stalled ontology project" as a credible artifact in its own right, and move to Module 3 with the Pizza ontology (from Exercise 2.1) as your reasoning target instead.

---

## Module navigation

⬅ [Module 1 — Foundations](../01-foundations/README.html) · [Back to repo](../../README.md) · ➡ [Module 3 — Reasoning](../03-reasoning/module-03-README.html)
