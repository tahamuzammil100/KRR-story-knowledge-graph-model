# KRR Story Knowledge Model

An OWL 2 ontology for modelling story plots in [Turtle](https://www.w3.org/TR/turtle/) format.

The running example is the *Narn i Chîn Húrin* (*Tale of the Children of Húrin*) by J.R.R. Tolkien — a story rich enough in characters, places, overlapping events, and plot twists to illustrate the full power of knowledge representation formalisms.

---

## Repository structure

```
.
├── familly_relation_fo.ttl       # Given: family relations ontology (fo:)
├── Middle_earth_ontolog_meo.ttl  # Given: Middle-earth races & characters (meo:)
├── rcc.ttl                       # Given: Region Connection Calculus RCC8 (rcc:)
│
├── place.ttl                     # Place hierarchy & spatial relations (npo:)
├── social.ttl                    # Social relations between characters (loc:)
├── time.ttl                      # Time intervals & Allen's algebra (nti:)
├── event.ttl                     # Event hierarchy & relations (nev:)
├── action.ttl                    # Action ontology (nac:)
├── plot.ttl                      # Narrative/plot structure (npl:)
│
├── narn_instances.ttl            # Concrete instances from the Narn (narn:)
│
├── index.html                    # Full HTML documentation
└── README.md
```

---

## Ontology modules

### Given modules (provided by the course)

| File | Prefix | Description |
|------|--------|-------------|
| `familly_relation_fo.ttl` | `fo:` | Family relations: isMarriedTo, isAParentOf, isASonOf, isADaughterOf, isASiblingOf |
| `Middle_earth_ontolog_meo.ttl` | `meo:` | Middle-earth races (Adan, Elda, Maia, Vala, Lócë, EvilBeing) and named individuals |
| `rcc.ttl` | `rcc:` | RCC8 spatial relations: dc, ec, po, tpp, ntpp and their inverses |

### Authored modules

| File | Prefix | Description |
|------|--------|-------------|
| `place.ttl` | `npo:` | Place hierarchy and spatial relations |
| `social.ttl` | `loc:` | Social relations between characters |
| `time.ttl` | `nti:` | Temporal concepts and Allen's 13 interval relations |
| `event.ttl` | `nev:` | Event hierarchy, participants, and causal links |
| `action.ttl` | `nac:` | Actions as intentional/unintentional events with agents, patients, and instruments |
| `plot.ttl` | `npl:` | Narrative structure: Freytag pyramid, arcs, subplots |
| `narn_instances.ttl` | `narn:` | Concrete data instantiating all modules using the Narn story |

---

## Module descriptions

### Place (`place.ttl` — `npo:`)

Defines a hierarchy of place types rooted in RCC8's `Region`:

- **Settlement** (City, Fortress) — disjoint with WildArea
- **WildArea** (Forest, Mountain)
- **Cavern**, **River**, **GeographicRegion**

Key spatial properties:
- `npo:isSubpartOf` / `npo:hasSubpart` — transitive, irreflexive; sub-property of `rcc:ntpp`
- `npo:borders` — symmetric; sub-property of `rcc:ec`
- `npo:isLocatedIn` — transitive; general containment
- `npo:isDisconnectedFrom` — symmetric; sub-property of `rcc:dc`
- `npo:hasCapital` — links a geographic region to its principal settlement

Rich axioms enforce that a Cavern inside a Settlement becomes an underground settlement (e.g. Menegroth), and that GeographicRegions must contain at least one place.

---

### Social Relations (`social.ttl` — `loc:`)

Complements the given family ontology with non-familial bonds. Uses the `loc:` prefix as required by the story description conventions.

Classes: `SocialGroup`, `Kingdom`, `MilitaryUnit`, `Fellowship`, `HouseOfMen`

Key properties:
- `loc:isAllyOf` / `loc:isEnemyOf` — symmetric, declared disjoint (one cannot be both)
- `loc:isLordOf` / `loc:isVassalOf` — inverse pair; transitive feudal hierarchy
- `loc:isMentorOf` / `loc:isProtégeOf` — inverse pair
- `loc:isMemberOf` / `loc:hasMember` — character–group membership
- `loc:isFriendOf` — symmetric personal bond
- `loc:isBetrayedBy` / `loc:betrays` — inverse pair
- `loc:owesAllegianceTo` — derived via property chain: `isMemberOf ∘ isLordOf`

---

### Time (`time.ttl` — `nti:`)

Provides `TimeInstant` and `TimeInterval` (disjoint), and all **13 Allen interval relations** with their inverses declared:

`before/after`, `meets/metBy`, `overlaps/overlappedBy`, `during/contains`, `starts/startedBy`, `finishes/finishedBy`, `equals`

All 13 relations are declared pairwise disjoint and as sub-properties of a common `nti:hasTemporalRelation` super-property. `before` and `after` are transitive and irreflexive. `TimeInterval` is constrained to exactly one `hasBeginning` and one `hasEnd` value.

---

### Event (`event.ttl` — `nev:`)

The central module. Event hierarchy:

`Event` → Battle, War, Journey, Meeting, Birth, Death, Exile, Betrayal, Curse, Capture, Rescue

Key properties:
- `nev:occursAt` — links event to place (every event must have at least one)
- `nev:involvesCharacter` / `nev:hasSubject` / `nev:hasAgent` — participant roles
- `nev:hasTemporalExtent` — links event to a `nti:TimeInterval`
- `nev:causedBy` / `nev:resultsIn` — causal chain between events
- `nev:isPartOf` / `nev:hasPart` — event composition (e.g. battles within a war)
- `nev:precedes` / `nev:follows` — event ordering; sub-properties of `nti:before/after`
- `nev:hasDeparturePlace` / `nev:hasArrivalPlace` — specialised for Journey
- `nev:hasItem` — artefact or object used in an event

Key axioms:
- Battle must involve at least one `meo:EvilBeing`
- Birth and Death have exactly one subject
- War must contain at least one Battle
- Journey has exactly one departure and one arrival place
- Events at disconnected places cannot be simultaneously occupied by the same character

---

### Action (`action.ttl` — `nac:`)

Actions are a sub-type of Event performed by an agent.

Hierarchy: `Action` → `IntentionalAction` / `UnintentionalAction` (disjoint), `PhysicalAction` → `ViolentAction`, `SpeechAct`, `CoerciveAction`, `MentalAction`

Key properties:
- `nac:hasAgent` — the performing character (min 1)
- `nac:hasPatient` — the affected character
- `nac:hasPurpose` — goal of an intentional action (min 1)
- `nac:hasInstrument` — the item used (answers: *what item was used in event E?*)
- `nac:hasResult` — resulting event or state

Item hierarchy: `Item` → `Weapon`, `Artefact`

Axioms: every Action has at least one agent; every IntentionalAction has at least one purpose; ViolentAction requires a patient; intentional violent acts classify as CoerciveAction.

---

### Plot Structure (`plot.ttl` — `npl:`)

Models the story from a *narrative* (extra-diegetic) viewpoint using the **Freytag pyramid**:

`PlotPoint` → Exposition → RisingAction → Climax → FallingAction → Resolution (all pairwise disjoint)

Classes: `Story`, `Chapter`, `PlotArc`, `Subplot`, `Tragedy`

Key properties:
- `npl:hasPlotArc` / `npl:hasPlotPoint` — structural composition
- `npl:beginsWithEvent` / `npl:endsWithEvent` — links narrative structure to in-world events
- `npl:hasProtagonist` / `npl:hasAntagonist`
- `npl:hasClimax` — every Story has exactly one Climax
- `npl:correspondsToEvent` — links a PlotPoint to its in-world Event
- `npl:hasFatalFlaw` — specific to Tragedy

Axioms enforce the Freytag ordering: Exposition → Rising → Climax → Falling → Resolution.

---

### Instances (`narn_instances.ttl` — `narn:`)

Illustrates all modules using characters, places, times, events, actions, social relations, and plot structure from the *Narn i Chîn Húrin*.

**Characters:** Húrin, Morwen, Túrin, Nienor, Beleg, Finduilas, Glaurung, Melian, Thingol, Brandir, Mablung

**Places:** Beleriand, Dor-lómin, Doriath, Menegroth, Nargothrond, Brethil, Angband, Dimbar

**Events (chronological):** Nirnaeth Arnoediad (FA 472) → Capture of Húrin → Morgoth's Curse → Túrin's exile → Death of Beleg → Fall of Nargothrond (FA 496) → Glaurung's curse on Nienor → Death of Finduilas → Túrin slays Glaurung → Death of Nienor → Death of Túrin (FA 499)

**Actions:** Túrin's accidental killing of Beleg (UnintentionalAction), Morgoth's curse (SpeechAct + CoerciveAction), Túrin's suicide with Gurthang (IntentionalAction + ViolentAction)

**Plot arc:** Full Freytag pyramid mapped to in-world events; the story is typed as a `npl:Tragedy`.

---

## Competency questions

The ontology is designed to answer:

| Question | Module |
|----------|--------|
| Who is the parent / spouse / sibling of X? | `fo:`, `narn_instances.ttl` |
| Where did character X go during the story? | `nev:`, `npo:` |
| Who was involved in event E? | `nev:involvesCharacter` |
| Did event E1 happen before E2? | `nti:before`, `nev:precedes` |
| Where did event E occur? | `nev:occursAt` |
| Can a character be in two disconnected places at the same time? | `npo:isDisconnectedFrom` + `nev:` axiom |
| What event ends story S? | `npl:endsWithEvent` |
| What item was used in event E / action A? | `nac:hasInstrument`, `nev:hasItem` |
| Is X ally / enemy / vassal of Y? | `loc:` |
| What is the climax of story S? | `npl:hasClimax` |

---

## Documentation

Open `index.html` in a browser for the full documentation including design rationale and usage examples per module.
