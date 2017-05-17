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

#### ICD-10-CM diagnosis code hierarchy (we will use the standard ICD-10 hierarchy as shown in part below; all ICD-10 codes will be available for query)
TODO

### Procedures
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|
| PROCEDURE_CODE | | | Procedure code. See below for content. |
| PROCEDURE_CODING_SYSTEM | | ICD-9-CM<br/>ICD-10-PCS<br/>CPT-4 (i.e., HCPCS Level 1) | Procedure coding system. |
| PROCEDURE_CODING_SYSTEM_VERSION | Example: ICD-9-CM Version 31 | Procedure coding system version. |
| PROCEDURE_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Procedure date and time. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |

#### ICD-9-CM (Inpatient; we will use the standard ICD-9 hierarchy; all ICD-9 codes will be available)
* Diagnostic and nonsurgical procedures …
* Obstetrical procedures …
* Operations on cardiovascular system …
* Operations on digestive system …
* Operations on ear …
* Operations on endocrine system …
* Operations on eye …
* Operations on female genital system …
* Operations on hemic and lymphatic system
* Operations on integument …
* Operations on male genital system …
* Operations on musculoskeletal system …
* Operations on nervous system …
* Operations on nose, mouth and pharynx …
* Operations on respiratory system …
* Operations on urinary system …
* Procedures and interventions, NEC …

#### ICD-10-PCS (Inpatient; we will use the standard ICD-10 hierarchy; all ICD-10 codes will be available)
TODO

#### (Future) CPT-4 (Clinic; only install if your institution has a license)
* Anesthesia Procedures …
* Emerging Technology, Services & Procedure Codes …
* Evaluation and Management Procedures …
* Medicine Services and Procedures …
* Pathology and Laboratory Tests …
* Radiology Procedures …
* Surgical Procedures …
* Tracking Codes for Performance Management …

v  CPT-4 (Clinic; all CPT codes will be available for query internally to Emory for Emory data; CPT codes will not be available from other institutions due to American Medical Association licensing)

Anesthesia Procedures …
Emerging Technology, Services & Procedure Codes …
Evaluation and Management Procedures …
Medicine Services and Procedures …
Pathology and Laboratory Tests …
Radiology Procedures …
Surgical Procedures …
Tracking Codes for Performance Management …

### Visits
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|
| ADMIT_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Date and time of visit or admission. An Age at visit field will be calculated from this. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |
| DISCHARGE_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Date and time of discharge. A Length of stay field will be calculated from this. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |
| VISIT_TYPE | TEXT(2) | IP=Inpatient Hospital Stay<br/>AV=Ambulatory Visit<br/>ED=Emergency Department<br/>OA=Other Ambulatory Visit<br/>NI=No information | Visit type. |

### Medication orders
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|
| MEDICATION_CODE | | RxNorm RxCUI | Map drugs to RxNorm’s Semantic Clinical Drug (SCD), Semantic Branded Drug (SBD), Generic Pack (GPCK), or Branded Pack (BPCK) form. These concepts contain drug name, strength, form, and route of administration. See below for content. |
| MEDICATION_TYPE | | “Products by VA Class” classification from the National Drug File - Reference Terminology (NDF-RT). | Medication classification system is NDF-RT and the medication coding system is RxNORM. The deepest level in the classification is RxNorm’s Semantic Clinical Drug (SCD) form, which contains name, form, and route of administration. |
| MEDICATION_CODING_SYSTEM_VERSION | | Example: RxNorm 01-Dec-2014;17-Dec-2014 | Medication classification system and medication coding system version. |
| ORDER_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Order date and time. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |
| ORDER_TYPE | TEXT(2) | ID=Inpatient Dispensed<br/>AP=Ambulatory Prescribed<br/>NI=No information | Location where medication was ordered. |

#### Medication hierarchy (all medications in all classes below are included)
* Antidotes, deterrents and poison control…
* Antihistamines…
* Antimicrobials…
* Antineoplastics…
* Antiparasitics…
* Antiseptics/disinfectants…
* Autonomic medications…
* Blood products/modifiers/volume expanders…
* Central nervous system medications…
* Cardiovascular medications…
* Dermatological agents…
* Diagnostic agents…
* Gastrointestinal medications…
* Genitourinary medications…
* Herbs/alternative therapies…
* Hormones/synthetics/modifiers…
* Immunological agents…
* Investigational agents…
* Intrapleural medications…
* Irrigation/dialysis solutions…
* Musculoskeletal medications…
* Nasal and throat agents, topical…
* Ophthalmic agents…
* Dental and oral agents, topical…
* Otic agents…
* Pharmaceutical aids/reagents…
* Respiratory tract medications…
* Rectal, local…
* Therapeutic nutrients/minerals/electrolytes…
* Vitamins…
* Miscellaneous agents…

