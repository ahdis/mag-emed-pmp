# Mobile Access Gateway for PMP

Test/demo cases for using the Mobile Access Gateway with the eMedication Service of CARA.
Test patients are currently setup fixed and described [here](mag-emed/testsetupcara.md)

## Getting the Current Medication List of a Patient

### 1. Get Patient ID's (EPR-SPID and MPI-PID) based on local identifier (urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001)

IHE PIXm Query [ITI-83] (https Query)

```
https://test.ahdis.ch/mag-pmp/fhir/fhir/Patient/$ihe-pix?sourceIdentifier=urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001&targetSystem=urn:oid:2.999.756.42.21&targetSystem=urn:oid:2.16.756.5.30.1.127.3.10.3 HTTP/1.1
Accept: application/fhir+json
```
returns identifiers for EPR-SPID (2.16.756.5.30.1.127.3.10.3) and MPI-ID (2.999.756.42.2)

```json
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "targetIdentifier",
      "valueIdentifier": {
        "system": "urn:oid:2.16.756.5.30.1.127.3.10.3",
        "value": "761337610435209810"
      }
    },
    {
      "name": "targetId",
      "valueReference": {
        "reference": "http://test.ahdis.ch/mag-pmp/fhir/Patient/2.999.756.42.2-CARAMED001"
      }
    },
    {
      "name": "targetIdentifier",
      "valueIdentifier": {
        "system": "urn:oid:2.999.756.42.2",
        "value": "CARAMED001"
      }
    }
  ]
}
```

### 2. Get Access Token based on Authenticated Healthcare Professional 

Get Assertion based on IdP SAML token, here saml token is abbreviated for testing, Patient (resourceId as EPR-SPID), Role (NORM) and PurposeOfUse (HCP) for Health Professional who is identified with GLN 7601002469191

```
POST https://test.ahdis.ch/mag-pmp/camel/assertion HTTP/1.1
Scope: resourceId/761337610445502987 purposeOfUse/NORM role/HCP
Accept: application/json
Content-Type: application/xml

<saml2:Assertion xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion" Version="2.0">
   <saml2:AttributeStatement>
      <saml2:Attribute FriendlyName="GLN" Name="GLN"
            NameFormat="urn:oasis:names:tc:ebcore:partyid-type:DataUniversalNumberingSystem:0060">
      <saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xsd:string">7601002469191</saml2:AttributeValue>
               </saml2:Attribute>
   </saml2:AttributeStatement>
</saml2:Assertion>
```

returns IHE-SAML access token for the specified scope:

```json
{
  "access_token": "PHNh.....",
  "token_type": "IHE-SAML",
  "expires_in": 60000,
  "scope": "resourceId/761337610435209810 purposeOfUse/NORM role/HCP"
}
```

### 3. Query Medication List or Medication Card with the $find-medication-list operation 

```
https://test.ahdis.ch/mag-pmp/fhir/DocumentReference/$find-medication-list?status=current&patient.identifier=urn:oid:2.999.756.42.2|CARAMED001
Accept: application/fhir+json
Authorization: IHE-SAML PHNh.....
```
if you wan to query the Medication Card instead of the Medication List you need to add the format parameter

```
https://test.ahdis.ch/mag-pmp/fhir/DocumentReference/$find-medication-list?status=current&patient.identifier=urn:oid:2.999.756.42.2|CARAMED001&format=urn:oid:2.16.756.5.30.1.127.3.10.10|urn:ch:cda-ch-emed:medication-card:2018
Accept: application/fhir+json
Authorization: IHE-SAML PHNh.....
```

### 4. Retrieve Medication List or Medication Card

IHE MHD 68 Document retrieve with url received from above request

```
https://test.ahdis.ch/mag-pmp/fhir/camel/xdsretrieve?uniqueId=51570022-9b6a-474b-927b-e6a1b193ce16&repositoryUniqueId=2.999.756.42.1
Accept: application/fhir+json
Authorization: IHE-SAML PHNh.....
```

### 5. Convert CDA to FHIR

FHIR API $transform Operation

```
POST https://test.ahdis.ch/r4/StructureMap/$transform?source=http://fhir.ch/ig/cda-fhir-maps/StructureMap/CdaChEmedMedicationListDocumentToBundle
Accept: application/fhir+json;fhirVersion=4.0
Content-Type: text/xml
```

## Updating the medication


### 1. Get Patient ID's (EPR-SPID and MPI-PID) based on local identifier (urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001)

