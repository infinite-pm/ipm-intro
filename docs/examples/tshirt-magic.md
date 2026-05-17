# T-shirt magic

ipmt example illustrating the ETC vocabulary defined in the [loops-ipm glossary](https://github.com/infinite-pm/loops-ipm/blob/main/docs/glossary.md).

## Patrick changes t-shirt color

A minimal ipmt story: Patrick wears one t-shirt, then swaps it for another of a different color. Illustrates all three ETC node kinds and the LEADS-TO, CONTAINS, and EXPRESSES relations.

Note: this is an **observer's** account — somebody else watching Patrick, not Patrick's own account. Every ipm model is told from a chosen viewpoint; the observer is implicit but shapes which events and things appear in the graph.

### Overview — just the top event

The coarse-grained view: a single event with the participating things, no sub-events yet.

```ipmt
# Top event
Patrick t-shirts magic ::e tshirtsMagic::a

# Things contained in the event
Patrick --> tshirtsMagic
Patrick --> human ::c

t-shirt B --> tshirtsMagic
t-shirt B --> t-shirt ::c, black ::c

t-shirt W --> tshirtsMagic
t-shirt W --> t-shirt ::c, white ::c
```

### Detail — sub-events

Same scene, expanded into a LEADS-TO chain of sub-events that are part-of the top event.

```ipmt
# Parent event
Patrick t-shirts magic ::e tshirtsMagic::a

# Sub-events (LEADS-TO chain)
Patrick wears t-shirt B ::e wearB::a
  --> Patrick swaps t-shirt ::e swapTshirt::a
  --> Patrick wears t-shirt W ::e wearW::a

# Each sub-event is part of tshirtsMagic (event part-of event)
wearB --::P--> tshirtsMagic
swapTshirt --::P--> tshirtsMagic
wearW --::P--> tshirtsMagic

# Actor: Patrick (a thing) is contained in the parent event and classified as Human
# (transitively contained in each sub-event via CONTAINS)
Patrick --> tshirtsMagic
Patrick --> human ::c

# Two t-shirts (things), each classified as T-shirt and expressing its color
t-shirt B --> wearB, swapTshirt
t-shirt B --> t-shirt ::c, black ::c

t-shirt W --> swapTshirt, wearW
t-shirt W --> t-shirt ::c, white ::c

# Both wearing events express the "Wearing t-shirt" concept;
# the swap event expresses the "Swap t-shirt" concept
wearB --> wearing t-shirt ::c
wearW --> wearing t-shirt ::c
swapTshirt --> swap t-shirt ::c
```

## Zooming into the swap event

A swap is made of taking off one t-shirt and taking on the other. This shows event-as-container via part-of (`--::P-->`):

```ipmt
Patrick --> Patrick swaps t-shirt swapTshirt::a ::e --> swap t-shirt ::c
Patrick --> human ::c

Patrick wears t-shirt B wearB::a ::e --::P--> swapTshirt
Take off t-shirt B takeOffB::a ::e --::P--> swapTshirt
Patrick half-naked halfNaked::a ::e --::P--> swapTshirt
Take on t-shirt W takeOnW::a ::e --::P--> swapTshirt
Patrick wears t-shirt W wearW::a ::e --::P--> swapTshirt
wearB --> takeOffB --> halfNaked --> takeOnW --> wearW

# What each sub-event expresses
wearB --> wearing t-shirt ::c
takeOffB --> taking off ::c
halfNaked --> half naked ::c
takeOnW --> taking on  ::c
wearW --> wearing t-shirt ::c

# Things contained in the sub-events
t-shirt B --> wearB, takeOffB, t-shirt ::c
t-shirt W --> takeOnW, wearW, t-shirt ::c
```

## Alternative observation — black worn over white

Same top-level event (`tshirtsMagic`) — what differs is **which sub-events the observer saw**. Here the observer noticed Patrick was already wearing both t-shirts (black over white), and saw only the black one being taken off — no take-on. The white t-shirt persists throughout.

```ipmt
# Top event (same name as the first observation)
Patrick t-shirts magic ::e tshirtsMagic::a

# Sub-events (LEADS-TO chain): wear black over white -> takes off black -> wear white
Patrick wears t-shirt B (over t-shirt A) ::e wearLayered::a
  --> Take off t-shirt B ::e takeOffB::a
  --> Patrick wears t-shirt W ::e wearW::a

# Sub-events are part of the top event
wearLayered --::P--> tshirtsMagic
takeOffB --::P--> tshirtsMagic
wearW --::P--> tshirtsMagic

# Actor
Patrick --> tshirtsMagic
Patrick --> human ::c

# White t-shirt is worn throughout
t-shirt W --> wearLayered, wearW
t-shirt W --> t-shirt ::c, white ::c

# Black t-shirt is on during the layered wearing and is being removed in takeOffB
t-shirt B --> wearLayered, takeOffB
t-shirt B --> t-shirt ::c, black ::c

# What each event expresses
wearing two t-shirts ::c --> wering layered ::c
wearLayered --> wearing two t-shirts ::c --> wearing t-shirt ::c
takeOffB --> taking off ::c
wearW --> wearing t-shirt ::c
```

## Observation is open-world

An ipmt observation records what was *seen*, not what was absent — two observations can differ without contradicting each other. To decide which scenario above actually happened, the observer needs **positive evidence** for one of the discriminating shapes. A single sighting is enough.

```ipmt
# Confirms scenario 2 (layered): both t-shirts co-present on Patrick at the same moment
Both t-shirts seen on Patrick ::e probeBoth::a
Patrick --> probeBoth
t-shirt B --> probeBoth
t-shirt W --> probeBoth
```

```ipmt
# Confirms scenario 1 (exchange): t-shirt W observed being taken on (a positive transition)
Take-on of t-shirt W observed ::e probeTakeOnW::a
Patrick --> probeTakeOnW
t-shirt W --> probeTakeOnW
probeTakeOnW --> taking on ::c
```

Without either probe succeeding, the scenario stays undecided — the honest open-world answer.

## Color taxonomy

White and Black are kinds of Color — a concept-to-concept EXPRESSES relation:

```ipmt
white ::c --> color ::c
black ::c --> color ::c
```

## Thing taxonomies

```ipmt
t-shirt T1 --> t-shirt ::c --> clothes ::c --> human thing ::c
human thing ::c --> thing ::c
human thing ::c --- human ::c

stone S1 --> stone ::c --> natural thing ::c --> thing ::c
natural thing ::c --- nature ::c
```
