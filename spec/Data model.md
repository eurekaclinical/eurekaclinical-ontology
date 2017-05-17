# Eureka! Clinical Electronic Health Record Data Model
## Overview
This document describes the electronic health record data model that this project specifies for Eureka! Clinical. The starting point for this document was the data model of a national cohort discovery network called NIH/NCATS Accrual to Clinical Trials (ACT). Emory received a CTSA supplemental award to become a founding member of this network, which initially will include 13 CTSA programs’ affiliated health systems. Using an i2b2 extension called SHRINE (Shared Health Research Information NEtwork), Emory investigators will be able to specify inclusion and exclusion criteria using their web browser, and within minutes get patient counts from each participating health system. In the Atlanta area, Morehouse School of Medicine and Emory are participating.

The data model below describes the main subject areas and what fields are included. While the initial release this model aims to cover a wide variety of potential cohort discovery queries, some of the content, in particular some of the lab tests, are less common but are required for three use cases that are guiding the technical implementation:
* Clinical trial to evaluate safety and efficacy of a novel biologic in early rheumatoid arthritis inadequate responders to methotrexate. 
* Multiple Sclerosis.
* Clinical trial of new anti-fibrosis medication for children with biliary atresia who have undergone hepatic portoenterostomy and have evidence of portal hypertension but have not yet had liver transplant.

## Missing or Unknown data values
The data model uses a single null value, NI=No Information, to represent missing or unknown values. NI means: 
* The data field is not present in the source system, or
* The data field is present in the source system, but the source value is null or blank, or
* The data field is present in the source system, but the source value explicitly denotes an unknown value, or
* The data field is present in the source system, but the source value cannot be mapped to the data model.

## Subject areas
### Demographics
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|
| BIRTH_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Date and time of birth. Current age (at time of query) is calculated from this. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |
| SEX | TEXT(2) | A=Ambiguous<br/>F=Female<br/>M=Male<br/>O=Other<br/>NI=No information | Administrative sex. Assign ambiguous for transgender/hermaphrodite. For individuals undergoing gender re-assignment, use the Other category. |
| HISPANIC | TEXT(2) | Y=Yes<br/>N=No<br/>NI=No information | A person of Cuban, Mexican, Puerto Rican, South or Central American, or other Spanish culture or origin, regardless of race.<br/><br/>Uses "two question" approach. |
| RACE | TEXT(2) | 1=American Indian or Alaska Native<br/>2=Asian<br/>3=Black or African American<br/>4=Native Hawaiian or Other Pacific Islander<br/>5=White<br/>6=Multiple race<br/>NI=No information | Uses one or more race values per patient.<br/><br/>American Indian or Alaska Native – A person having origins in any of the original peoples of North and South America (including Central America), and who maintains tribal affiliation or community attachment.<br/>Asian – A person having origins in any of the original peoples of the Far East, Southeast Asia, or the Indian subcontinent including, for example, Cambodia, China, India, Japan, Korea, Malaysia, Pakistan, the Philippine Islands, Thailand, and Vietnam.<br/>Black or African American – A person having origins in any of the black racial groups of Africa.<br/>Native Hawaiian or Other Pacific Islander – A person having origins in any of the original peoples of Hawaii, Guam, Samoa, or other Pacific Islands.<br/>White – A person having origins in any of the original peoples of Europe, the Middle East, or North Africa.<br/>Multiple - A person identifying themselves as more than one race.<br/><br/>Uses the "two question" approach.
| VITAL_STATUS | TEXT(1) | 1=Known deceased | Note that NI is not allowed. |
| DEATH_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Date and time of death. Death date is not PHI. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |

### Diagnoses
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|
| DIAGNOSIS_CODE | | Diagnosis code. See below for content. |
| DIAGNOSIS_CODING_SYSTEM | ICD-9-CM<br/>ICD-10-CM | Diagnosis coding system. |
| DIAGNOSIS_CODING_SYSTEM_VERSION | Example:<br/><br/>ICD-9-CM Version 32 | Diagnosis coding system version. |
| DIAGNOSIS_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Diagnosis date and time. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |
| DIAGNOSIS_SOURCE | TEXT(2) | AD=Admitting<br/>DI=Discharge<br/>FI=Final<br/>IN=Interim<br/>NI=No information | Classification of diagnosis source. We include these categories to allow some flexibility in implementation. The context is to capture available diagnoses recorded during a specific encounter. It is not necessary to populate interim diagnoses unless readily available.<br/><br/>Ambulatory encounters would generally be expected to have a source of “Final.” |
| DIAGNOSIS_PRIORITY | TEXT(2) | P=Primary<br/>S=Secondary<br/>NI=No information | Principal discharge diagnosis flag |

#### ICD-9-CM diagnosis code hierarchy (we will use the standard ICD-9 hierarchy as shown in part below; all ICD-9 codes will be available for query)
* Circulatory system …
* Conditions in the perinatal period …
* Congenital anomalies …
* Digestive system …
* Endocrine disorders …
* Events of pregnancy …
* Genitourinary system …
* Hematologic diseases …
* Infectious and parasitic diseases …
* Injury and poisoning …
* Mental disorders …
* Metabolic and immune diseases …
* Musculoskeletal and connective tissue diseases …
* Neoplasms …
* Neurologic disorders …
* Nutritional deficiencies …
* Respiratory system diseases …
* Skin diseases …
* Symptoms, signs, and ill-defined conditions …
* E-codes …
* V-codes …

### Procedures
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|

### Visits
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|

### Medication orders
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|

### Laboratory tests
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|
