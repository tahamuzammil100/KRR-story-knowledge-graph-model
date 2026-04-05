# KRR Story Knowledge Graph — Fixed Ontology Files
## What was fixed
| File | Fix |
|------|-----|
| event.ttl | Removed spatial DisjointWith axiom (caused inconsistency) |
| time.ttl | Removed IrreflexiveProperty from nti:before/after (non-simple) |
| time.ttl | Removed nti:before/after from AllDisjointProperties (non-simple) |
| place.ttl | Removed IrreflexiveProperty from isSubpartOf/hasSubpart (non-simple) |
| place.ttl | Replaced minCardinality with someValuesFrom on transitive property |
| plot.ttl | Fixed owl:AllDisjointClasses blank-node syntax |
| plot.ttl | Removed IrreflexiveProperty from npl:precedes/follows (non-simple) |
| Middle_earth_ontolog_meo.ttl | owl:equivalentTo → owl:equivalentClass |
| Middle_earth_ontolog_meo.ttl | owl:inversOf → owl:inverseOf (typo) |
| Middle_earth_ontolog_meo.ttl | Fixed mojibake encoding (e.g. meo:Lócë) |
| familly_relation_fo.ttl | fo:isTheChildOf → fo:isAChildOf (undefined) |
| familly_relation_fo.ttl | fo:isASibingOf → fo:isASiblingOf (typo) |
| narn_instances.ttl | Fixed mojibake encoding |
| narn_instances.ttl | fo:isASibingOf → fo:isASiblingOf |

## How to load in Protégé
1. Extract ALL files (including catalog-v001.xml) into ONE folder
2. File → Open → select narn_instances.ttl
3. The catalog-v001.xml resolves all imports automatically
4. Reasoner → HermiT → Start Reasoner
