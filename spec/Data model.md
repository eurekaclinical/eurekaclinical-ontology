# Overview
This document describes the content currently planned for inclusion in Emory’s i2b2 deployment. I2b2 supports rapid cohort discovery using electronic health record data. From a web browser, investigators will be able to specify inclusion and exclusion criteria, and within minutes get a count of how many patients meet those criteria. I2b2 will be populated with data from the Emory Clinical Data Warehouse.

The starting point for this document was the data model of a national cohort discovery network called NIH/NCATS Accrual to Clinical Trials (ACT). Emory received a CTSA supplemental award to become a founding member of this network, which initially will include 13 CTSA programs’ affiliated health systems. Using an i2b2 extension called SHRINE (Shared Health Research Information NEtwork), Emory investigators will be able to specify inclusion and exclusion criteria using their web browser, and within minutes get patient counts from each participating health system. In the Atlanta area, Morehouse School of Medicine and Emory are participating.

The data model below describes the main subject areas to be included in the initial release of i2b2 at Emory, including what fields will be included, and for labs, meds, diagnoses and procedures, which labs, meds, etc. are planned for inclusion. While the initial release of i2b2 aims to cover a wide variety of potential cohort discovery queries, some of the content, in particular some of the lab tests, are less common but are required for three use cases the ACT project is using to guide its technical implementation:
* Clinical trial to evaluate safety and efficacy of a novel biologic in early rheumatoid arthritis inadequate responders to methotrexate. 
* Multiple Sclerosis.
* Clinical trial of new anti-fibrosis medication for children with biliary atresia who have undergone hepatic portoenterostomy and have evidence of portal hypertension but have not yet had liver transplant.

# Missing or Unknown data values
The data model uses a single null value, NI=No Information, to represent missing or unknown values. NI means: 
* The data field is not present in the source system, or
* The data field is present in the source system, but the source value is null or blank, or
* The data field is present in the source system, but the source value explicitly denotes an unknown value, or
* The data field is present in the source system, but the source value cannot be mapped to the data model.

# Demographics

# Diagnoses

# Procedures

# Visits

# Medication orders

# Laboratory tests

