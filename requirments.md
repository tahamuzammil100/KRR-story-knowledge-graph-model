# Knowledge Representation and Reasoning: Instructions for Homework

## Modelling story plots

This page contains instructions on the exercise on knowledge representation. The goal is to provide a knowledge model to describe information related to story plots (that could be fiction or historical events). The goal is provide enough knowledge in sufficiently precise way that story elements can be identified, retrieved, analysed easily. From fragmentary descriptions of events, it should be possible to reconstruct (at least in part) the timeline of the story, whether there are inconsistencies such as a character appear at 2 different places at the same time, etc.

The delivery consists in providing a formal specification (an _ontology_) in the standard [Web Ontology Language](https://www.w3.org/TR/owl2-overview/) (OWL). OWL files can be generated using [Protégé](https://protege.stanford.edu/), an ontology editor from Stanford University, but other methods of creating the files can be used, such as editing the code directly, with the help of an AI assistant if needed.

## Use case

During the session, we rely on a specific story that illustrates features of knowledge representation formalisms and technologies: the _Narn i Chîn Húrin_ (meaning _Tale of the Children of Húrin_ in the invented language Sindarin) which was published as a standalone book in 2007. We will refer to this story as the _Narn_. The tale has a good number of characters of very different types and roles, has events that occur at different places at times that sometimes overlap, has plot twists, etc. that makes it adequate to illustrate many challenges of knowledge representation. These challenges, in turn, can be extrapolated to cover other stories, and more importantly, to describe events of real life involving real people in real places. Historical knowledge bases are indeed an important use case for knowledge representation.

## Knowledge Model

The _knowledge model_ in this exercise corresponds to the ontology or ontologies that define the generic classes and properties that characterise the domain of story plots. It is very unlikely that you need to introduce instances at the level of the _knowledge model_. In your homework, instances should only exist to exemplify how to instantiate the classes and properties of your knowledge model.

### Modelling characters

Characters in stories are mostly people, but in cases of fantasy fiction, there may be animal characters, aliens, races that are different altogether from humans. This is the case in the _Narn_, where the tale involves a mix of humans (the _Atani_), elves (the _Quendi_), dwarves (the _Naugrim_), orcs (the _Yrch_), angelic powers (the _Maiar_ and the _Valar_), and a dragon (a _lócë_).

The types of characters and peoples in the world of the _Narn_ are organised in hierarchies: there are immortal and mortal races, there are different ethnical groups of _Atani_, _Quendi_, and _Naugrim_, etc.

The knowledge about peoples in the _Narn_ is contained in the [Middle-earth ontology](https://www.emse.fr/~zimmermann/Teaching/KRR/Homework/meo.ttl) provided by the teacher.

In addition, characters have relations between them that can be familial or social. A [separate ontology module about family relations](https://www.emse.fr/~zimmermann/Teaching/KRR/Homework/fo.ttl) is given to illustrate some features of the ontology language, as seen in [Session 3](https://www.emse.fr/~zimmermann/Teaching/KRR/LabWork/3).

You should add a module that has social relations (exemplified in the given description of the _Narn_ with terms where prefix `loc:` is used).

### Modelling places

A separate module of places must be provided. There are very general spatial relationships that can exist between places. The simplest of them is the "subpart" relation (e.g., Saint-Étienne is a subpart of _département de la Loire_). You have to introduce general spatial relations in this module.

Additionally, places can be organised in hierarchies. Such hierarchies may be story-specific but can be very general too. For instance, we can distinguish settlements from wild areas, as distinct subtypes of places.

As part of the ontology of places, there can be spatial relations according the Region Connection Calculus, as provided in [the RCC ontology](https://www.emse.fr/~zimmermann/Teaching/KRR/Homework/rcc.ttl) from [Session 4](https://www.emse.fr/~zimmermann/Teaching/KRR/LabWork/4) of the course.

### Events

This is the most interesting and complex part. Events occur at specific time points or during a period of time. We may not know the exact duration, starting time and ending time of an event, but we know when they occur with respect to another event (before, after, during, etc.). Events occur at places and involve characters.

Defining relations between events, as well as relations between events and places and characters is the main part of this homework. Events can also be organised in hierarchies (e.g., wars, meetings, births are types of events). Provide an event hierarchy as needed.

The temporal aspect of events can be modelled by relying on [Allen's temporal algebra](https://www.emse.fr/~zimmermann/Teaching/KRR/Homework/allen.html), as seen in [Session 5](https://www.emse.fr/~zimmermann/Teaching/KRR/LabWork/5). Going further than Allen's algebra, you can reuse the standard [Time Ontology in OWL](https://www.w3.org/TR/owl-time/) recommended by the W3C.

Events are central to a lot of knowledge representation and there have been several examples of event ontology that you could start from or reuse: The [Event Ontology](https://motools.sourceforge.net/event/event.html) of the BBC, the [Event Ontology](https://w3id.org/MON/event.owl) from the MARIO project, or the [event model from schema.org](https://schema.org/Event).

### Plot structure

Beyond the internal entities and events of the story from the point of view of characters inside the fictitious world, we may want to define how the story itself is structured, from a narrative or literary point of view. This part requires some research or interaction with experts or with a proxy for experts, namely an AI chatbot. Provide properties and classes that fill in this requirement as well as what interactions you had with your AI tool.

### Actions

A possible approach to describing a story plot is by describing actions. It is not obligatory, because depending on the ontological viewpoint, actions could be simply described as events, but to be more precise and have a richer knowledge representation, actions should be considered with their own characteristics. For this part especially, it is good to talk with an expert. In the absence of an actual expert in the ontology of events and actions, you will rely on a chatbot that you have to employ in a conversation in order to reach a knowledge module for that.

## Instructions

Your work will be delivered individually. You will deliver several files: _ontology files_ in Turtle that correspond to the modules mentioned above (place, space, time, event, family, plot); the _documentation_ that goes with it, preferably in HTML but possibly in PDF or (worse) MS Word or OpenOffice writer; and a separate Turtle file that shows a concrete example of data instantiating and illustrating all parts of your model. This latter file can extend the files provided for the description of the _Narn_.

### The ontology file

The OWL ontology should provide classes and properties related to the different aspects of plot descriptions.

#### Competency questions

Using your ontology, it **should** be possible to answer the following competency questions:

- Who is parent of _X_? married to _X_? relative to _X_?
- Where did character _X_ go during the story?
- Who was involved in event _E_?
- Did event _E1_ happen before event _E2_?
- Where did event _E_ occurred?
- Is it possible to be in location _L1_ and _L2_ at the same time?
- What event ends story _S_?
- What item was used as part of event _E_ (or action _A_)?
- ...write your own competency questions?

#### Organise your ontology well

Separate concerns as much as possible. This can be apparent by documenting different aspects of your knowledge model in different sections.

#### Add rich axioms

The extensiveness of the coverage is not essential in this work. I will value much more a small ontology with few classes and properties but rich and complex axioms. Make use of the complex concept constructs. Identify interesting knowledge that constrain how your ontology terms could be interpreted.

### The documentation

The documentation must contain natural language labels for all the terms defined in the ontology, and a textual description of what the terms mean (you can use Protégé annotations with `rdfs:label` and `rdfs:comment`). The documentation must contain examples of usage of the terms you introduce. Additionally, any amount of details about the design choices can be given in the introduction of the documentation. The way AI tools were used can also add from the point of view of assessing your work.

The text of the documentation can be entirely embedded in the ontology file (better) and the documentation can be generated automatically from the ontology file, using tools such as [WIDOCO](https://github.com/dgarijo/Widoco). You can also use the online service [LODE](https://essepuntato.it/lode/). Otherwise, you can write your documentation from scratch in a document (HTML preferred, possibly PDF, avoid word processor formats).

### The instance file

A Turtle file with instances that illustrate all the things from your model must be provided.

For this, you will extend the example file given during the course.

### Delivery

Deadline for delivery: **April 5th, 2026**

The ideal way to deliver your work is by using a Git repository. It is also advisable to use Git to collaborate on the files, if you are familiar with it. Otherwise, use a file hosting service. Send me the link by email before the deadline. Make sure that files delivered by way of a link to the Web are kept available for long enough.

---

_last modified 2026/03/04 11:42:42 by Antoine Zimmermann_
