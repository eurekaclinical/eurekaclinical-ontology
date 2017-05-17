
# Extensions to the i2b2 metadata schema
Eureka! Clinical's extensions to the i2b2 metadata schema start from the i2b2 version 1.7 metadata schema. See the [i2b2 metaschema changelog](https://github.com/eurekaclinical/eurekaclinical-ontology/blob/master/src/main/resources/dbmigration/i2b2-meta-schema-changelog.xml) for database-agnostic DDL for these extensions.

## Ontology tables
Eureka! Clinical ontology tables contain one additional column over stock i2b2, EK_UNIQUE_ID, which is a VARCHAR with length 700. It is expected to be globally unique. We also index the column. 

## Additional tables
The additional tables are represented in the following model:

![Metadata extensions model](https://github.com/eurekaclinical/eurekaclinical-ontology/blob/master/spec/Eureka%20Clinical%20metadata%20extensions.png)

### EK_MODIFIER_INTERP
When i2b2 modifiers are specified as records in an i2b2 metadata table, there is insufficient metadata for Eureka! Clinical to map a modifier to a Eureka! Clinical property. The EK_MODIFIER_INTERP table annotates such modifier records to indicate the modifier to which they belong.
### EK_TEMP_UNIQUE_IDS
A transaction-scoped temporary table for caching EK_UNIQUE_ID values during retrieval of metadata.

### EK_TEMP_PROPERTIES
A session-scoped temporary table for caching Eureka! Clinical property information during retrieval of metadata.
