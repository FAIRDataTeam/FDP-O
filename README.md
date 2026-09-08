# FDP-O

The FAIR Data Point Ontology (FDP-O) defines the classes and properties that are specific to the FAIR Data Point (FDP) and their relations to the Data Catalog Vocabulary (DCAT) version 3. It is the vocabulary used by the [FAIR Data Point specification](https://specs.fairdatapoint.org/).

Namespace: `https://w3id.org/fdp/fdp-o#` (prefix `fdp-o`). The namespace `http://purl.org/fdp/fdp-o#` used by earlier releases is deprecated.

## Files

| File | Role |
| --- | --- |
| `fdp-ontology.ttl` | Source of the ontology, in RDF Turtle. Edit this file. |
| `fdp-ontology.owl` | RDF/XML serialisation generated from the Turtle source. Do not edit by hand. |
| `fdp-api.owl` | Legacy description of the FDP API, unchanged. |

To regenerate the RDF/XML after editing the Turtle:

```sh
uv run --with rdflib python -c "from rdflib import Graph; g=Graph().parse('fdp-ontology.ttl'); open('fdp-ontology.owl','w').write(g.serialize(format='pretty-xml'))"
```

## Version 2.0

Version 2.0 aligns the ontology with version 2.0 of the FAIR Data Point specification.

- `fdp-o:MetadataRecord` is the class of the record that describes the registration of an entity in an FDP. It is linked to the entity with `fdp-o:isMetadataOf` and `fdp-o:hasMetadata`, which are sub-properties of `foaf:primaryTopic` and `foaf:isPrimaryTopicOf`. The domain and range of these properties are no longer restricted to `dcat:Resource`. `fdp-o:Metadata` is deprecated in its favour.
- `fdp-o:servesMetadata` relates a `fdp-o:MetadataService` to the metadata records it serves, and is what distinguishes a metadata service from other `dcat:DataService`s.
- `fdp-o:metadataCatalog` has domain `fdp-o:MetadataService`, range `dcat:Catalog`, and specialises `dcterms:relation`.
- The properties of a FAIR Data Point follow the names used by the specification: `fdp-o:startDate`, `fdp-o:endDate`, `fdp-o:hasSoftwareVersion`, `fdp-o:uiLanguage` (an object property with an IRI value) and `fdp-o:conformsToFdpSpec`. The former `fdpStartDate`, `fdpEndDate`, `fdpSoftwareVersion` and `fdpUILanguage` are deprecated and point to their replacements.
- `fdp-o:metadataIssued`, `fdp-o:metadataModified` and `fdp-o:metadataIdentifier` are deprecated. The creation and modification dates of a metadata record are stated with `dcterms:issued` and `dcterms:modified` on the `fdp-o:MetadataRecord`, which is identified by its own IRI.
- Every term has an `rdfs:label`; every non-deprecated term has a `skos:definition`.
- The ontology has a version IRI, `https://w3id.org/fdp/fdp-o/2.0`.

Deprecated terms carry `owl:deprecated true` and, where a replacement exists, `dcterms:isReplacedBy`. Terms of the pre-1.0 namespace `http://rdf.biosemantics.org/ontologies/fdp-o#` are kept as deprecated equivalents.

## Licence

[Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/legalcode).
