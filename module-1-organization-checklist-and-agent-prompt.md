# Module 1 organization cleanup checklist and coding-agent prompt

## Purpose

This file turns the Module 1 organization review into an actionable work plan. The goal is to make Module 1 feel like a real course module for outsiders while preserving the public-learning voice of the Sensemaking Semantic Web curriculum.

The intended end state:

- Module 1 has a clear route selector.
- Canonical readings are required in the recommended path and placed at the right moment.
- The three submodules can be completed at any pace.
- Naruto and Greek mythology are both fully supported dataset paths, with clear context.
- The root-level documentation, Module 1 README, map, roadmap, syllabus, and workbooks agree with each other.
- A coding agent can safely make many of the mechanical documentation and navigation improvements without rewriting the intellectual content.

---

## Key decisions

### 1. Canonical readings are required for the recommended path

The recommended path should not treat Allemang, W3C, DuCharme, or Hogan as optional background. The course’s value is the combination of:

1. canonical sources,
2. Sensemaking synthesis,
3. runnable workbook/lab,
4. small student receipt.

Use this rhythm:

> Read the canon → read the synthesis → run the workbook → save the receipt.

A reading companion may come before the canon when a source is dense.

### 2. Module 1 should be framed as three submodules, not three fixed weeks

Keep the “Module 1 · Foundations” label, but describe the path as three self-paced submodules:

- Submodule 1.1 — RDF as a data model
- Submodule 1.2 — SPARQL basics and query forms
- Submodule 1.3 — Vocabulary landscape and the Resume Graph Explorer

The twelve-week framing can remain at the whole-curriculum level, but Module 1 itself should say that learners can complete the three submodules at their own pace.

### 3. The route selector belongs in the Module 1 README

Do not add a separate `START-HERE.md` yet unless the README becomes too long. The Module 1 README is the natural landing page on GitHub and should become the authoritative start page for the module.

Add the full route selector near the top of:

```text
modules/01-foundations/README.md
```

Place it after the module metadata and before “What you’ll come away with.”

### 4. `map.html` should become the visual companion, not the source of truth

The existing map already explains the materials well: Module README → required reading → synthesis page → exercise, with the cheat sheet as a reference rail. Keep that structure.

Revise the framing so it supports three routes rather than one route:

> Five kinds of material, three ways through.

Add three route cards above the existing visual map:

- Full course path
- Builder-first path
- Artifact path

### 5. `roadmap.html` should stay a status/timeline page

Do not put the route selector in `roadmap.html`. Use it to communicate status, milestones, and what has shipped.

### 6. Greek mythology remains a fully supported alternate path

Do not describe Greek mythology as a fallback or lesser option. Use something like:

> Naruto is the continuity path because it carries into Modules 2–4. Greek mythology is the alternate domain path, designed for learners who prefer a more culturally familiar or less anime-specific dataset. Both paths teach the same RDF/Turtle/SPARQL patterns.

### 7. Shift Module 1 language toward “you will learn”

Because the goal is now an outsider-facing course module, the Module 1 README and student-facing route copy should mostly use “you.” Root-level public-learning language can still acknowledge that the curriculum began as one practitioner’s public learning project.

Avoid making the whole repo sound like a fake institution. Keep the voice honest and solo-authored.

---

## Standalone vs. starter-kit reality check

### What appears standalone now

The conceptual and navigational materials are standalone:

- Root README
- Syllabus
- Module 1 README
- `map.html`
- `roadmap.html`
- glossary
- cheat sheet
- synthesis pages
- reading companion PDF

The resume workbook appears close to standalone because it uses:

```text
modules/01-foundations/artifacts/resume-graph/ttl/resume-001.ttl
```

which lives inside the curriculum repo.

### What is not fully standalone yet

The hands-on Naruto and Greek mythology workbook path does not appear fully standalone at the moment. The workbooks refer to:

```text
data/example.ttl
fuseki/config.ttl
starter-kit root
```

but `data/example.ttl` was not found in the curriculum repo during review, and the workbooks explicitly say they require Fuseki plus the starter kit.

### Recommended strategy

Use the next two weeks to make the starter kit public and excellent, but also make Module 1 “standalone enough” by doing one of the following:

Option A — Keep curriculum and starter kit separate, but make the dependency explicit everywhere.

Option B — Copy the minimum required workbook data/config into the curriculum repo so Module 1 can run without a second repo.

Option C — Use a hybrid approach: keep the full starter kit separate, but include a small `/data/` folder in the curriculum repo with the exact files needed for Module 1.

Recommended choice: **Option C**.

This keeps the course easy for beginners while preserving the starter kit as the fuller runnable environment.

---

## Route selector copy to add to Module 1 README

### Start here: choose your path through Module 1

