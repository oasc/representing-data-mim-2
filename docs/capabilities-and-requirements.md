# Capabilities and Requirements

## Capabilities and Requirements

**C1: All entities included in data sources are described using consistent data models**\
**to enable interoperability for applications and systems.**

| C1 Requirements:                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>R1. Data models used for all entities in any data source shall be made explicit. They<br>shall be well documented and have descriptive metadata, where the terms used<br>shall be semantically unambiguous. For attributes related to units of measurement,<br>time formats etc, the units, formats etc, used shall be made explicit. The data models<br>should be catalogued* so that they can be easily findable.</p> |
| <p>R2a. Data models used shall be based (wherever possible) on commonly recognised<br>standardised data models as listed below</p>                                                                                                                                                                                                                                                                                         |
| <p>R2b. Where it is not possible to use existing standardised data models, efforts shall<br>be made to extend existing standardised data models that are most closely aligned<br>or to define new ones, following best practice and conventions of the community or<br>organisation defining the data models.</p>                                                                                                          |
| <p>R3. Data models used shall support the exchange of data by using the relevant<br>requirements of the MIMs on Accessing data and Interlinking data</p>                                                                                                                                                                                                                                                                   |

\*Note: Should the cataloguing be done in a human readable way, the data models\
themselves would not necessarily need to be made explicit in a human readable\
way.

**C2: Different data models for the same entity that are used within a common data**\
**sharing ecosystem should be easily transformable into a common data model**

| C2 Requirements                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>R1. Data models used for all entities in any data source shall be made explicit. They<br>shall be well documented and have descriptive metadata, where the terms used<br>shall be semantically unambiguous. For attributes related to units of measurement,<br>time formats etc, the units, formats etc, used shall be made explicit. The data models<br>should be catalogued* so that they can be easily findable.</p> |

\*Note: As far as possible this common data model should be a standard data model\
for that entity and one that would also enable additional new fields to be included in\
the future

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

