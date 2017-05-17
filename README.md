# Eureka! Clinical Ontology Installation Files
Atlanta Clinical and Translational Science Institute (ACTSI), Emory University, Atlanta, GA

## What does it do?
It specifies Eureka! Clinical's extensions to the i2b2 metadata schema. It also contains [liquibase](http://liquibase.org) XML changelog files for creating i2b2 metadata schema tables with those extensions.

## Version 2 development series
Includes changes to the metadata schema to support improved performance of SQL statements to retrieve concepts.

## Version 1.2
Initial version, with various bug fixes.

## Requirements
* Java 8
* Liquibase 3.3 or greater

## Terminologies provided
* ICD9-CM diagnosis codes
* ICD9 procedure codes
* ICD10-CM diagnosis codes
* ICD10-PCS procedure codes
* The Lab test hierarchy (LOINC codes) in the ACT ontology version 1.3 from https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization
* The NDF-RT/RxNorm hierarchy in the ACT ontology version version 1.3 from https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization

The project also provides customized demographics and vital signs concepts.

## Extensions to the i2b2 metadata schema

## Running liquibase with the changelog files
There are two ways to run liquibase on Eureka! Clinical project, both described in the [liquibase documentation](http://www.liquibase.org/documentation/index.html):
* [from the command line](http://www.liquibase.org/documentation/command_line.html)
* [using maven](http://www.liquibase.org/documentation/maven/index.html).