Module 1 is organized as three self-paced submodules. The recommended path uses the canonical readings, the Sensemaking synthesis pages, and the hands-on workbooks together. The alternate paths are there because different learners need different entry points.

#### Path 1 — Full course path, recommended

Best for learners who want the full conceptual foundation.

1. Read the Module 1 overview.
2. Keep the Module 1 cheat sheet open.
3. For each submodule:
   - Do the canonical reading.
   - Read the Sensemaking synthesis page.
   - Run the workbook.
   - Save the receipt.
4. Finish by building the Resume Graph Explorer RDF slice.
5. Take the 30-second test: explain when to choose RDF over a labeled property graph, and when not to.

#### Path 2 — Builder-first path

Best for learners who need a runnable win before the theory lands.

1. Start Fuseki.
2. Open the Module 1 cheat sheet.
3. Run the 1.1 workbook.
4. Run the 1.2 workbook.
5. Load `resume-001.ttl` and run the 1.3 workbook.
6. Then go back to the canonical readings and synthesis pages to understand what you just did.

#### Path 3 — Artifact path

Best for advanced learners, portfolio builders, or return visits.

1. Read the RDF-vs-LPG synthesis.
2. Run enough workbook queries to understand the data model.
3. Build your own resume RDF slice.
4. Write the side-by-side query comparison.
5. Draft the end-of-module reflection or blog post.

---

## Canonical readings by submodule

| Submodule | Canonical reading | Sensemaking material | Workbook / lab | Receipt |
|---|---|---|---|---|
| 1.1 — RDF as a data model | Allemang Ch. 1–3; W3C RDF Primer; Turtle spec skim | 1.1 RDF vs LPG synthesis; 1.1 reading companion | 1.1 workbook, Naruto or Greek mythology | Explain the URI tax; create or inspect a small Turtle graph |
| 1.2 — SPARQL basics | DuCharme Ch. 1–2 | 1.2 SPARQL query forms synthesis | 1.2 workbook, Naruto or Greek mythology; Wikidata orientation | Run SELECT, ASK, CONSTRUCT, DESCRIBE; save three query patterns |
| 1.3 — Vocabulary landscape | Hogan sections 3–4; optional Linked Data design note | 1.3 vocabulary landscape synthesis | 1.3 resume workbook | Build or adapt a resume RDF slice; run the ESCO/SKOS interop query |

---

## Dataset framing copy

Use this language in the Module 1 README and workbook intros.

### Dataset paths

The Module 1 workbooks support two narrative datasets plus one resume dataset.

**Naruto path.** Use Naruto if you want continuity with the rest of the curriculum. The Naruto graph carries forward into Module 2 ontology design, Module 3 reification/provenance, and Module 4 deployment.

**Greek mythology path.** Use Greek mythology if you want the same RDF/Turtle/SPARQL patterns in a domain that may feel more familiar or less anime-specific. This is a fully supported alternate path, not a lesser version of the exercises.

**Resume path.** Use the resume workbook in Submodule 1.3. This is the professional-data path and the bridge into the primary Module 1 artifact: a resume graph slice with RDF, SKOS, and ESCO-style interoperability.

---

## Action checklist

### A. Root-level documentation

- [ ] Update root README module status from “Not started” to “In progress” for Module 1.
- [ ] Adjust the “not a course you can enroll in” language to something like “not a cohort course or paid enrollment course,” since the materials should now feel usable as a real course module.
- [ ] Revise “How to use this site” so the three reader types remain site-level, but “New readers” are pointed explicitly to the Module 1 route selector.
- [ ] Update `PROGRESS.md` so it reflects Module 1 underway and lists shipped Module 1 materials.
- [ ] Update `roadmap.html` status text so it no longer says only the first synthesis page exists.
- [ ] Keep `roadmap.html` as status/timeline, not a learning route page.

### B. Module 1 README

- [ ] Add a top-level section: “Start here: choose your path through Module 1.”
- [ ] Include three route cards or subsections:
  - Full course path, recommended
  - Builder-first path
  - Artifact path
- [ ] Make the Full course path clearly recommended for outsiders.
- [ ] Add a “Canonical readings by submodule” table.
- [ ] Replace the standalone required-reading block with a shorter section that points to the submodule table.
- [ ] Update the synthesis/reference table to include:
  - 1.1 RDF vs LPG synthesis
  - 1.1 Naruto workbook
  - 1.1 Greek mythology workbook
  - 1.1 reading companion
  - 1.2 SPARQL query forms synthesis
  - 1.2 Naruto workbook
  - 1.2 Greek mythology workbook
  - 1.3 vocabulary landscape synthesis
  - 1.3 resume workbook
  - Module 1 cheat sheet
  - Glossary
  - Curriculum map
