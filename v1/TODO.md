# TODOs

> IMPORTANT : this file (TODO.md) will be deleted if profile is finalized

## TODO

### https://en.wikipedia.org/wiki/ISO_8601

https://en.wikipedia.org/wiki/ISO_8601


### 8. Making an ODRL Profile publicly available
   If an ODRL Profile should be used by a public audience it is highly recommended to make its spefications publicly accessible:

- A human-readable specification as HTML web document
- An OWL Ontology as resource using a common Semantic Web format, like RDF/Turtle, RDF/XML, RDF/N-Triples, or JSON-LD
- A resource using the W3C Profile Vocabulary in a common Semantic Web format, like RDF/Turtle, RDF/XML, RDF/N-Triples, or JSON-LD
- If the JSON-LD form should be supported for ODRL Policies a JSON-LD Context resource.

All these resourced can be made accessible by URLs.

An alternative option is based on http request-based content negotiation, this feature must be supported by the web server delivering the documents. In this case a generic URL is defined for the human readable HTML document and the OWL Ontology in Semantic Web formats. Depending of the IANA Media Type expressed by the accept-header of the http(s) request the corresponding resource is delivered by the http(s) response.

The URL(s) used for such resources should be persistent over time. The publisher of a Profile should consider whether to reflect the version of the Profile in the URL or to use version-agnostic URLs.

---

### 9. Registering a profile with the ODRL Community Group

The ODRL Community Group provides a list of registered ODRL 2.2 Profiles at https://www.w3.org/community/odrl/profile/

Contact this group by email public-odrl@w3.org and provide these details of the profile:

- Business name of the profile
- Name and web URL of the party having created and planning to maintain the profile
- Identifier of the profile
- URL of the human-readable specification document
- URL of the OWL Ontology and the name of the used format (e.g. RDF/Turtle, RDF/XML, JSON-LD)
- Optional: URL of the JSON-LD context resource
- Optional: URL of the W3C Profile Vocabulary resource

---

### Candidate Recommendation Exit Criteria

> FROM <https://www.w3.org/TR/odrl-model/#cr-exit>

For this specification to be advanced to Proposed Recommendation, there must be at least two independent implementations of each feature described below. Each feature may be implemented by a different set of products, and there is no requirement that any single product implement every feature.

Features

For the purposes of evaluating exit criteria, the following are considered as features:

- A Set/Offer/Agreement Policy type with required properties
- A Policy that utilises an ODRL Profile
- A Policy with an Asset Collection, including parts
- A Policy with a Party Collection, including parts
- A Policy with a Rule including a constraint property
- A Policy with a Permission including a duty property
- A Policy with a Permission including a duty and a consequence property
- A Policy with a Prohibition
- A Policy with a Prohibition including a remedy property
- A Policy with an Obligation
- A Policy with a refinement property on an Action, Asset and Party Collection
- A Policy with a Logical Constraint
- A Compact Policy that requires translation into an Atomic Policy
- A Policy containing metadata
- A Policy that includes Policy inheritance
- A Policy that includes a Conflict Strategy

Software that does not alter its behavior in the presence or lack of a given feature is not deemed to implement that feature for the purposes of exiting the Candidate recommendation phase.

---

## Work in Progress

## Backlog

## DONE

---