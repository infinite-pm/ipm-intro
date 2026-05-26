# infinite.pm

A newcomer's introduction to [**infinite.pm**](https://infinite.pm) — Infinite Process Modeling (**ipm**, also written **IPM**).

_"The universe is made of stories, not of atoms."_ – Muriel Rukeyser

## What is infinite.pm?

**infinite.pm** is a way to model processes, stories, and systems as readable graphs. It is an experiment in applying Mark Burgess's [Semantic Spacetime γ(3,4)](https://semantic.st/) (**SST**) representation — to everyday modeling work and software engineering.

Mark Burgess's insight, and the foundation of γ(3,4): with just **three kinds of nodes** and **four kinds of edges**, you can sketch (in our reading) *any observer's view of anything* in space and time — a process, a story, a system, life, the universe, and everything.

**Where this is going.** The infinite.pm project is an **experiment** in **Semantic Spacetime-based modeling and cooperation** between agents. **Smart agents** like humans, AI agents, and smart machines assess promises made by stigmergic trails, tools, and things — to explore, evolve, and endure. The aim is to help us *externalize* our mental models in the form of ipm stories/processes/loops, **think with them as a partner** (in the spirit of Niklas Luhmann's [Zettelkasten](https://en.wikipedia.org/wiki/Zettelkasten)), and gradually integrate them into **one living graph**. The medium we are aiming at: the [infinite canvas](https://infinitecanvas.tools/).

**Tooling.** Today there is a VS Code extension for live editing and preview of `ipmt` (the infinite.pm text format for these graphs), plus a small renderer that compiles ipmt fenced blocks into the SVG diagrams you see throughout this README. [mj41](https://mj41.cz/) is prototyping these (**spec-driven/vibe-coded**) and will open-source them over time as they stabilize. [Sponsors](https://github.com/sponsors/mj41) — AI-token kind or life kind — are always welcome; both speed this up a bit.

## The three node kinds

| Kind | Symbol | What it is | Examples |
| --- | :---: | --- | --- |
| **Event** | `e` (orange) | A transient happening — fast at the model's timescale | "User clicks button", "Build runs", "K8s service deploying", "Plum murders Scarlet" |
| **Thing** | `t` (green) | A persistent participant — slow at the model's timescale | "Alice", "my laptop", "service A container", "knife K1", "Mrs. Scarlet", "Prof. Plum" |
| **Concept** | `c` (blue) | A quasi-invariant pattern; a property that events or things can express | "human", "microservice", "production environment", "murder" |

Rule of thumb, in order:

1. *Is something happening here, at the timescale I care about?* → **event**
2. *Does it persist with stable identity while its state changes?* → **thing**
3. *Does it stay the same across all events and things that express it?* → **concept**

A thing isn't literally static — it's *slow enough* at the chosen timescale that you can treat it as unimportant for the model's purpose. A laptop is a thing inside a "type a doc" event; the laptop *is* an event chain if you zoom out to its whole lifetime, from purchase to retirement. Pick the scale first, then split fast/dynamic and slow/static.

### Every model has a purpose

> *A model is a simplified representation of something for a purpose.* — Joshua Spodek, *Leadership Step by Step*, via [mj41 — my mental models](https://blog.mj41.cz/my-mental-models-83adc08d648b)

The purpose decides what goes in and — equally important — what stays out. *"What is not in the scope of your model has the same importance as what is in the scope."* A map of the Czech Republic for *"where is it on a globe?"* looks nothing like a map for *"where is the nearest bakery?"* Both are good models if the purpose is clear; both are useless if the purpose is the other one.

Before you start creating an infinite.pm graph, decide what **question** or **purpose** this model/view is going to answer. That decides which events, things, and concepts belong in it, and which would just be noise.

### Every model is an observer's account

There is no view-from-nowhere. An ipm graph is always **someone's** account of a slice of the world — what *they* saw, at *their* chosen timescale, with *their* chosen boundary. This matters most for concepts: deciding that `swap t-shirt ::e` expresses `swap of clothing ::c` rather than `magic trick ::c` is in the eye of the beholder. Two honest observers can produce two different but non-contradictory models of the same scene. Combined with a shared collection of models, infinite.pm tools can surface views and beliefs you missed.

## Build it up — by example

We'll model the same tiny scene step by step: *Patrick swaps a black t-shirt for a white one.*

### Step 1 — just an event chain

Start with the activity. Events lead to other events.

```ipmt
Patrick wears black t-shirt ::e
  --> Patrick wears white t-shirt ::e
```
<!-- ipm-svg id=01 hash=0183bb61 -->
![](_ipm/README/01.ipm.svg)


`-->` between two events means **leads-to** (rendered as an **orange arrow**) — temporal/causal flow. `::e` marks each node as an event. The chain shows only what the observer *directly saw*: two wear states. Step 2 onward adds a `swap` event between them — a *hypothesized* middle step the observer didn't witness.

### Step 2 — add a participant (thing → event)

Patrick is *in* every event. A thing participates in an event by being **part of** it — a **spatial** containment relation (the thing sits inside the event's region of space and time), rendered as a **green arrow**.

```ipmt
Patrick wears black t-shirt ::e wearB::a
  --> Patrick swaps t-shirt ::e swapT::a
  --> Patrick wears white t-shirt ::e wearW::a

# Patrick participates in every event in the chain
Patrick --> wearB, swapT, wearW
```
<!-- ipm-svg id=02 hash=440d7925 -->
![](_ipm/README/02.ipm.svg)

Two new tricks:

- `wearB::a` is an **alias** — a short stable name for the long event title.
- `Patrick --> wearB, swapT, wearW` fans out: one source, three targets.

Unmarked nodes default to **things**. The arrow goes *from the thing to the event* — the thing is part of the event, never the other way around (a modeling rule, not a syntactic accident).

**Add the t-shirts as participants too.** The black t-shirt is worn in `wearB` and is still on Patrick (briefly) during `swapT`; the white one enters at `swapT` and stays on through `wearW`. Each thing attaches to the events where it actually appears.

```ipmt
Patrick wears black t-shirt ::e wearB::a
  --> Patrick swaps t-shirt ::e swapT::a
  --> Patrick wears white t-shirt ::e wearW::a

Patrick --> wearB, swapT, wearW

t-shirt B --> wearB, swapT
t-shirt W --> swapT, wearW
```
<!-- ipm-svg id=03 hash=44bba970 -->
![](_ipm/README/03.ipm.svg)

**You can also zoom *out*.** The same scene can be told at a coarser level: one single event that names only the *observable* change (Patrick wore black, then white), with every participant attached at that one level. The mechanism — *how* he changed t-shirts — is hidden inside the wrapper event and revealed only when you zoom in.

```ipmt
Patrick wears black then wears white ::e wearBW::a

Patrick    --> wearBW
t-shirt B  --> wearBW
t-shirt W  --> wearBW
```
<!-- ipm-svg id=04 hash=65822860 -->
![](_ipm/README/04.ipm.svg)

Same story, different zoom level. The right level depends on the **purpose** of your model — and you don't have to pick just one.

Going the other direction, **zoom in**: replace a coarse event with its sub-events. The next two diagrams show pure *event structure* — no participants, no concepts — so the zoom move stands on its own. First, drill into `wearBW` and show its three mid-level sub-events as a leads-to chain, each part-of the parent:

```ipmt
Patrick wears black then wears white ::e wearBW::a

Patrick wears black t-shirt ::e wearB::a
  --> Patrick swaps t-shirt ::e swapT::a
  --> Patrick wears white t-shirt ::e wearW::a

wearB --::P--> wearBW
swapT --::P--> wearBW
wearW --::P--> wearBW
```
<!-- ipm-svg id=05 hash=119e8e54 -->
![](_ipm/README/05.ipm.svg)


We can keep going — `swapT` itself decomposes into a finer chain of moments. Here are both zoom levels at once, three levels of pure event nesting:

```ipmt
Patrick wears black then wears white ::e wearBW::a

# Mid-level: wear -> swap -> wear, each part-of the top
Patrick wears black t-shirt ::e wearB::a
  --> Patrick swaps t-shirt ::e swapT::a
  --> Patrick wears white t-shirt ::e wearW::a

wearB --::P--> wearBW
swapT --::P--> wearBW
wearW --::P--> wearBW

# Inner: the swap decomposes further
Take off black ::e takeOff::a       --::P--> swapT
Patrick half-naked ::e halfNaked::a --::P--> swapT
Take on white ::e takeOn::a         --::P--> swapT

takeOff --> halfNaked --> takeOn
```
<!-- ipm-svg id=06 hash=e7b5cdce -->
![](_ipm/README/06.ipm.svg)


Step 4 will bring Patrick, the t-shirts, and the concepts back into this nested structure.

### Step 3 — give a property with a concept

What *properties* does Patrick express? What *property* does the swap event express? Each concept names a single, independent property.

```ipmt
Patrick --> human ::c
swaps t-shirt ::e --> swap of clothing ::c
```
<!-- ipm-svg id=07 hash=34d22075 -->
![](_ipm/README/07.ipm.svg)


`::c` marks the node as a concept. The arrow `thing --> concept ::c` (an **expresses** arrow, rendered **blue dashed**) reads as "the thing expresses property cX" — and `event ::e --> concept ::c` reads the same way for an event. A node can have several such arrows, one per property; this is **not** isa / classification — each concept is one promise the node makes, not a slot in a taxonomy. Patrick can express `human ::c`, `tall ::c`, and `colleague ::c` simultaneously without any of those being his "type".

A concept is what stays the same across all events and things that express it — what Mark Burgess calls a **quasi-invariant pattern**. The patterns are out there in the scene, but **which patterns the observer names** is a choice, not a fact about the world: Mark writes that "there is no universal set of concepts to subdivide knowledge … these are merely ad hoc ways of spanning a collection of connected ideas, chosen by convention or happenstance" ([article 13](https://mark-burgess-oslo-mb.medium.com/avoiding-the-ontology-trap-2f1c3f3ed8e2)). Two honest observers can carve the same scene into different — and equally valid — concept vocabularies; writing `swap of clothing ::c` is the modeler saying *this is the pattern I noticed and chose to name*.

### Step 4 — bring it together, with a parent event

The full story now has *three zoom levels*: the top event (the whole swap), its three mid-level events (wear → swap → wear), and the inner moments of the swap itself (take-off → half-naked → take-on). We attach each participant at the finest level where it actually appears — part-of transitivity automatically carries it upward into every containing event. A small **color taxonomy** (`t-shirt ::c`, `black ::c`, `white ::c`, `color ::c`) joins the concepts from Step 3 (`human ::c`, `swap of clothing ::c`).

```ipmt
# Top-level event
Patrick wears black then wears white ::e wearBW::a

# Mid-level sub-events — leads-to chain, each part-of the top
Patrick wears black t-shirt ::e wearB::a
  --> Patrick swaps t-shirt ::e swapT::a
  --> Patrick wears white t-shirt ::e wearW::a

wearB --::P--> wearBW
swapT --::P--> wearBW
wearW --::P--> wearBW

# Inner sub-events — the swap itself decomposes into a finer chain
Take off black ::e takeOff::a       --::P--> swapT
Patrick half-naked ::e halfNaked::a --::P--> swapT
Take on white ::e takeOn::a         --::P--> swapT

takeOff --> halfNaked --> takeOn

# Patrick is present for the whole swap — attach at the top.
# Part-of transitivity carries him into every sub-event automatically.
Patrick --> wearBW
Patrick --> human ::c
swapT --> swap of clothing ::c

# T-shirts come and go — attach at the finest level where they actually appear:
# the black one is worn (wearB) and then removed (takeOff); the white one is
# put on (takeOn) and then worn (wearW).
t-shirt B --> wearB, takeOff
t-shirt W --> takeOn, wearW
t-shirt B --> t-shirt ::c, black ::c
t-shirt W --> t-shirt ::c, white ::c

# A color is itself a property — concept expresses concept
black ::c --> color ::c
white ::c --> color ::c
```
<!-- ipm-svg id=08 hash=9bd40bd3 -->
![](_ipm/README/08.ipm.svg)


That's a complete ipmt model: events lead to events, things participate in events, things and events express concepts as properties, and concepts can themselves express properties of other concepts.

**Spacetime, made explicit.** The leads-to chain is *time*; the part-of containment is *space*. Mark Burgess puts it directly: an event is *"any region of space and time"* — a slice of the world where **things and ideas come together for a while** (his phrase is "occurrences of things and ideas together in time"). The parent event `wearBW` is one such region — it holds Patrick (the slow worldline) for its whole duration; each sub-event is a smaller spacetime region nested inside it, where faster things (specific t-shirts being worn or swapped) come and go. Concepts (`human ::c`, `color ::c`) sit *outside* spacetime entirely — they are invariant patterns the events and things express, the same in every frame.

**Zoom out far enough, and "things" become events too.** At the timescale of the swap, each t-shirt is a stable thing. Zoom out to the t-shirt's whole life — manufactured, bought, worn through hundreds of days, washed many times, eventually torn, thrown away (or perhaps given a second life as a rag) — and that *thing* is itself an event chain on its own worldline. Patrick, zoomed out to his whole life, is the same: born, grows up, swaps many t-shirts, and eventually dies. The thing/event split is **not** a property of the world; it is a property of the **scale you chose** to model at. Every "thing" is a slow process; every "event" is a process you decided to look at closely.

**An alternative, fuller worked example** of the same scene — with two different observer accounts of the swap (one exchange, one layered black-over-white), a deeper zoom into the swap itself, *open-world* probe events that decide which observation actually happened, and small color and clothing taxonomies — is in [`docs/examples/tshirt-magic.md`](docs/examples/tshirt-magic.md). Same building blocks; more depth.

## The four edge kinds

<img src="docs/etc-LPXN.png" alt="Semantic Spacetime gamma(3,4) edges" width="500"/>

The triangle is **e** (event), **t** (thing), and **c** (concept). The arrows and self-loops show every legal edge. The dotted circles (Nₑ, Nₜ, N𞁞) are **NEAR** — similarity between two nodes of the same kind, undirected.

> The edge symbols **L / P / X / N** are IPM's mnemonic; Burgess's original SST uses **L / C / E / N**. For why IPM renames C → P (and reverses its direction) and E → X, see [`docs/ipm-vs-sst.md`](docs/ipm-vs-sst.md).

| Symbol | Color | Name | Meaning | When to use |
| :---: | --- | --- | --- | --- |
| **L** | orange | LEADS-TO | Temporal / causal flow | One event causes or precedes another |
| **P** | green | PART-OF | Containment / participation | A thing is inside an event, a sub-event is inside a parent event, or a sub-part is inside a bigger thing |
| **X** | blue dashed | EXPRESSES | Property (a single promise) | An event or thing expresses a concept as a property; a concept itself can express another concept the same way. Not is-a — a node can express many independent properties |
| **N** | gray dotted | NEAR-TO | Similarity / proximity (undirected) | Two same-kind nodes are alike but you do not want to merge them |

## All allowed edges

Every legal source → target combination, matching the diagram above. The "ipmt syntax" column shows the most common form for each edge.

| # | Source → Target | Edge | ipmt syntax | Reads as |
|:-:|:--|:-:|:--|:--|
| 1 | event → event | L | `e1 ::e --> e2 ::e` | e1 leads to e2 |
| 2 | event → event | P | `inner ::e --::P--> outer ::e` | inner event is part of outer event |
| 3 | event → event | X | `e1 ::e --::X--> e2 ::e` | e1 expresses e2 |
| 4 | event — event | N | `e1 ::e --- e2 ::e` | e1 is similar to e2 (and vice versa) |
| 5 | thing → event | P | `tA --> e1 ::e` | tA participates in (is part of) e1 |
| 6 | thing → thing | P | `subpart --> whole` | subpart is part of the whole (physical composition) |
| 7 | thing — thing | N | `tA --- tB` | tA is near / similar to tB (and vice versa) |
| 8 | event → concept | X | `e1 ::e --> cX ::c` | e1 expresses property cX |
| 9 | thing → concept | X | `tA --> cX ::c` | tA expresses property cX |
| 10 | concept → concept | X | `cX ::c --> cY ::c` | cX expresses property cY |
| 11 | concept — concept | N | `cX ::c --- cY ::c` | cX is similar to cY (and vice versa) |

Two important rules baked into this table:

- **No `thing --> thing` arrow except part-of.** To say "Alice owns the car" or "Mike uses his phone," create an **event** — a region of spacetime that co-locates both participants for some duration — and let it express the relation as a concept-property (`Ownership ::c`, `Uses ::c`). This is SST's general handling of arbitrary binary relations: the event is the *temporal* container that brings the two things together; the concept on the event names what that co-location *means*. There is no direct `thing --uses--> thing` edge.
- **The bare `-->` arrow defaults to the relation that fits the two node kinds** — leads-to for event-to-event, part-of for thing-to-event, expresses for thing-to-concept. The explicit `--::L-->`, `--::P-->`, `--::X-->`, `--::N--` forms are documented in the ipmt syntax spec.

## Where to look next

**Worked examples in this repo:**

- [`docs/examples/murder-full.md`](docs/examples/murder-full.md) — a Clue-style murder narrative
- [`docs/examples/meta-ipm.md`](docs/examples/meta-ipm.md) — IPM modeling itself

**ipmt syntax spec:** the formal grammar of the text format — type markers, aliases, arrow forms, edge tooltips, escaping, fence behaviour — lives in a separate document that will be published alongside the open-source `ipm-drawio` release. Until then, the build-up section above plus the worked examples in `docs/examples/` show the vocabulary that covers nearly every model in the wild.

External reading — Mark Burgess ([ResearchGate profile](https://www.researchgate.net/profile/Mark-Burgess-9)) on Semantic Spacetime γ(3,4):

- [Designing Nodes and Arrows in Knowledge Graphs with Semantic Spacetime](https://mark-burgess-oslo-mb.medium.com/designing-nodes-and-arrows-in-knowledge-graphs-with-semantic-spacetime-0992b9cae595) — the source article for the etc / LCEN triangle
- [Semantic Spacetime 1: The Shape of Knowledge](https://mark-burgess-oslo-mb.medium.com/semantic-spacetime-1-the-shape-of-knowledge-86daced424a5) — fast/slow variable separation, why a thing is a *worldline*
- [Knowledge Management series](https://mark-burgess-oslo-mb.medium.com/list/knowledge-management-da2834a25b99) — the full medium series
- [Agent Semantics, Semantic Spacetime, and Graphical Reasoning](https://arxiv.org/abs/2506.07756) — arxiv.org, June 2025; the academic write-up ([ResearchGate mirror](https://www.researchgate.net/publication/392507642_Agent_Semantics_Semantic_Spacetime_and_Graphical_Reasoning))
- [Smart Spacetime: How information challenges our ideas about space, time, and process](https://markburgess.org/smartspacetime.html) — Mark Burgess's book, the long-form treatment

## Related repos

All `infinite.pm` repositories live under the [`infinite-pm` GitHub org](https://github.com/orgs/infinite-pm/repositories).
