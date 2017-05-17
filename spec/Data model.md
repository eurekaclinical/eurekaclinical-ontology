# Eureka! Clinical Electronic Health Record Data Model
## Overview
This document describes the electronic health record data model that is used by Eureka! Clinical. The starting point for this document was the data model of a national cohort discovery network called NIH/NCATS Accrual to Clinical Trials (ACT). Emory received a CTSA supplemental award to become a founding member of this network, which initially will include 13 CTSA programs’ affiliated health systems. Using an i2b2 extension called SHRINE (Shared Health Research Information NEtwork), Emory investigators will be able to specify inclusion and exclusion criteria using their web browser, and within minutes get patient counts from each participating health system. In the Atlanta area, Morehouse School of Medicine and Emory are participating.

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
| SEX | TEXT(2) | A=Ambiguous, F=Female, M=Male, O=Other, NI=No information | Administrative sex. Assign ambiguous for transgender/hermaphrodite. For individuals undergoing gender re-assignment, use the Other category. |
| HISPANIC | TEXT(2) | Y=Yes, N=No, NI=No information | A person of Cuban, Mexican, Puerto Rican, South or Central American, or other Spanish culture or origin, regardless of race. Uses "two question" approach. |
| RACE | TEXT(2) | 1=American Indian or Alaska Native, 2=Asian, 3=Black or African American, 4=Native Hawaiian or Other Pacific Islander, 5=White, 6=Multiple race, NI=No information | Uses one or more race values per patient. American Indian or Alaska Native – A person having origins in any of the original peoples of North and South America (including Central America), and who maintains tribal affiliation or community attachment. Asian – A person having origins in any of the original peoples of the Far East, Southeast Asia, or the Indian subcontinent including, for example, Cambodia, China, India, Japan, Korea, Malaysia, Pakistan, the Philippine Islands, Thailand, and Vietnam. Black or African American – A person having origins in any of the black racial groups of Africa. Native Hawaiian or Other Pacific Islander – A person having origins in any of the original peoples of Hawaii, Guam, Samoa, or other Pacific Islands. White – A person having origins in any of the original peoples of Europe, the Middle East, or North Africa. Multiple - A person identifying themselves as more than one race. Uses the "two question" approach.

### Diagnoses

### Procedures

### Visits

### Medication orders

### Laboratory tests

