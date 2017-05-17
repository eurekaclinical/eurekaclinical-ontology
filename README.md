# Eureka! Clinical Ontology Installation Files
[Atlanta Clinical and Translational Science Institute (ACTSI)](http://www.actsi.org), [Emory University](http://www.emory.edu), Atlanta, GA

## What does it do?
It specifies Eureka! Clinical's extensions to the i2b2 metadata schema. It specifies an electronic health record data model and set of terminologies. It also contains [liquibase](http://liquibase.org) XML changelog files for creating i2b2 metadata schema tables with those extensions (in `src/main/resources/dbmigration`).

## Version 2 development series
Includes changes to the metadata schema to support improved performance of SQL statements to retrieve concepts. We also plan to update all of our terminologies to the latest versions.

## Version 1.2
Initial version, with various bug fixes.

## Build requirements
* [Oracle Java JDK 8](http://www.oracle.com/technetwork/java/javase/overview/index.html)
* [Maven 3.2.5 or greater](https://maven.apache.org)

## Runtime requirements
* [Oracle Java JRE 8](http://www.oracle.com/technetwork/java/javase/overview/index.html)
* [Liquibase 3.3 or greater](http://www.liquibase.org/download/index.html)
* One of the following relational databases:
  * [Oracle](https://www.oracle.com/database/index.html) 11g or greater
  * [PostgreSQL](https://www.postgresql.org) 9.1 or greater
  * [H2](http://h2database.com) 1.4.193 or greater (for testing)

## Building it
The project uses the maven build tool. Typically, you build it by invoking `mvn clean install` at the command line. For simple file changes, not additions or deletions, you can usually use `mvn install`. See https://github.com/eurekaclinical/dev-wiki/wiki/Building-Eureka!-Clinical-projects for more details.

## Creating an i2b2 metadata schema with Eureka! Clinical extensions
1) Create a schema and a user account for accessing that schema. 
2) Get a JDBC driver for your database and put it the liquibase lib directory. 
3) Create the TABLE_ACCESS table by execute the following from the liquibase installation:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/create-table-access-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
4) Next, add the Eureka! Clinical extra tables to the schema:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/i2b2-meta-schema-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
5) Install the demographics concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_DEMOG-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
6) Install the ICD-10-CM concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_ICD10CM-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
7) Install the ICD-10-PCS concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_ICD10PCS-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
8) Install the ICD-9-CM concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_ICD9D-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
9) Install the ICD-9 procedure concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_ICD9P-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
10) Install the medication order concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_MED_ORDERS-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
11) Install the lab test concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_LABS-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```
12) Install the vital signs concepts:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-EK_VITALS-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```

## Adding breakdown paths to the data schema
Assuming you already have an i2b2 data schema, run the following:
```
./liquibase \
      --driver=JDBC_DRIVER_CLASS_NAME \
      --classpath=/path/to/jdbcdriver.jar:/path/to/eurekaclinical-ontology-<version>.jar \
      --changeLogFile=dbmigration/eureka-ontology-QT_BREAKDOWN_PATH-changelog.xml \
      --url="JDBC_CONNECTION_URL" \
      --username=DB_USER \
      --password=DB_PASS \
      update
```

## Maven dependency
```
<dependency>
    <groupId>org.eurekaclinical</groupId>
    <artifactId>eurekaclinical-ontology</artifactId>
    <version>version</version>
</dependency>
```

## Data model
The electronic health record data model is described at https://github.com/eurekaclinical/eurekaclinical-ontology/blob/master/spec/Data%20model.md.

## Terminologies provided
| Name | Version | Source |
|------|---------|--------|
| ICD9-CM diagnosis codes | | Analytic Information Warehouse project, circa 2010 |
| ICD9 procedure codes | | Analytic Information Warehouse project, circa 2010 |
| ICD10-CM diagnosis codes | 2015 | UMLS 2015AA release, obtained from the [NCBO BioPortal Ontology to i2b2 File Mappings page](http://i2b2.bioontology.org) |
| ICD10-PCS procedure codes | 2015 | UMLS 2015AA release, obtained from the [NCBO BioPortal Ontology to i2b2 File Mappings page](http://i2b2.bioontology.org) |
| NCATS ACT lab test hierarchy (LOINC codes) | 1.3 | https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization |
| NCATS ACT NDF-RT/RxNorm hierarchy | 1.3 | https://ncatswiki.dbmi.pitt.edu/acts/wiki/DataHarmonization |
| Demographics | 1.0 | Locally developed, based on the i2b2 1.5 demo data ontology |
| Vital signs | | Locally developed |

## Extensions to the i2b2 metadata schema
See [Metadata extensions spec.md](https://github.com/eurekaclinical/eurekaclinical-ontology/blob/master/spec/Metadata%20extensions%20spec.md).

## Running liquibase with the changelog files
There are two ways to run liquibase on Eureka! Clinical project, both described in the [liquibase documentation](http://www.liquibase.org/documentation/index.html):
* [from the command line](http://www.liquibase.org/documentation/command_line.html)
* [using maven](http://www.liquibase.org/documentation/maven/index.html).

## Getting help
Feel free to contact us at help@eurekaclinical.org.
