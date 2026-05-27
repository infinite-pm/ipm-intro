# Spec — main README (`/README.md`)

This file is part of the [`meta/`](.) directory: short living specs for each documentation artifact in the repo. It describes the **purpose, scope, structure, and style** the top-level [`/README.md`](../README.md) should follow. Update this spec when the practice changes; treat it as a guide, not a contract.

## Purpose

The main README is **the onboarding doc for newcomers to infinite.pm modeling**. A reader who has never heard of Semantic Spacetime or `ipm` should leave the page able to:

- say what infinite.pm is (one sentence) and where it is heading;
- recognize the **three node kinds** (event, thing, concept) and the **four edge kinds** (leads-to, part-of, expresses, near-to) — as **modeling primitives**, not as text-format details;
- read and roughly understand a small ipmt diagram;
- find the next thing to read (a worked example, an external reference, or — when they want it — the ipmt syntax spec).

If the reader closes the tab wanting to look at a worked example or try modeling something themselves, the README has done its job. If they close it buried in escape rules or rendering internals, it has not.

## In scope

- **A short framing** of what infinite.pm is and where it is heading. Two or three paragraphs, no more.
- **A small amount of project context**: who is building it, current status, how to support it. Brief, factual.
- **The modeling vocabulary** — events, things, concepts; leads-to, part-of, expresses, near-to. The *domain meaning* of each node and edge kind: what it represents in the world being modeled.
- **A step-by-step build-up** on one concrete tiny scene (Patrick swaps a t-shirt). Each step adds exactly one new modeling idea: chain → participants → properties → containment / zoom levels.
- **Reference tables** for the edge kinds and the legal source→target combinations, after the example so the reader can use them as a lookup once they have vocabulary.
- **Pointers** to deeper material: worked examples under `docs/examples/`, external Mark Burgess reading, and the separate ipmt syntax spec when the reader needs syntactic detail.

## Out of scope — belongs elsewhere

- **ipmt syntax**. The text format's grammar — escaping rules, alias declarations, comma/quote handling, fence behaviour — belongs in a separate document (`docs/ipmt-spec.md` or the upstream `ipm-drawio/docs/ipmt-spec.md`). The main README *uses* ipmt in fenced blocks but does not teach its grammar. Where syntactic detail is unavoidable in the README, link out, do not inline.
- **Tooling internals.** How the renderer works, how to install the VS Code extension, contributor guide, CI integration — all go in their own files when they exist. The README mentions tooling exists, but does not document it.
- **Theoretical depth.** Full Semantic Spacetime γ(3,4) treatment, Promise Theory background, comparisons to ontology / RDF / property graphs — link to Mark Burgess's writings (and the [semantic.st](https://semantic.st/) project home) rather than repeating them. Mark explains his framework better than we can.

## Structure rules

The README walks the reader through one logical arc; each section adds something new without backtracking.

1. **Title + one-line tagline.** A short quote or epigraph is allowed if it earns its place.
2. **What is infinite.pm?** Short framing paragraphs: what it is, what is powerful about it, where it is heading. Tooling note (current status + sponsors) sits here too, near the bottom of the section. Brief mention of the `ipmt` text format — no syntax.
3. **The three node kinds.** Quick table (Event / Thing / Concept) with examples. Rule-of-thumb decision flow. Note that "thing-ness" depends on the chosen timescale. Two short subsections immediately after: **Every model has a purpose** and **Every model is an observer's account** — they frame the modeling stance *before* the example starts.
4. **Build it up — by example.** A small numbered step sequence on the Patrick scene. Each step introduces exactly one new idea: event chain → participants (thing → event) → properties (concept) → containment / zoom levels → full nested model. Optionally close with a link to an alternative worked example.
5. **The four edge kinds + All allowed edges.** Reference tables with the LPXN diagram, after the example. The reader now has enough vocabulary to use this as a lookup. A short blockquote near the LPXN diagram flags that IPM's edge labels differ from Burgess's original SST labels and links to [`docs/ipm-vs-sst.md`](../docs/ipm-vs-sst.md) for the rename rationale — but the actual C→P / E→X explanation does **not** live in the README; it is one click away in its own doc.
6. **Where to look next.** Pointers: worked examples in this repo, external Mark Burgess reading, the **ipmt syntax spec** for readers who now want syntactic detail, and related repos.

## Style rules

- **Example-led.** Every modeling idea is introduced through the Patrick scene, not as an abstract definition. Definitions come second, after the reader has seen the thing.
- **One new idea per step.** If a step adds participants *and* concepts, split it. The reader's working memory is the budget.
- **Smart-but-new audience.** No jargon without an in-line definition the first time. No syntax explanation unless it directly serves a modeling point right there.
- **Avoid syntax detail.** When the reader needs to know how an alias works, how to escape a comma, or how leads-to vs part-of resolves between event-to-event, the answer is *"see the ipmt spec"* — not three sentences of grammar in the README.
- **Tight prose.** A clear short paragraph beats a long elegant one. Cut sentences that only restate the previous one.
- **Diagrams render inline.** Every ipmt fence is paired with a rendered SVG below it (auto-generated by [`md-embed`](https://github.com/mj41/ipm-drawio/tree/main/cmd/md-embed)). PNG diagrams use `<img height|width="...">` so they fit the column.
- **No marketing voice.** No "powerful," "revolutionary," "next-generation." The framework is interesting enough on its own.
