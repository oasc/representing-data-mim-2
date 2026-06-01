# Capabilities and Requirements

## Capabilities and Requirements

### **C1: All entities included in data sources are described using consistent data models to enable interoperability for applications and systems.**

**Requirements:**

**R.1**. Data models used for all entities in any data source shall be made explicit. They\
shall be well documented and have descriptive metadata, where the terms used\
shall be semantically unambiguous. For attributes related to units of measurement,\
time formats etc, the units, formats etc, used shall be made explicit. The data models\
should be catalogued\* so that they can be easily findable.

**R1.2a**. Data models used shall be based (wherever possible) on commonly recognised\
standardised data models as listed below

**R1.2b**. Where it is not possible to use existing standardised data models, efforts shall\
be made to extend existing standardised data models that are most closely aligned\
or to define new ones, following best practice and conventions of the community or\
organisation defining the data models.

**R3**. Data models used shall support the exchange of data by using the relevant\
requirements of the MIMs on Accessing data and Interlinking data\*

\*Note: Should the cataloguing be done in a human readable way, the data models\
themselves would not necessarily need to be made explicit in a human readable\
way.

### **C2: Different data models for the same entity that are used within a common data sharing ecosystem should be easily transformable into a common data model**

**Requirements:**

**R2.1** A common data model for each key entity should be developed for any data ecosystem. That common data model should contain all the fields included within the different data models for that entity that are used within that data ecosystem. Each different data model used within that data ecosystem could then be transformed into the common data model.

\*Note: As far as possible this common data model should be a standard data model\
for that entity and one that would also enable additional new fields to be included in\
the future



### **C3: Any data and its associated metadata can be shared in open, standardised, data transport formats so that data can be exchanged and interpreted consistently by different tools and implementations.**

**Requirements:**

**R3.1** Each data model used shall have at least one defined machine-readable data transport format ("serialisation") that is open, publicly available and implementation-independent.&#x20;

**R3.2** The documentation of the data transport format should be sufficient to allow the creation of non-proprietary application or interpretor that is able to reconstruct all the data stored in such a data format.

**R3.3** Where multiple data transport formats are supported for the same data model, they shall represent the same information content consistently and without loss of meaning.

**R3.4** The representation should support validation using openly published schemas, grammars, or equivalent machine-readable constraints, where such validation mechanisms exist for the chosen format.

### **C4: When useful, it should be possible to create "Application Profiles" for a data model, so that use case specific attributes can be added or specified without changing the underlying data model\***

**Requirements:**

**R4.1** Application Profiles that extend a data model should not impact the already existing model and its users

**R4.2** The specialisations or extensions introduced in the Application Profile of the model should be well documented, separate from the base data model



## Specifications

The following list provides the recommended standardised sets of data models for\
MIM2. This will continue to be added to, as new and suitable sets are identified.

* ISO/IEC JTC1 is developing the ISO/IEC 5087 series of standards on City\
  Data Model, of which Part 1: Foundation level concepts (ISO/IEC 5087-\
  1:2023) has already been published and Part 2: City level concepts (ISO/IEC\
  DIS 5087-2) is at the final draft stage.
* SAREF: Smart Appliances REFerence (SAREF) ontology specified by ETSI\
  OneM2M committee with the extension of SAREF4Cities provides an ontology\
  focused on smart cities.
* oneM2M base ontology (that is compatible with SAREF). Additionally,\
  oneM2M provides the means to instantiate ontologies as a means to provide\
  semantic descriptions of the data exchanged (through the use of metadata).
* Core vocabularies of former ISA2 (now Interoperable Europe) like Core Public\
  Service Vocabulary Application Profile used as the basis for the Single Digital\
  Gateway Regulation that touches local governments, Core Person, Core\
  Organization etc.
* DTDL is the Digital twin Definition Language developed by Microsoft. This\
  language is based on top of json-ld and the existing Fiware data models are\
  converted in this format.
* For spatial (and spatio-temporal) observation data, the provisions of MIM-7\
  (Places) about data encoding have to be taken into consideration.
* For the mobility domain it is recommended to use DateX II.
* For general use cases, where a more flexible, data model is needed, NGSI-\
  LD compliant data models have been defined by organisations and projects,\
  including OASC, FIWARE, GSMA and the SynchroniCity project and there is\
  an ongoing joint activity of TM Forum and FIWARE to specify more under the\
  Smart Data Models initiative, see [https://smartdatamodels.org/](https://smartdatamodels.org/)

