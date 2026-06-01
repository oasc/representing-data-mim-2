# Mechanisms

### M1 Smart Data Models with NGSI-LD

#### 1. Overview

This Mechanism defines how public sector data systems can represent, document, validate, and transform data in an interoperable way using **Smart Data Models** as the canonical data model layer, expressed as **NGSI-LD** entities with **JSON Schema** definitions and **JSON-LD `@context`** files. It fulfils all capabilities and requirements of MIM2 (Representing Data).

Smart Data Models is a joint initiative by FIWARE, TM Forum, IUDX, and OASC that seeks to harmonise data models across smart applications. The initiative defines models grouped by subject and domain, with each model consisting of a JSON Schema, a human-readable specification, a URI-resolvable attribute registry, and NGSI-LD payload examples — all under a royalty-free licence. [data-models](https://smart-data-models.github.io/data-models/)

Where direct adoption of an existing Smart Data Model is not possible, the Mechanism provides a structured path for extending existing models or defining new ones, using a three-phase **ontology alignment pipeline** (detection → representation → execution) to bridge heterogeneous legacy models into a common model.

***

#### 2. Core Standards Referenced

| Standard                                                     | Role in this Mechanism                                                                                                                         |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **ETSI NGSI-LD** (ETSI GS CIM 009)                           | Information model and API for context entities; the structural backbone for all Smart Data Models                                              |
| **JSON Schema (Draft 2020-12)**                              | Machine-readable schema definition for each data model; enables automated validation                                                           |
| **JSON-LD 1.1** (W3C Rec)                                    | Serialisation format linking JSON field names to globally unique IRIs via `@context`; makes every attribute semantically unambiguous           |
| **Smart Data Models initiative** (smartdatamodels.org)       | Curated library of subject-specific data models across smart city domains, each with schema, specification, context file, and payload examples |
| **SKOS** (W3C Rec)                                           | Lightweight concept mapping (`skos:exactMatch`, `skos:broadMatch`) for cross-model alignment                                                   |
| **SSSOM** (Simple Standard for Sharing Ontological Mappings) | TSV/JSON format for publishing, versioning, and sharing alignment mappings between models with full provenance metadata                        |
| **RML / R2RML** (W3C Rec / community spec)                   | Declarative mapping rules for transforming data instances between models; executed by engines such as RMLMapper and Morph-KGC                  |
| **SPARQL 1.2 CONSTRUCT** (W3C)                               | Graph rewriting queries that transform source-vocabulary triples into target-vocabulary triples, consumable by any SPARQL endpoint             |
| **SAREF / SAREF4Cities** (ETSI)                              | Reference ontology for smart devices and smart city concepts; declared as alignment target in `@context` files                                 |
| **W3C SOSA/SSN**                                             | Sensor, observation, and actuator ontology; referenced in Smart Data Models for environmental and IoT domains                                  |
| **ISO/IEC 5087-1:2023** (City Data Model)                    | Foundation-level city data model; used as upper alignment target for entity type hierarchies                                                   |
| **RFC 9110** (IETF)                                          | HTTP semantics governing content negotiation for multi-format serialisation delivery                                                           |

***

#### 3. Mechanism Description

**3.1 Data Model Structure: The Smart Data Model Artefact Set**

Every data model conforming to this Mechanism consists of a standardised set of four artefacts, mirroring the Smart Data Models programme structure:

**1. JSON Schema** (`schema.json`): A JSON Schema 2020-12 document defining the technical structure of the data model — property names, data types, cardinality, enumeration values, units of measurement, and required vs. optional fields. Units are expressed using UN/CEFACT unit codes (the `unitCode` property in NGSI-LD), and datetime fields follow ISO 8601 / RFC 3339. The schema covers the "key-value" (simplified) representation; the normalised NGSI-LD representation is covered by the `@context`.

**2. JSON-LD `@context` file** (`context.jsonld`): A JSON-LD 1.1 context document that maps every property name in the schema to a globally unique IRI. Each subject repository in the Smart Data Models programme contains a `context.jsonld` at its root, providing an unambiguous IRI mapping for all terms within that subject. Every IRI is resolvable: dereferencing it returns the attribute's human-readable specification and machine-readable metadata. The `@context` also declares alignments to external vocabularies such as SAREF, SOSA/SSN, and schema.org using `skos:exactMatch` or `owl:equivalentProperty`. [data-models](https://smart-data-models.github.io/data-models/)

**3. Human-readable specification** (`DESCRIPTION.md` / `spec.html`): A written document for human readers covering the entity type's purpose, attributes (with description, type, allowed values, and unit), relationships to other entity types, and worked examples. This constitutes the "descriptive metadata" required by R1.1.

**4. Payload examples**: Concrete JSON and NGSI-LD normalised examples (`example.json`, `example-normalized.jsonld`) that illustrate real payloads, serving as test fixtures for validation and as onboarding material for integrators.

This four-artefact structure ensures that a data model is simultaneously human-readable, machine-validatable, semantically unambiguous, and directly usable in NGSI-LD context brokers.

**3.2 Selecting and Adopting an Existing Smart Data Model (R1.2a)**

For any new data-sharing initiative, the first step is to survey the Smart Data Models catalogue at `smartdatamodels.org`. Data models are organised into subjects (each a Git repository) and those subjects belong to one or more domains representing industrial sectors. Relevant domains for smart cities include Smart Environment, Smart Cities, Smart Energy, Smart Mobility, Smart Water, and Cross-Sector. [FIWARE](https://www.fiware.org/smart-data-models/)

When an applicable model exists, it is adopted as-is. The adopting system:

* References the canonical `context.jsonld` from the Smart Data Models repository (or hosts a local copy for firewall-constrained deployments)
* Validates all outgoing payloads against the published `schema.json` using a JSON Schema validator
* Publishes its entity IDs as NGSI-LD URNs: `urn:ngsi-ld:{EntityType}:{localId}`
* Includes the `@context` reference in every NGSI-LD entity, either inline or via the HTTP `Link` header

**3.3 Extending an Existing Model or Creating a New One (R1.2b)**

Where no suitable model exists, the Mechanism provides two extension patterns:

**Subject-level extension**: A new `schema.json` is created that includes all properties of the closest existing model via JSON Schema `$ref` or `allOf` composition, and adds the domain-specific properties. The new model is contributed back to the Smart Data Models programme following the contribution checklist, so it becomes a community asset. The new `@context` extends the parent context file and adds new IRI mappings for the additional properties.

**Application Profile (C4)**: A lightweight Application Profile is defined as a separate SHACL shape or JSON Schema `if/then` overlay that constrains the base model for a specific deployment context — for example, mandating `location` on every `AirQualityObserved` entity within a particular data space. The Application Profile references but does not modify the base model's `schema.json` or `@context`, ensuring non-breaking extension (R4.1). The profile's constraints and any additional properties are documented separately (R4.2).

**3.4 Cross-Ecosystem Model Transformation: The Ontology Alignment Pipeline (C2)**

Where multiple systems in a data ecosystem use different models for the same entity type, the Mechanism defines a three-phase alignment pipeline — directly drawing on the ASKEM MIM2 ontology alignment framework:

**Phase 1 — Detection: Finding Correspondences**

Candidate mappings between a source model and the Smart Data Model target are identified through a combination of techniques, applied in order of increasing cost:

**Lexical / string matching**: Property labels are compared using string similarity metrics (Levenshtein distance, Jaccard overlap, n-gram comparison) and synonym lookup. This is fast and catches obvious cases such as `temperatura` ↔ `temperature`.

**Structural / graph matching**: The topology of the two schemas is compared — shared sub-types, property domains and ranges, cardinality constraints. Two properties with similar "neighbourhoods" in the schema graph are likely equivalent.

**Embedding-based matching**: Property labels and descriptions are encoded as sentence embeddings (e.g. using Sentence-BERT) and compared by cosine similarity. This captures semantic proximity even when labels are lexically dissimilar, such as `AirQualityIndex` ↔ `PollutionLevel`.

**LLM-assisted alignment**: For complex (1-to-N) correspondences — where one source concept maps to multiple target properties or requires a computation — an LLM is provided with the source and target property definitions, their schema contexts, and any available axioms, and asked to reason about the relationship. This is particularly effective for alignments that would previously have required a domain expert.

Hybrid systems (LogMap, AML, OntoAligner) combining lexical, structural, and ML-based matching are the recommended tooling for production use, as they aggregate evidence from multiple matchers and apply consistency repair.

**Phase 2 — Representation: Expressing the Mappings**

Detected correspondences are published in two complementary formats:

**SSSOM (TSV/JSON)**: SSSOM provides a machine-readable and extensible vocabulary to describe metadata that makes imprecision, inaccuracy and incompleteness in mappings explicit, with a simple table-based format that integrates into existing data science pipelines and aligns with Linked Data principles. Each row in an SSSOM file records: `subject_id` (source IRI), `predicate_id` (the SKOS relation), `object_id` (target IRI), `confidence`, `mapping_justification`, and `mapping_tool`. SSSOM files are versioned in Git alongside the data model artefacts. [arxiv](https://arxiv.org/pdf/2112.07051)

**SKOS mapping properties in the `@context`**: Direct one-to-one correspondences are also expressed as `skos:exactMatch` or `skos:closeMatch` annotations within the JSON-LD `@context` or in a companion RDF mapping graph. This makes them directly queryable and traversable by Linked Data clients without needing to parse SSSOM files.

**OWL axioms** (for formal equivalences): Where two properties are provably logically equivalent — confirmed by a Description Logic reasoner — `owl:equivalentProperty` or `owl:equivalentClass` axioms are added to the alignment ontology. This is reserved for well-formalised cases where automated reasoning is intended.

**Phase 3 — Execution: Transforming Data Instances**

The mappings drive three complementary transformation mechanisms:

**RML mapping rules**: SSSOM correspondences are translated into RML (RDF Mapping Language) rules, which declaratively specify how source data fields map to target NGSI-LD properties. Engines such as RMLMapper or Morph-KGC execute these rules on live data streams or batch exports, producing NGSI-LD payloads conforming to the target Smart Data Model.

**SPARQL CONSTRUCT queries**: Each mapping correspondence becomes a `CONSTRUCT` pattern that rewrites triples from the source vocabulary into the target vocabulary. This is particularly suitable for systems that already expose a SPARQL endpoint (in line with the MIM2 Linked Data Mechanism), and allows transformation to be composed with filtering and enrichment in a single query.

**LLM-assisted rule generation**: For complex transformations, an LLM generates draft RML rules or SPARQL CONSTRUCT queries from natural-language descriptions of the correspondence. A human validator reviews and approves the generated rules before they are executed in production. This hybrid human-AI workflow is appropriate for cases where correspondences involve unit conversion, structural reshaping, or semantic reinterpretation.

**3.5 Multi-Format Serialisation (C3)**

Each Smart Data Model supports multiple serialisation formats, all encoding the same information content without loss:

| Format                             | MIME Type                          | Use Case                                    |
| ---------------------------------- | ---------------------------------- | ------------------------------------------- |
| **NGSI-LD normalised**             | `application/ld+json`              | Native FIWARE/context broker exchange       |
| **NGSI-LD simplified (key-value)** | `application/json` + `Link` header | Lightweight REST API consumption            |
| **Turtle**                         | `text/turtle`                      | RDF store ingestion, Linked Data publishing |
| **CSV**                            | `text/csv`                         | Bulk export, spreadsheet tooling            |
| **GeoJSON**                        | `application/geo+json`             | GIS tooling, map visualisation              |

Format selection follows HTTP content negotiation (RFC 9110) using the `Accept` header, as specified in the MIM1 Accessing Data Mechanism. The `@context` link is propagated across formats via the HTTP `Link` header, ensuring semantic annotations are not lost in simplified representations.

Validation is schema-based: the published `schema.json` is used with any JSON Schema 2020-12 validator (e.g. AJV, jsonschema-rs). The Smart Data Models programme provides an online validation API (`pysmartdatamodels`) and a payload validation endpoint for NGSI-LD payloads, lowering the barrier to compliance testing.

**3.6 Cataloguing and Discoverability (R1.1)**

All data models used in a deployment MUST be registered in a machine-readable data catalogue. The catalogue entry for each model includes:

* A URI linking to the canonical `schema.json` and `context.jsonld`
* The version of the model in use
* The NGSI-LD entity type(s) covered
* A `dcat:Dataset` or `dcat:DataService` record linking the model to the data source that uses it

This catalogue is expressed as a DCAT-AP 3 compliant metadata record, linking the data offering (covered by MIM1) to its data model (MIM2) and to its interlinking context (MIM3/former MIM2). DCAT-AP's `dct:conformsTo` property points to the Smart Data Model URI; this makes models programmatically discoverable by data space catalogues and aggregators.

**3.7 Why This Mechanism Is Interoperable**

**Structural interoperability** is achieved by grounding all data in the NGSI-LD property graph model, which is an ETSI standard built on JSON-LD and RDF. Any NGSI-LD compliant context broker — Orion-LD, Scorpio, Stellio — can ingest payloads from any system following this Mechanism, without custom connectors.

**Semantic interoperability** is achieved by the mandatory `@context` file, which maps every JSON property name to a globally unique IRI. Two systems using the same Smart Data Model share the same IRI-level semantics, making their data mergeable without ambiguity. Cross-model alignment via SKOS and SSSOM extends this to systems using different but mappable models.

**Syntactic interoperability** is provided by JSON Schema validation: any system can verify that an incoming payload conforms to the expected data model before processing it, catching integration errors at the boundary.

**Transformation interoperability** is provided by the alignment pipeline. Even where systems cannot adopt the same model directly, the SSSOM + RML or SPARQL execution path provides a standardised, reproducible, and versionable transformation that any competent team can implement, audit, and update.

**Ecosystem-level interoperability** is supported by the open, royalty-free, community-governed nature of the Smart Data Models catalogue. Models are contributed by cities, standards bodies, and industry — meaning the catalogue grows to cover new domains while remaining anchored to a shared governance structure including OASC, FIWARE, TM Forum, and IUDX.

***

#### 4. Requirements Mapping Table

| Req. ID   | Requirement Text                                                                                                                                                       | How This Mechanism Implements It                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **R1.1**  | Data models shall be made explicit, well documented with descriptive metadata, semantically unambiguous, with units and formats explicit. Models should be catalogued. | Every Smart Data Model consists of four mandatory artefacts: JSON Schema (technical structure), JSON-LD `@context` (IRI-level semantic disambiguation), human-readable specification (including attribute descriptions, units as UN/CEFACT codes, datetime formats as ISO 8601), and payload examples. Models are catalogued at smartdatamodels.org and MUST be registered in a DCAT-AP 3 catalogue entry within the deployment. |
| **R1.2a** | Data models shall be based wherever possible on commonly recognised standardised data models.                                                                          | The Mechanism mandates adoption of Smart Data Models from the smartdatamodels.org catalogue as the first choice. The catalogue covers hundreds of entity types across smart city domains. Where Smart Data Models reference upstream standards (SAREF, SOSA/SSN, ISO 5087, DateX II), those alignments are declared in the `@context` via `skos:exactMatch` and `owl:equivalentClass`.                                           |
| **R1.2b** | Where no suitable model exists, extend the closest existing model or define a new one following community best practice.                                               | A JSON Schema `allOf`-based extension pattern is used to add domain-specific properties to the closest existing Smart Data Model. New models follow the Smart Data Models contribution checklist and are submitted for community review. New `@context` entries inherit and extend the parent context, preserving semantic continuity.                                                                                           |
| **R2.1**  | A common data model for each key entity should be developed; different models within the ecosystem should be transformable into it.                                    | The common data model is the applicable Smart Data Model for the entity type. The ontology alignment pipeline (detection → SSSOM representation → RML/SPARQL execution) provides a standardised, reproducible transformation path from any ecosystem-internal model into the common Smart Data Model.                                                                                                                            |
| **R3.1**  | Each data model shall have at least one machine-readable, open, implementation-independent serialisation format.                                                       | JSON (simplified NGSI-LD) and JSON-LD (normalised NGSI-LD) are the mandatory baseline formats. Both are open, implementation-independent W3C and ETSI standards. Additional formats (Turtle, GeoJSON, CSV) are supported via HTTP content negotiation.                                                                                                                                                                           |
| **R3.2**  | Documentation of the data transport format must be sufficient to allow creation of a non-proprietary interpreter.                                                      | The JSON Schema `schema.json` is fully self-describing: any JSON Schema 2020-12 compliant validator can reconstruct and validate payloads without proprietary tooling. The normalised NGSI-LD format is fully specified in ETSI GS CIM 009, a publicly available standard.                                                                                                                                                       |
| **R3.3**  | Multiple transport formats for the same model shall represent the same information content consistently.                                                               | The JSON-LD `@context` file is the single source of truth for property semantics. All serialisations (normalised, simplified, Turtle, GeoJSON) are derived from or mappable to the same `@context`-grounded graph model, ensuring semantic equivalence across formats.                                                                                                                                                           |
| **R3.4**  | The representation should support validation using openly published schemas or machine-readable constraints.                                                           | Validation is performed against the published `schema.json` using any JSON Schema 2020-12 validator. The Smart Data Models programme also provides an online validation API and an NGSI-LD payload validator. For stricter constraints, SHACL shapes can be applied as an Application Profile layer.                                                                                                                             |
| **R4.1**  | Application Profiles extending a data model should not impact the existing model or its users.                                                                         | Application Profiles are defined as separate JSON Schema overlays (`if/then` constraints) or SHACL shape graphs that reference the base `schema.json` via `$ref` / `sh:targetClass` without modifying it. The base model remains unchanged and its consumers are unaffected.                                                                                                                                                     |
| **R4.2**  | Specialisations or extensions in an Application Profile shall be well documented and separate from the base model.                                                     | Application Profile artefacts (schema overlay, SHACL shapes, specification document) are maintained in a separate repository or subdirectory from the base Smart Data Model. The profile's specification document explicitly lists all additions and constraints relative to the base model, and references the base model URI for traceability.                                                                                 |
