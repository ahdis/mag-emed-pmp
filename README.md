# Mobile Access Gateway for PMP

Test/demo cases for using the Mobile Access Gateway with the eMedication Service of CARA

## Getting the Current Medication List of a Patient


1. Get Access Token

Same as in EPR Context (needs to be defined)

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

FHIR API $transform Operation

```
POST https://test.ahdis.ch/r4/StructureMap/$transform?source=http://fhir.ch/ig/cda-fhir-maps/StructureMap/CdaChEmedMedicationListDocumentToBundle
Accept: application/fhir+json;fhirVersion=4.0
Content-Type: application/fhir+xml;fhirVersion=4.0
```


## Updating the medication

[ ] Get Access Token

[ ] Get Patient ID

[ ] Convert FHIR to CDA

[ ] Provide Document