### Laboratory tests
| Field name | Data type | Predefined value sets and descriptive text for categorical fields | Definition/comments |
|------------|-----------|-------------------------------------------------------------------|---------------------|
| LAB_CODE | | LOINC laboratory test code. | Laboratory test code. See below for content. |
| LAB_TYPE | | LOINC multi-axial codes (codes that start with LP). | Laboratory test classification system uses LP codes while the laboratory test coding system is LOINC. See below for content. |
| LAB_CODING_SYSTEM_VERSION | | Example: LOINC 2.48;2014-06-27 | Laboratory test classification system and laboratory test coding system version. |
| RESULT_LOCATION | TEXT(2) | L=Laboratory<br/>P=Point of Care<br/>NI=No information | Location of the test result. Point of Care locations may include anticoagulation clinic, newborn nursery, finger stick in provider office, or home. The default value is ‘L’ unless the result is Point of Care. There should not be any missing values. |
| SPECIMEN_DATE | Date-time field | YYYY-MM-DD HH:MM:SS | Date and time specimen was collected. If times don’t exist in the source data, set HH:MM:SS to 00:00:00. |
| RESULT_QUALITATIVE | TEXT(10) | BORDERLINE<br/>POSITIVE<br/>NEGATIVE<br/>UNDETERMINED<br/>NI=No information | Standardized result for qualitative results. This variable should be NI for quantitative results. |
| RESULT_NUMERICAL | NUMBER(8) | | Standardized/converted result for quantitative results. This variable should be left blank for qualitative results. |
| RESULT_MODIFIER | TEXT | EQ=Equal<br/>GE=Greater than or equal to<br/>GT=Greater than<br/>LE=Less than or equal to<br/>LT=Less than<br/>TX=Text<br/>NI=No information | Modifier for result values. Any symbols in the RAW_RESULT value should be reflected in the RESULT_MODIFIER variable. For example, if the original source data value is "<=200" then RAW_RESULT=200 and RESULT_MODIFIER=LE. If the original source data value is text then RESULT_MODIFIER=TX. If the original source data value is a numeric value then RESULT_MODIFIER=EQ. |
| RESULT_UNIT | TEXT(11) | | Standardized units for the result. |
| ABNORMAL_RESULT_INDICATOR | TEXT(2) | AB=Abnormal<br/>AH=Abnormally high<br/>AL=Abnormally low<br/>CH=Critically high<br/>CL=Critically low<br/>CR=Critical<br/>IN=Inconclusive<br/>NL=Normal<br/>NI=No information | Abnormal result indicator. This value comes from the source data; do not apply logic to create it. |

