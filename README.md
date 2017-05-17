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
See [Metadata extensions spec.md](https://github.com/eurekaclinical/eurekaclinical-ontology/blob/master/spec/Metadata%20extensions%20spec.md).

## Running liquibase with the changelog files
There are two ways to run liquibase on Eureka! Clinical project, both described in the [liquibase documentation](http://www.liquibase.org/documentation/index.html):
* [from the command line](http://www.liquibase.org/documentation/command_line.html)
* [using maven](http://www.liquibase.org/documentation/maven/index.html).

## Getting help
Feel free to contact us at help@eurekaclinical.org.