- [ ] Add a “receipts” column or section describing what students should produce after each submodule.
- [ ] Clarify Naruto vs Greek mythology as continuity path vs fully supported alternate path.
- [ ] Add a note explaining the starter-kit dependency or the local data/config strategy.
- [ ] Make the 30-second end checkpoint visible near both the beginning and end.
- [ ] Shift most student-facing language from “I will learn” to “you will learn.”

### C. `map.html`

- [ ] Change masthead line from “Five kinds of page, one reading path” to “Five kinds of material, three ways through.”
- [ ] Add three route cards above the existing SVG map:
  - Full course path
  - Builder-first path
  - Artifact path
- [ ] Keep the existing SVG map as the visual explanation of material types.
- [ ] Update the companion deck link so it points to the actual 1.1 reading companion instead of `roadmap.html`.
- [ ] Consider adding submodule links for 1.1, 1.2, and 1.3 rather than only linking to 1.1.

### D. Syllabus

- [ ] Update Module 1 submodule materials to mark 1.2 and 1.3 as developed.
- [ ] Align the syllabus submodule sequence with the Module 1 README route.
- [ ] Decide whether Exercise 1.1 Wikidata belongs in Submodule 1.2 rather than Submodule 1.1. Current recommendation: put it in 1.2, after SPARQL basics.
- [ ] Replace “What I’ll actually learn” with “What you’ll actually learn” in student-facing sections, unless preserving a personal-learning framing is intentional in a specific paragraph.

### E. Workbooks and student friction

- [ ] Fix the 1.2 workbook dataset naming/conflict around Naruto vs mythology.
- [ ] Add “before you begin” boxes to each workbook with exact prerequisites.
- [ ] Add “after you finish” boxes to each workbook with the receipt students should save.
- [ ] Add next/previous navigation between:
  - 1.1 synthesis
  - 1.1 workbooks
  - 1.2 synthesis
  - 1.2 workbooks
  - 1.3 synthesis
  - 1.3 resume workbook
- [ ] Make every workbook state whether it uses curriculum repo files, starter-kit files, or both.
- [ ] Ensure Greek mythology workbooks receive the same navigation and explanatory treatment as Naruto workbooks.
- [ ] If keeping a separate starter kit, add a clear clone/setup box:
  - curriculum repo = reading and HTML materials
  - starter kit repo = runnable data/config
- [ ] If making Module 1 standalone, add minimal data/config to this repo:
  - `data/naruto-example.ttl`
  - `data/mythology-example.ttl`
  - `fuseki/config.ttl`
  - README explaining local setup

### F. Safety and quality checks

- [ ] Do not rewrite the core teaching voice in the synthesis pages unless explicitly asked.
- [ ] Preserve sentence case for headers.
- [ ] Avoid corporate-speak.
- [ ] Avoid adding fake institutional language.
- [ ] Keep Sensemaking AI framed as a solo independent consulting practice.
- [ ] Do not claim credentials not earned.
- [ ] Do not remove the public-learning honesty.
- [ ] Check every link locally or via the hosted site.
- [ ] Search for stale status phrases:
  - `pre-launch`
  - `Not started`
  - `not yet developed`
  - `first synthesis page`
  - `one reading path`
- [ ] Search for starter-kit assumptions:
  - `starter-kit root`
  - `data/example.ttl`
  - `fuseki/config.ttl`
  - `mythology dataset`
- [ ] Verify all changed pages render in browser.
- [ ] Verify no workbook has contradictory dataset instructions.
- [ ] Commit changes in small logical commits.

---

## Coding-agent prompt

Use this prompt with a coding assistant after giving it this checklist.