Laboratory test hierarchy (test name, specimen type, LOINC code, units)
* Chemistry LP40271-6
  * Electrolytes LP19403-2
    * Bicarbonate LP46218-1
      * Bicarbonate in Blood 1959-6 mmol/L
      * Bicarbonate in Plasma 1962-0 mmol/L
      * Bicarbonate in Serum 1963-8 mmol/L
    * Calcium LP42656-6 
      * Calcium in Blood 49765-1 mg/dL
      * Calcium in Serum or Plasma 17861-6 mg/dL
    * Chloride LP46433-6
      * Chloride in Blood 2069-3 mmol/L
      * Chloride in Serum or Plasma 2075-0 mmol/L
    * Creatinine LP41281-4
      * Creatinine in Blood 38483-4 mg/dL
      * Creatinine in Serum or Plasma 2160-0 mg/dL
    * Glucose LP42107-0
      * Glucose in Blood 2339-0 mg/dL
      * Glucose in Serum or Plasma 2345-7 mg/dL
    * Phosphate LP43710-0
      * Phosphate in Blood 2774-8 mg/dL
      * Phosphate in Serum or Plasma 2777-1 mg/dL
    * Potassium LP42189-8
      * Potassium in Blood 6298-4 mmol/L
      * Potassium in Serum or Plasma 2823-3 mmol/L
    * Sodium LP48861-6
      * Sodium in Blood 2947-0 mmol/L
      * Sodium in Serum or Plasma 2951-2 mmol/L
    * Urate LP43752-2
      * Urate in Serum or Plasma 3084-1 mg/dL
    * Urea nitrogen LP41307-7
      * Urea nitrogen in Blood 6299-2 mg/dL
      * Urea nitrogen in Serum or Plasma 3094-0 mg/dL
  * Lipids LP15705-4
    * Cholesterol in HDL LP99408-4
      * Cholesterol in HDL in Serum or Plasma 2085-9 mg/dL
      * Cholesterol in HDL in Serum or Plasma ultracentrifugate 18263-4 mg/dL                                                         
      * Cholesterol in HDL in Serum or Plasma by Electrophoresis 49130-8 mg/dL
    * Cholesterol in LDL LP99407-6
      * Cholesterol in LDL in Serum or Plasma 2089-1 mg/dL
      * Cholesterol in LDL in Serum or Plasma ultracentrifugate 18261-8 mg/dL
      * Cholesterol in LDL in Serum or Plasma by Electrophoresis 49132-4 mg/dL
      * Cholesterol in LDL in Serum or Plasma by calculation 13457-7 mg/dL
    * Cholesterol non HDL LP52754-6
      * Cholesterol non HDL in Serum or Plasma 43396-1 mg/dL
    * Cholesterol Total LP43571-6
      * Cholesterol total in Serum or Plasma 2093-3 mg/dL
      * Cholesterol total in Serum or Plasma ultracentrifugate 48620-9 mg/dL
    * Cholesterol/HDL Ratio LP44836-2
      * Cholesterol/HDL Ratio in Serum or Plasma 9830-1 ratio
    * Triglyceride LP42275-5
      * Triglyceride in Serum or Plasma 2571-8 mg/dL
      * Triglyceride in Serum or Plasma by calculation 12951-0 mg/dL
  * Enzymes LP31392-1
    * ALP LP45609-2
      * ALP in Blood 1783-0 U/L
      * ALP in Serum or Plasma 6768-6 U/L
    * ALT LP44699-4
      * ALT in Serum or Plasma 1742-6 U/L
      * ALT in Serum or Plasma With P-5'-P 1743-4 U/L
      * ALT in Serum or Plasma Without P-5'-P 1744-2 U/L
    * AST LP45656-3
      * AST in Serum or Plasma 1920-8 U/L
      * AST in Serum or Plasma With P-5'-P 30239-8 U/L
    * GGT LP47479-8
      * GGT in Serum or Plasma 2324-2 U/L
    * LDH LP43656-5
      * LDH in Serum or Plasma 2532-0 U/L
      * LDH in Serum or Plasma by Lactate to pyruvate reaction 14804-9 U/L
      * LDH in Serum or Plasma by Pyruvate to lactate reaction 14805-6 U/L
  * Liver function LP31397-0
    * Bilirubin LP43561-7
      * Bilirubin total 42719-5 mg/dL
      * Bilirubin total in Serum or Plasma 1975-2 mg/dL
      * Bilirubin conjugated in Serum or Plasma 15152-2 mg/dL
  * Neuromuscular LP31403-6
    * Myelin basic protein LP14685-9
      * Myelin basic protein in Serum 56661-2 ng/mL
      * Myelin basic protein in CSF 2638-5 ng/mL
  * Protein LP15838-3
    * Albumin LP43038-6
      * Albumin in Serum or Plasma 1751-7 g/dL
      * Albumin in Serum or Plasma by Electrophoresis 2862-1 g/dL
    * C reactive protein LP41279-8
      * C reactive protein in Blood by High sensitivity method 71426-1 mg/L
      * C reactive protein in Serum or Plasma 1988-5 mg/L
      * C reactive protein in Serum or Plasma by High sensitivity method 30522-7 mg/L
    * Protein LP69961-8
      * Protein in Serum or Plasma 2885-2 g/dL