IHE PIXm Query [ITI-83] (https Query)

```
https://test.ahdis.ch/mag-pmp/fhir/fhir/Patient/$ihe-pix?sourceIdentifier=urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001&targetSystem=urn:oid:2.999.756.42.21&targetSystem=urn:oid:2.16.756.5.30.1.127.3.10.3 HTTP/1.1
Accept: application/fhir+json
Content-Type: application/fhir+json
```
returns identifiers for EPR-SPID (2.16.756.5.30.1.127.3.10.3) and MPI-ID (2.999.756.42.2)

```json
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "targetIdentifier",
      "valueIdentifier": {
        "system": "urn:oid:2.16.756.5.30.1.127.3.10.3",
        "value": "761337610435209810"
      }
    },
    {
      "name": "targetId",
      "valueReference": {
        "reference": "http://test.ahdis.ch/mag-pmp/fhir/Patient/2.999.756.42.2-CARAMED001"
      }
    },
    {
      "name": "targetIdentifier",
      "valueIdentifier": {
        "system": "urn:oid:2.999.756.42.2",
        "value": "CARAMED001"
      }
    }
  ]
}
```

### 2. Get Access Token based on Authenticated Healthcare Professional 

Get Assertion based on IdP SAML token, here SAML token is abbreviated for testing, Patient (resourceId as EPR-SPID), Role (NORM) and PurposeOfUse (HCP) for Health Professional who is identified with GLN 7601002469191

```
POST https://test.ahdis.ch/mag-pmp/camel/assertion HTTP/1.1
Scope: resourceId/761337610445502987 purposeOfUse/NORM role/HCP
Accept: application/json
Content-Type: application/xml

<saml2:Assertion xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion" Version="2.0">
   <saml2:AttributeStatement>
      <saml2:Attribute FriendlyName="GLN" Name="GLN"
            NameFormat="urn:oasis:names:tc:ebcore:partyid-type:DataUniversalNumberingSystem:0060">
      <saml2:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xsd:string">7601002469191</saml2:AttributeValue>
               </saml2:Attribute>
   </saml2:AttributeStatement>
</saml2:Assertion>
```

returns XUA Authorization Assertion for the specified scope:

```json
{
  "access_token": "PHNh.....",
  "token_type": "IHE-SAML",
  "expires_in": 60000,
  "scope": "resourceId/761337610435209810 purposeOfUse/NORM role/HCP"
}
```

### 3. Convert FHIR to CDA

FHIR API $transform Operation

The following maps can be used to transform the different type of documents