```text
You are helping reorganize the public Sensemaking Semantic Web curriculum repository:

https://github.com/dagny099/semantic-web-curriculum

Your task is to improve the organization and navigation of Module 1 so it feels like a coherent course module for outside learners, while preserving the author’s voice, public-learning honesty, and existing content.

Read these files first:

1. README.md
2. SYLLABUS.md
3. PROGRESS.md
4. roadmap.html
5. map.html
6. modules/01-foundations/README.md
7. modules/01-foundations/submodules/1-1-rdf-vs-lpg.html
8. modules/01-foundations/submodules/1-2-sparql-basics.html
9. modules/01-foundations/submodules/1-3-vocabulary-landscape.html
10. modules/01-foundations/submodules/1-1-workbook-naruto.html
11. modules/01-foundations/submodules/1-1-workbook-mythology.html
12. modules/01-foundations/submodules/1-2-workbook-naruto.html
13. modules/01-foundations/submodules/1-2-workbook-mythology.html
14. modules/01-foundations/submodules/1-3-workbook-resume.html
15. reference/cheatsheets/module-1-cheatsheet.html
16. glossary.html

Project context:

- This is a 12-week self-directed curriculum through RDF, OWL, SPARQL, and modern knowledge graphs.
- The curriculum has four modules: Foundations, Modeling, Reasoning, Shipping.
- Module 1 should be organized as three self-paced submodules, not fixed calendar weeks.
- The recommended path requires canonical readings.
- The three Module 1 paths are:
  1. Full course path, recommended
  2. Builder-first path
  3. Artifact path
- Naruto and Greek mythology are both fully supported dataset paths.
- Naruto is the continuity path into Modules 2–4.
- Greek mythology is the alternate domain path for learners who prefer a less anime-specific dataset.
- The Resume Graph Explorer path is the professional-data path and the bridge into the Module 1 artifact.
- The course should now feel usable by outside learners, not only like a personal notebook.

Voice and style constraints:

- Use sentence case for headers.
- Preserve the author’s voice: curious, pragmatic, concrete, honest about tradeoffs.
- Avoid corporate-speak such as “leverage,” “synergy,” “robust,” and “best-in-class.”
- Do not imply a fake team. Sensemaking AI is a solo independent consulting practice.
- Do not invent credentials or affiliations.
- Do not delete the public-learning honesty. It is okay to say the curriculum is worked in public.
- Student-facing Module 1 route copy may use “you,” but root-level framing may still acknowledge the author’s public learning project.
- Do not rewrite the major synthesis essays unless absolutely necessary for navigation consistency.

Primary implementation tasks:

1. Update modules/01-foundations/README.md.
   - Add a “Start here: choose your path through Module 1” section near the top.
   - Include the three route paths.
   - Add a “Canonical readings by submodule” table.
   - Update the synthesis/reference table so it includes all shipped Module 1 synthesis pages and workbooks.
   - Clarify Naruto, Greek mythology, and Resume paths.
   - Clarify what files or repos are required to run the workbooks.
   - Make the 30-second checkpoint visible near the beginning and end.

2. Update map.html.
   - Change the framing from “one reading path” to “three ways through.”
   - Add three route cards above the existing map.
   - Keep the existing map as the visual explanation of material types.
   - Fix the reading companion link if it currently points to roadmap.html.
   - Add links to 1.2 and 1.3 materials where appropriate.

3. Update root-level docs.
   - README.md should point new readers to the Module 1 route selector.
   - README.md status table should not say Module 1 is “Not started” if materials have shipped.
   - PROGRESS.md should reflect Module 1 underway and list shipped materials.
   - roadmap.html should no longer say only the first synthesis page exists.

4. Update SYLLABUS.md.
   - Mark 1.2 and 1.3 materials as developed.
   - Align the Module 1 submodule structure with the Module 1 README.
   - Keep canonical readings attached to the submodule where they are used.

5. Fix workbook navigation and friction.
   - Add or update “before you begin” boxes.
   - Add or update “after you finish” receipt boxes.
   - Add next/previous navigation where missing.
   - Fix contradictory dataset language, especially places where Naruto data is described as loaded into a mythology dataset.
   - Make each workbook explicit about whether it uses files in this curriculum repo, the starter kit repo, or both.

Important safety instructions:

- Work in small commits or a branch.
- Before editing, search the repository for:
  - pre-launch
  - Not started
  - not yet developed
  - first synthesis page
  - one reading path
  - starter-kit root
  - data/example.ttl
  - fuseki/config.ttl
  - mythology dataset
- Do not remove existing pages.
- Do not rename public HTML files unless you also update every link.
- Do not make sweeping style changes.
- Do not change the curriculum’s conceptual claims without flagging the change.
- After editing, verify links and render the HTML pages locally.
- Return a concise summary of changed files, decisions made, and any remaining questions.

Deliverables:

- Updated files in the repo.
- A short implementation summary.
- A list of unresolved questions or places where manual author review is needed.
```

---

## Suggested first branch name

```text
module-1-route-selector
```

## Suggested commit sequence

1. `docs: add module 1 route selector`
2. `docs: update curriculum status and roadmap`
3. `docs: align module 1 syllabus entries`
4. `docs: clarify workbook prerequisites and dataset paths`
5. `docs: update curriculum map routes`

## Manual review checklist after coding agent finishes

- [ ] Does Module 1 feel like a course module an outsider can start?
- [ ] Can a beginner tell exactly when to do the canonical readings?
- [ ] Can a builder tell exactly how to start running queries?
- [ ] Can an advanced learner tell what artifact to produce?
- [ ] Are Naruto and Greek mythology both framed respectfully and clearly?
- [ ] Are starter-kit dependencies honest?
- [ ] Is any page still saying “pre-launch” or “not yet developed” incorrectly?
- [ ] Are there any broken links?
- [ ] Does the tone still sound like Sensemaking AI rather than a generic course platform?