* Hematology/Coagulation LP31756-7
  * Hematology LP30786-5
    * Basophils LP48336-9
      * Basophils 26444-0 10^3/uL = k/mm^3
      * Basophils by Automated count 704-7 10^3/uL = k/mm^3
      * Basophils by Manual count 705-4 10^3/uL = k/mm^3
      * Basophils/100 leukocytes 30180-4 %
      * Basophils/100 leukocytes by Automated count 706-2 %
      * Basophils/100 leukocytes by Manual count 707-0 %
    * Eosinophils LP48337-7
      * Eosinophils 26449-9 10^3/uL = k/mm^3
      * Eosinophils by Automated count 711-2 10^3/uL = k/mm^3
      * Eosinophils by Manual count 712-0 10^3/uL = k/mm^3
      * Eosinophils/100 leukocytes 26450-7 %
      * Eosinophils/100 leukocytes by Automated count 713-8 %
      * Eosinophils/100 leukocytes by Manual count 714-6 %
    * ESR LP45671-2
      * ESR 30341-2 mm/h
      * ESR by 15 minute reading 43402-7 mm/15 min
      * ESR by Westergren method 4537-7 mm/h
      * ESR by 2H Westergren method 18184-2 mm/2 h
      * ESR by Wintrobe method 4538-5 mm/h
    * Hematocrit LP45040-0
      * Hematocrit 20570-8 %
      * Hematocrit by Automated count 4544-3 %
    * Hemoglobin LP43135-0
      * Hemoglobin 718-7 g/dL
    * Hemoglobin A1c LP100945-7
      * Hemoglobin A1c in Blood 4548-4 %
      * Hemoglobin A1c in Blood by calculation 17855-8 %
      * Hemoglobin A1c in Blood by HPLC 17856-6 %
      * Hemoglobin A1c in Blood by JDS/JSCC protocol 62388-4 %
      * Hemoglobin A1c in Blood by IFCC protocol 59261-8 %
    * Lymphocytes LP48347-6
      * Lymphocytes 26474-7 10^3/uL = k/mm^3
      * Lymphocytes by Automated count 731-0 10^3/uL = k/mm^3
      * Lymphocytes by Manual count 732-8 10^3/uL = k/mm^3
      * Lymphocytes/100 leukocytes 26478-8 %
      * Lymphocytes/100 leukocytes by Automated count 736-9 %
      * Lymphocytes/100 leukocytes by Manual count 737-7 %
    * MCH LP48918-4
      * MCH 28539-5 pg
      * MCH by Automated count 785-6 pg
    * MCHC LP48919-2
      * MCHC 28540-3 g/dL
      * MCHC by Automated count 786-4 g/dL
    * MCV LP99254-2
      * MCV 30428-7 fL
      * MCV by Automated count 787-2 fL
    * Monocytes LP48349-2
      * Monocytes 26484-6 10^3/uL = k/mm^3
      * Monocytes by Automated count 742-7 10^3/uL = k/mm^3
      * Monocytes by Manual count 743-5 10^3/uL = k/mm^3
      * Monocytes/100 leukocytes 26485-3 %
      * Monocytes/100 leukocytes by Automated count 5905-5 %
      * Monocytes/100 leukocytes by Manual count 744-3 %
    * Neutrophils LP47720-5
      * Neutrophils 26499-4 10^3/uL = k/mm^3
      * Neutrophils by Automated count 751-8 10^3/uL = k/mm^3
      * Neutrophils by Manual count 753-4 10^3/uL = k/mm^3
      * Neutrophils/100 leukocytes 26511-6 %
      * Neutrophils/100 leukocytes by Automated count 770-8 %
      * Neutrophils/100 leukocytes by Manual count 23761-0 %
    * Platelet Count LP7631-7
      * Platelet by Automated count 777-3 10^9/L = k/mm^3
      * Platelet by Manual count 778-1 10^9/L = k/mm^3
    * RBC Count LP7536-8
      * RBC by Automated count 789-8 10^12/L
      * RBC by Manual count 790-6 10^12/L
    * RDW LP46692-7
      * RDW 30384-2 fL
      * RDW by Automated count 21000-5 fL
    * WBC Count LP7720-8
      * WBC by Automated count 6690-2 10^9/L = k/mm^3
      * WBC by Manual count 804-5 10^9/L = k/mm^3
* Microbiology LP31755-9
  * Reagin Ab LP39544-9
    * Reagin Ab in CSF LP47110-9
      * Reagin Ab in CSF [presence] 22459-2 present/absent/indeterminate
      * Reagin Ab in CSF by VDRL [presence] 5290-2 present/absent/indeterminate
      * Reagin Ab in CSF [concentration] 22460-0 U/L
      * Reagin Ab in CSF by VDRL [concentration] 5289-4 U/L
      * Reagin Ab in CSF [titer] 46203-6 titer
      * Reagin Ab in CSF by VDRL [titer] 31146-4 titer
    * Reagin Ab in serum LP41330-9
      * Reagin Ab in Serum [presence] 22461-8 present/absent/indeterminate
      * Reagin Ab in Serum by RPR [presence] 20507-0 present/absent/indeterminate
      * Reagin Ab in Serum by VDRL [presence] 5292-8 present/absent/indeterminate
      * Reagin Ab in Serum [concentration] 22462-6 U/L
      * Reagin Ab in Serum by RPR [concentration] 20508-8 U/L
      * Reagin Ab in Serum by VDRL [concentration] 5291-0 U/L
      * Reagin Ab in Serum [titer] 11084-1 titer
      * Reagin Ab in Serum by RPR [titer] 31147-2 titer
      * Reagin Ab in Serum by VDRL [titer] 50690-7 titer
  * Tuberculosis Interferon LP18171-6
    * Mycobacterium tuberculosis Mitogen stimulated gamma interferon LP71013-4
      * Mycobacterium tuberculosis Mitogen stimulated gamma interferon in Blood [concentration] 39017-9 IU/mL
      * Mycobacterium tuberculosis Mitogen stimulated gamma interferon in Blood [presence] 45323-3 present/absent/indeterminate
    * Mycobacterium tuberculosis stimulated gamma interferon LP149695-1
      * Mycobacterium tuberculosis stimulated gamma interferon in Blood [concentration] 46217-6 IU/mL
      * Mycobacterium tuberculosis stimulated gamma interferon in Blood [presence] 71773-6 present/absent/indeterminate