| Document  | Map  |
|---|---|
| [Medication Treatment Plan document](http://fhir.ch/ig/ch-emed/medication-treatment-plan-document.html)  |  [BundleToCdaChEmedMedicationTreatmentPlanDocument](http://fhir.ch/ig/cda-fhir-maps/StructureMap/BundleToCdaChEmedMedicationTreatmentPlanDocument) |
| [Medication Prescription document](http://fhir.ch/ig/ch-emed/medication-prescription-document.html) |  [BundleToCdaChEmedMedicationPrescriptionDocument](http://fhir.ch/ig/cda-fhir-maps/StructureMap/BundleToCdaChEmedMedicationPrescriptionDocument) |
| [Medication Dispense document](http://fhir.ch/ig/ch-emed/medication-dispense-document.html) |  [BundleToCdaChEmedMedicationDispenseDocument](http://fhir.ch/ig/cda-fhir-maps/StructureMap/BundleToCdaChEmedMedicationDispenseDocument) |
| [Pharmaceutical Advice document](http://fhir.ch/ig/ch-emed/pharmaceutical-advice-document.html) |  [BundleToCdaChEmedPharmaceuticalAdviceDocument](http://fhir.ch/ig/cda-fhir-maps/StructureMap/BundleToCdaChEmedPharmaceuticalAdviceDocument) |
| [Medication Card document](http://fhir.ch/ig/ch-emed/medication-card-document.html) | [BundleToCdaChEmedMedicationCardDocument](http://fhir.ch/ig/cda-fhir-maps/StructureMap/BundleToCdaChEmedMedicationCardDocument) |

```
POST https://test.ahdis.ch/r4/StructureMap/$transform?source=http://fhir.ch/ig/cda-fhir-maps/StructureMap/BundleToCdaChEmedMedicationDispenseDocument
Content-Type: application/fhir+json;fhirVersion=4.0
Accept: text/xml

< ./pmp-pharm/Bundle-1-2-MedicationDispense.json
```

### 4. Publish CDA document with IHE MHD Provide Document Bundle transaction

The document has to be submitted according to the IHE MHD Provide Document Bundle [ITI-65](http://fhir.ch/ig/ch-epr-mhealth/iti-65.html) transaction with the following special considerations for each of the resource elements within the Bundle. As a Document Source you need to provide different identifiers:

| Resource Element  | Value  |
|---|---|
| Binary.contentType | text/xml |
| Binary.data |  Base64 encoded CDA according to above step |
| DocumentManifest.extension | [author role extension](http://fhir.ch/ig/ch-epr-mhealth/StructureDefinition/ch-ext-author-authorrole) |
| DocumentManifest.masterIdentifier | unique oid generated by Document Source |
| DocumentManifest.identifier | unique uuid generated by Document Source |
| DocumentManifest.status| current |
| DocumentManifest.type| Procedure |
| DocumentManifest.created| Publish time from Document Source |
| DocumentManifest.subject.reference | targetID from PIXm call (see sep 1)|
| DocumentManifest.source | oid of Document Source |
| DocumentReference.masterIdentifier | uuid of Document (Bundle.identifier.value or CDA.id.root) used as uniqueId for XDS |
| DocumentReference.identifier |  optional,  corresponds to XDS entryUUID, when the DocumentReference.identifier carries the entryUUID then the DocumentReference.identifier use shall be ‘official’|
| DocumentReference.status | current|
| DocumentReference.date | Bundle.Composition.date |
| DocumentReference.subject | targetID from PIXm call (see step 1)|
| DocumentReference.content.attachment.creation |  Bundle.Composition.date |
 DocumentReference.content.format | DocumentEntry.formatCode, see table below  |
| DocumentReference.author| |
| DocumentReference.type | [XDS typeCode](https://fhir.ch/ig/ch-epr-term/ValueSet-DocumentEntry.typeCode.html), see table below |
| DocumentReference.category | [XDS classCode](https://fhir.ch/ig/ch-epr-term/ValueSet-DocumentEntry.classCode.html), see table below |
| DocumentReference.securityLabel | [XDS confidentialityCode](https://fhir.ch/ig/ch-epr-term/ValueSet-DocumentEntry.confidentialityCode.html)  | 


The following codes are used in the PMP for the CDA documents:


|     Document type                           |     DocumentEntry.classCode                  |     DocumentEntry.typeCode                                      |     DocumentEntry.formatCode               |
|---------------------------------------------|--------------------------------------------------|---------------------------------------------------------------------|------------------------------------------------|
|     MTP Medication    Treatment Plan        |     440545006     (Prescription record)          |     419891008     (Record artifact)                                 |     urn:ihe:pharm:mtp:2015                     |
|     PRE Medication    Prescription          |     440545006     (Prescription record)          |     761938008    Medicinal Prescription record (record artifact)    |     urn:ihe:pharm:pre:2010                     |
|     DIS Medication    Dispense              |     440545006     (Prescription record)          |     419891008     (Record artifact)                                 |     urn:ihe:pharm:dis:2010                     |
|     PADV Community Pharmaceutical Advice    |     440545006     (Prescription record)          |     419891008     (Record artifact)                                 |     urn:ihe:pharm:padv:2010                    |
|     PML Community Medication List           |     422735006     (Summary clinical document)    |     721912009     (Medication summary document)                     |     urn:ihe:pharm:pml:2013                     |
|     Medication Card (PMLC)                  |     422735006     (Summary clinical document)    |     721912009     (Medication summary document)                     |     urn:ch:cda-ch-emed:medication-card:2018    |


See [CARAMED001.1-1-MedicationTreatmenPlan.mhd.json](pmp-pharm/CARAMED001.1-1-MedicationTreatmenPlan.mhd.json) for a Provide Document Bundle message example.

The Provide Document Bundle message is sent to the base URL as defined in FHIR. See http://hl7.org/fhir/R4/http.html for the definition of “HTTP” access methods and “base”.

```
POST https://test.ahdis.ch/mag-pmp/fhir/
Accept: application/fhir+json
Content-Type: application/fhir+json
Authorization: IHE-SAML PHN...

```

The server returns a HTTP Status code appropriate to the processing outcome, conforming to the transaction specification requirements as specified in http://hl7.org/fhir/R4/http.html#transaction
