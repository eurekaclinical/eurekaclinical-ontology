# Eureka! Clinical Ontology Installation Files
[Atlanta Clinical and Translational Science Institute (ACTSI)](http://www.actsi.org), [Emory University](http://www.emory.edu), Atlanta, GA

## What does it do?
It specifies Eureka! Clinical's extensions to the i2b2 metadata schema. It also contains [liquibase](http://liquibase.org) XML changelog files for creating i2b2 metadata schema tables with those extensions.

## Version 2 development series
Includes changes to the metadata schema to support improved performance of SQL statements to retrieve concepts.

## Version 1.2
Initial version, with various bug fixes.

## Requirements
* [Oracle Java JRE 8](http://www.oracle.com/technetwork/java/javase/overview/index.html)
* [Liquibase 3.3 or greater](http://www.liquibase.org/download/index.html)

## Terminologies provided
* ICD9-CM diagnosis codes 
* ICD9 procedure codes
* ICD10-CM diagnosis codes from the UMLS 2015AA release, obtained from the [NCBO BioPortal Ontology to i2b2 File Mappings page](http://i2b2.bioontology.org)
* ICD10-PCS procedure codes from the UMLS 2015AA release, obtained from the [NCBO BioPortal Ontology to i2b2 File Mappings page](http://i2b2.bioontology.org)
* The Lab test hierarchy (LOINC codes) in the ACT ontology version 1.3 from https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization
* The NDF-RT/RxNorm hierarchy in the ACT ontology version version 1.3 from https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization

The project also provides demographics and vital signs concept hierarchies that were created by the Eureka! Clinical team, borrowing heavily from the demo data ontology from the i2b2 distribution.

## Extensions to the i2b2 metadata schema
Eureka! Clinical's extensions to the i2b2 metadata schema start from the i2b2 version 1.7 metadata schema.

### Ontology tables
Eureka! Clinical ontology tables contain one additional column over stock i2b2, EK_UNIQUE_ID, which is a VARCHAR with the same length as C_FULLNAME. We also index the column. Here is the Oracle DDL for creating a new ontology table that will work with both i2b2 and Eureka. Replace TABLE_NAME with a descriptive name for your table. For the indexes, also replace ABBREV_TABLE_NAME with a descriptive name.
```
CREATE TABLE "TABLE_NAME" 
   (	"C_HLEVEL" NUMBER(22,0), 
	"C_FULLNAME" VARCHAR2(700), 
	"C_NAME" VARCHAR2(2000), 
	"C_SYNONYM_CD" CHAR(1), 
	"C_VISUALATTRIBUTES" CHAR(3), 
	"C_TOTALNUM" NUMBER(22,0), 
	"C_BASECODE" VARCHAR2(50), 
	"C_METADATAXML" CLOB, 
	"C_FACTTABLECOLUMN" VARCHAR2(50), 
	"C_TABLENAME" VARCHAR2(50), 
	"C_COLUMNNAME" VARCHAR2(50), 
	"C_COLUMNDATATYPE" VARCHAR2(50), 
	"C_OPERATOR" VARCHAR2(10), 
	"C_DIMCODE" VARCHAR2(700), 
	"C_COMMENT" CLOB, 
	"C_TOOLTIP" VARCHAR2(900), 
	"M_APPLIED_PATH" VARCHAR2(700), 
	"UPDATE_DATE" DATE, 
	"DOWNLOAD_DATE" DATE, 
	"IMPORT_DATE" DATE, 
	"SOURCESYSTEM_CD" VARCHAR2(50), 
	"VALUETYPE_CD" VARCHAR2(50), 
	"M_EXCLUSION_CD" VARCHAR2(25), 
	"C_PATH" VARCHAR2(700), 
	"C_SYMBOL" VARCHAR2(50), 
	"EK_UNIQUE_ID" VARCHAR2(700)
   ) ;
 
CREATE INDEX "META_PATH_ABBREV_TABLE_NAME_IDX" ON "TABLE_NAME" ("C_PATH");
CREATE INDEX "META_EKUID_ABBREV_TABLE_NAME_IDX" ON "TABLE_NAME" ("EK_UNIQUE_ID");
CREATE INDEX "META_FULLNAME_ABBREV_TABLE_NAME_IDX" ON "TABLE_NAME" ("C_FULLNAME");
CREATE INDEX "META_APP_PATH_ABBREV_TABLE_NAME_IDX" ON "TABLE_NAME" ("M_APPLIED_PATH");

ALTER TABLE "TABLE_NAME" MODIFY ("EK_UNIQUE_ID" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("UPDATE_DATE" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("M_APPLIED_PATH" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_DIMCODE" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_OPERATOR" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_COLUMNDATATYPE" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_COLUMNNAME" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_TABLENAME" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_FACTTABLECOLUMN" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_VISUALATTRIBUTES" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_SYNONYM_CD" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_NAME" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_FULLNAME" NOT NULL ENABLE);
ALTER TABLE "TABLE_NAME" MODIFY ("C_HLEVEL" NOT NULL ENABLE);
```
### Additional tables


## Running liquibase with the changelog files
There are two ways to run liquibase on Eureka! Clinical project, both described in the [liquibase documentation](http://www.liquibase.org/documentation/index.html):
* [from the command line](http://www.liquibase.org/documentation/command_line.html)
* [using maven](http://www.liquibase.org/documentation/maven/index.html).
