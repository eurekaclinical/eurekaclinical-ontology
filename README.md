# Eureka! Clinical Ontology Installation Files
[Atlanta Clinical and Translational Science Institute (ACTSI)](http://www.actsi.org), [Emory University](http://www.emory.edu), Atlanta, GA

## What does it do?
It specifies Eureka! Clinical's extensions to the i2b2 metadata schema. It also contains [liquibase](http://liquibase.org) XML changelog files for creating i2b2 metadata schema tables with those extensions (in `src/main/resources/dbmigration`).

## Version 2 development series
Includes changes to the metadata schema to support improved performance of SQL statements to retrieve concepts.

## Version 1.2
Initial version, with various bug fixes.

## Build requirements
* [Oracle Java JDK 8](http://www.oracle.com/technetwork/java/javase/overview/index.html)
* [Maven 3.2.5 or greater](https://maven.apache.org)

## Runtime requirements
* [Oracle Java JRE 8](http://www.oracle.com/technetwork/java/javase/overview/index.html)
* [Liquibase 3.3 or greater](http://www.liquibase.org/download/index.html)

## Building it
The project uses the maven build tool. Typically, you build it by invoking `mvn clean install` at the command line. For simple file changes, not additions or deletions, you can usually use `mvn install`. See https://github.com/eurekaclinical/dev-wiki/wiki/Building-Eureka!-Clinical-projects for more details.

## Maven dependency
```
<dependency>
    <groupId>org.eurekaclinical</groupId>
    <artifactId>eurekaclinical-ontology</artifactId>
    <version>version</version>
</dependency>
```

## Terminologies provided
* ICD9-CM diagnosis codes 
* ICD9 procedure codes
* ICD10-CM diagnosis codes from the UMLS 2015AA release, obtained from the [NCBO BioPortal Ontology to i2b2 File Mappings page](http://i2b2.bioontology.org)
* ICD10-PCS procedure codes from the UMLS 2015AA release, obtained from the [NCBO BioPortal Ontology to i2b2 File Mappings page](http://i2b2.bioontology.org)
* The Lab test hierarchy (LOINC codes) in the ACT ontology version 1.3 from https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization
* The NDF-RT/RxNorm hierarchy in the ACT ontology version version 1.3 from https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization

The project also provides demographics and vital signs concept hierarchies that were created by the Eureka! Clinical team, borrowing heavily from the demo data ontology from the i2b2 distribution.

## Extensions to the i2b2 metadata schema
Eureka! Clinical's extensions to the i2b2 metadata schema start from the i2b2 version 1.7 metadata schema. See `src/main/resources/dbmigration/i2b2-meta-schema-changelog.xml` for database-agnostic DDL for these extensions.

### Ontology tables
Eureka! Clinical ontology tables contain one additional column over stock i2b2, EK_UNIQUE_ID, which is a VARCHAR with length 700. It is expected to be globally unique. We also index the column. 

### Additional tables
The additional tables are represented in the following model:

![Metadata extensions model](https://github.com/eurekaclinical/eurekaclinical-ontology/blob/master/spec/Eureka%20Clinical%20metadata%20extensions.png)

#### EK_MODIFIER_INTERP
When i2b2 modifiers are specified as records in an i2b2 metadata table, there is insufficient metadata for Eureka! Clinical to map a modifier to a Eureka! Clinical property. The EK_MODIFIER_INTERP table annotates such modifier records to indicate the modifier to which they belong.
#### EK_TEMP_UNIQUE_IDS
A transaction-scoped temporary table for caching EK_UNIQUE_ID values during retrieval of metadata.

#### EK_TEMP_PROPERTIES
A session-scoped temporary table to caching Eureka! Clinical property information during retrieval of metadata.

## Running liquibase with the changelog files
There are two ways to run liquibase on Eureka! Clinical project, both described in the [liquibase documentation](http://www.liquibase.org/documentation/index.html):
* [from the command line](http://www.liquibase.org/documentation/command_line.html)
* [using maven](http://www.liquibase.org/documentation/maven/index.html).

## Getting help
Feel free to contact us at help@eurekaclinical.org.
