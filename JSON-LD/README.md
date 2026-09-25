Schema.org JSON-LD as a metadata format provides not only a rich interoperable structure for describing a myriad of objects, it enables machine discoverability through infrastructure already implemented on the internet. This metadata is to be presented in a user-friendly format on all RCO landing pages for human use and embedded directly into each RCO landing page for machine-actionability.

This folder contains the minimum requirements and several more examples of the Schema.org JSON-LD metadata for RCOs. The choice of field names in schema.org and the supplementary vocabularies used are based on the current guidelines for expressing datasets on schema.org, where relevant, which is maintained by the ESIP Schema-Dot-Org Cluster (https://www.esipfed.org/collaboration-areas/schema-org/).

# Required Fields  
The minimum metadata fields required for RCOs are primarily based on the metadata fields required by DataCite (https://datacite-metadata-schema.readthedocs.io/en/latest/, currently v4.7) and their mapping into Schema.org. We add the description and license fields based on the strong recommendation to do so in DataCite's documentation and elsewhere and the substantial benefit the fields lend to discoverability and reusability. These fields include:
- name
- creator/name
- datePublished
- publisher/name
- description
- license

Best Practices:
- The creator/name should be written in family_name, given_name format, e.g., "Charpy, Antoine;". See DataCite's documentation for more details.
- The publisher name should be identical to the name included in the ROR.org or similar directory for organizations, if a corresponding entry exists.
- The description should be between 50 and 2000 characters.
- The license should be the URL to the SPDX entry for the desired license, e.g., https://spdx.org/licenses/CC-BY-4.0.html.

The primary purpose of an RCO is to redirect a citation to the RCO to be attributed to the artifacts the RCO cites. Therefore, the "**citation**" field is also required with at minimum the URLs to the cited items. Ideally, these will be DOIs or other globally unique persistent identifiers for the artifacts.

To enable machine actionability, a few additional metadata fields are required with standard values. See the examples for details.

# Recommended fields
A few additional fields are expected to provide additional benefit for many use cases and are recommended.

## **citation/@type** 
Indicating the type of the artifact for each one provides the human and machine information to aid in matching the artifact in the RCO to those mentioned in the associated publication. However, this is not always allowed by indexers for all types (e.g., "ResearchProject" throws errors). For some resource types, including "Dataset" and "SoftwareApplication", including the resource type results in an additional requirement by Google. 

Dataset
- description
- name

SoftwareApplication 
- name, and two of the following:
- offers
- aggregateRating
- applicationCategory
- operatingSystem

The "Google" JSON file gives an example of the required structure for these two resource types when the type is included.

## **hasPart** 
This metadata field is recommended to include when some artifacts are useful to include, but should not be cited. If another metadata field more accurately indicates the relationship between this artifact and another, then that more specific metadata field should be used (see below). This and similar containers should be constructed similarly to the "citation" container. 

## **@reverse/citation** 
This metadata field is recommended to add _after publication_ of the associated paper to connect the RCO to that paper. The full DOI link for the paper should be included, e.g., 
```
  "@reverse": {
  	"citation": {
    	"@id": "https://doi.org/10.1038/s41586-024-08495-6",
      "@type": "ScholarlyArticle"
    }
  },
```
Note the "@type" field is included here as it is required by the schema.org validator tool for this structure.

## **prov:wasDerivedFrom** and **isBasedOn** 
These two fields are also important to many use cases. Use _both_ of these fields to indicate when one resource was used to create another (e.g., a software created a dataset or figure). See examples for details.

# Validation Resources
All files have been tested using Schema.org's validator (https://validator.schema.org/) for correct JSON-LD and schema.org alignment. The minimum and "Google" examples also pass validation with Google's Rich Results tool (https://search.google.com/test/rich-results). This means that Google will not exclude the RCO landing page from indexing. Including landing pages into Google's index requires additional steps which are beyond the scope of this work. The current choice of "Collection" for the schema.org type may change to "Dataset" based on conversations with publishers, but the "Collection" type is agreed as the more correct choice.
