# Mobile Access Gateway for PMP

Test/demo cases for using the Mobile Access Gateway with the eMedication Service of CARA

## Getting the Current Medication List of a Patient


1. Get Access Token

[ ] To be clarified

2. Get Patient ID

IHE PIXm Query [ITI-83] (https Query)

3. Query Medication List
IHE MHD DocRef Query according to PHARM-5
```
https://test.ahdis.ch/mag-pmp/fhir/DocumentReference/$find-medication-list?status=current&patient.identifier=urn:oid:2.999.756.42.2|12345678
```

4. Retrieve Medication List
IHE MHD 68 Document retreive
```
https://test.ahdis.ch/mag-pmp/fhir/camel/xdsretrieve?uniqueId=51570022-9b6a-474b-927b-e6a1b193ce16&repositoryUniqueId=2.999.756.42.1
```

5. Convert CDA to FHIR


OAuth or XUA, needs to be clarified by spec/project


IHE MHD RetrieveDoc Query [ITI-68] (https GET)
FHIR API $transform Operation


## Updating the medication

[ ] Get Access Token

[ ] Get Patient ID

[ ] Convert FHIR to CDA

[ ] Provide Document