* Urinalysis LP32744-2
  * Protein in Urine 2888-6 mg/dL
  * Protein in Urine by Test strip [presence] 20454-5 present/absent/indeterminate
  * Protein in 24 hour Urine [g] 2889-4 g/24H
  * Protein in 24 hour Urine [mg] 21482-5 mg/dL
* Virus LP14855-8
  * Hepatitis B virus LP14306-2
    * Hepatitis B virus core LP66853-0
      * Hepatitis B virus core in Serum [presence] 51914-0 present/absent/indeterminate
    * Hepatitis B virus surface Ab LP41149-3
      * Hepatitis B virus surface Ab in Serum [presence] 22322-2 present/absent/indeterminate
      * Hepatitis B virus surface Ab in Serum by Immunoassay [presence] 10900-9 present/absent/indeterminate
      * Hepatitis B virus surface Ab in Serum [concentration] 16935-9 mIU/mL
      * Hepatitis B virus surface Ab in Serum by Immunoassay [concentration] 5193-8 mIU/mL
  * Hepatitis B virus surface Ag LP54058-0
    * Hepatitis B virus surface Ag in Serum [presence] 5195-3 present/absent/indeterminate
    * Hepatitis B virus surface Ag in Serum by Immunoassay [presence] 5196-1 present/absent/indeterminate
    * Hepatitis B virus surface Ag in Serum [concentration] 58452-4 mIU/mL
    * Hepatitis B virus surface Ag in Serum by Immunoassay [concentration] 63557-3 mIU/mL
  * Hepatitis C virus LP14400-3
    * Hepatitis C virus Ab LP38332-0
      * Hepatitis C virus Ab in Serum [presence] 16128-1 present/absent/indeterminate
      * Hepatitis C virus Ab in Serum by Immunoassay [presence] 13955-0 present/absent/indeterminate
      * Hepatitis C virus Ab in Serum by Immunoblot [presence] 5199-5 [presence] present/absent/indeterminate
      * Hepatitis C virus Ab in Serum by Rapid immunoassay [presence] 72376-7 present/absent/indeterminate
      * Hepatitis C virus Ab in Serum [concentration] 22327-1 U/L
      * Hepatitis C virus Ab in Serum by Immunoassay [concentration] 5198-7 U/L
  * HIV LP17126-1
    * HIV 1 Ab LP42700-2
      * HIV 1 Ab in Serum [presence] 7917-8 present/absent/indeterminate
      * HIV 1 Ab in Serum by Immunoassay [presence] 29893-5 present/absent/indeterminate
      * HIV 1 Ab in Serum by Immunoblot [presence] 5221-7 present/absent/indeterminate
      * HIV 1 Ab in Serum by Immunofluorescence [presence] 14092-1 present/absent/indeterminate
      * HIV 1 Ab in Serum, Plasma or Blood by Rapid immunoassay [presence] 68961-2 present/absent/indeterminate
      * HIV 1 Ab in Serum [concentration] 22356-0 U/L
      * HIV 1 Ab in Serum by Immunoassay [concentration] 5220-9 U/L
      * HIV 1 Ab in Serum by Immunofluorescence [concentration] 43599-0 U/L
    * HIV 2 Ab LP47065-5
      * HIV 2 Ab in Serum [presence] 7919-4 present/absent/indeterminate
      * HIV 2 Ab in Serum by Immunoassay [presence] 30361-0 present/absent/indeterminate
      * HIV 2 Ab in Serum by Immunoblot [presence] 5225-8 present/absent/indeterminate
      * HIV 2 Ab in Serum [concentration] 22358-6 U/L
      * HIV 2 Ab in Serum by Immunoassay [concentration] 5224-1 U/L
    * HIV DNA LP55190-0
      * HIV DNA by Probe with amplification [presence] 9836-8 present/absent/indeterminate
