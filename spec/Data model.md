# Overview
This document describes the electronic health record data model that is used by Eureka! Clinical. The starting point for this document was the data model of a national cohort discovery network called NIH/NCATS Accrual to Clinical Trials (ACT). Emory received a CTSA supplemental award to become a founding member of this network, which initially will include 13 CTSA programs’ affiliated health systems. Using an i2b2 extension called SHRINE (Shared Health Research Information NEtwork), Emory investigators will be able to specify inclusion and exclusion criteria using their web browser, and within minutes get patient counts from each participating health system. In the Atlanta area, Morehouse School of Medicine and Emory are participating.

The data model below describes the main subject areas and what fields are included. While the initial release this model aims to cover a wide variety of potential cohort discovery queries, some of the content, in particular some of the lab tests, are less common but are required for three use cases that are guiding the technical implementation:
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

