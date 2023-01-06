# Mobile Access Gateway for PMP

Test/demo cases for using the Mobile Access Gateway with the eMedication Service of CARA.
Test patients are currently setup fixed and described [here](mag-emed/testsetupcara.md).

The test instance is available at https://test.ahdis.ch/mag-pmp2/fhir/

There is a GUI which allows to you execute the different functionality directly:
https://test.ahdis.ch/mag-pmp2/#/mag

Verify that you have in settings the correct endpoint, could be the old one because it is 
stored in the browser session: https://test.ahdis.ch/mag-pmp2/#/settings).


## Getting the Current Medication List of a Patient

### 1. Get Patient ID's (EPR-SPID and MPI-PID) based on local identifier (urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001)

IHE PIXm Query [ITI-83] (https Query)

```
https://test.ahdis.ch/mag-pmp2/fhir/fhir/Patient/$ihe-pix?sourceIdentifier=urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001&targetSystem=urn:oid:2.999.756.42.21&targetSystem=urn:oid:2.16.756.5.30.1.127.3.10.3 HTTP/1.1
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
        "reference": "http://test.ahdis.ch/mag-pmp2/fhir/Patient/2.999.756.42.2-CARAMED001"
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
POST https://test.ahdis.ch/mag-pmp2/camel/assertion HTTP/1.1
Scope: resourceId/761337610445502987 purposeOfUse/NORM role/HCP
Accept: application/json;charset=UTF-8
Content-Type: application/xml;charset=UTF-8

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

### 3. Query Medication List or Medication Card with the $find-medication-list operation 

```
https://test.ahdis.ch/mag-pmp2/fhir/DocumentReference/$find-medication-list?status=current&patient.identifier=urn:oid:2.16.756.5.30.1.191.1.0.2.1|c55f4ca7-bd4e-4134-8dcd-56b793ade958
Accept: application/fhir+json
Authorization: Bearer PHNh.....
```
if you wan to query the Medication Card instead of the Medication List you need to add the format parameter

```
https://test.ahdis.ch/mag-pmp2/fhir/DocumentReference/$find-medication-list?status=current&patient.identifier=urn:oid:2.16.756.5.30.1.191.1.0.2.1|c55f4ca7-bd4e-4134-8dcd-56b793ade958&format=urn:oid:2.16.756.5.30.1.127.3.10.10|urn:che:epr:ch-emed:medication-card:2022
Accept: application/fhir+json
Authorization: Bearer PHNh.....
```

### 4. Retrieve Medication List or Medication Card

IHE MHD 68 Document retrieve with url received from above request

```
https://test.ahdis.ch/mag-pmp2/fhir/camel/xdsretrieve?uniqueId=51570022-9b6a-474b-927b-e6a1b193ce16&repositoryUniqueId=2.999.756.42.1
Accept: application/fhir+json
Authorization: Bearer PHNh.....
```

## Updating the medication


### 1. Get Patient ID's (EPR-SPID and MPI-PID) based on local identifier (urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001)

IHE PIXm Query [ITI-83] (https Query)

```
https://test.ahdis.ch/mag-pmp2/fhir/fhir/Patient/$ihe-pix?sourceIdentifier=urn:oid:1.3.6.1.4.1.21367.2017.2.5.83|MAGMED001&targetSystem=urn:oid:2.999.756.42.21&targetSystem=urn:oid:2.16.756.5.30.1.127.3.10.3 HTTP/1.1
Accept: application/fhir+json;charset=UTF-8
Content-Type: application/fhir+json;charset=UTF-8
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
        "reference": "http://test.ahdis.ch/mag-pmp2/fhir/Patient/2.999.756.42.2-CARAMED001"
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
POST https://test.ahdis.ch/mag-pmp2/camel/assertion HTTP/1.1
Scope: resourceId/761337610445502987 purposeOfUse/NORM role/HCP
Accept: application/json;charset=UTF-8
Content-Type: application/xml;charset=UTF-8

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


### 3. Publish CH EMED FHIR document with IHE MHD Provide Document Bundle transaction

The document has to be submitted according to the IHE MHD Provide Document Bundle [ITI-65](http://fhir.ch/ig/ch-epr-mhealth/iti-65.html) transaction with the following special considerations for each of the resource elements within the Bundle. As a Document Source you need to provide different identifiers:

- Adjust Mapping with List to DocumentManifest

| Resource Element  | Value  |
|---|---|
| Binary.contentType | text/xml |
| Binary.data |  Base64 encoded CDA according to above step |
| List.extension | [author role extension](http://fhir.ch/ig/ch-epr-mhealth/StructureDefinition/ch-ext-author-authorrole) |
| List.extension | [ihe-sourceId](http://profiles.ihe.net/ITI/MHD/StructureDefinition/ihe-sourceId) |
| List.extension | [ihe-designationType](http://profiles.ihe.net/ITI/MHD/StructureDefinition/ihe-designationType) |
| List.identifier | unique oid generated by Document Source |
| List.identifier | unique uuid generated by Document Source |
| List.status| current |
| List.subject.reference | targetID from PIXm call (see sep 1)|
| DocumentReference.identifier | uuid of Document (Bundle.identifier.value as uniqueId for XDS |
| DocumentReference.status | current|
| DocumentReference.date | Bundle.Composition.date |
| DocumentReference.subject | targetID from PIXm call (see step 1)|
| DocumentReference.content.attachment.creation |  Bundle.Composition.date |
 DocumentReference.content.format | DocumentEntry.formatCode, see table below  |
| DocumentReference.author| reference to contained PractitionerRole |
| DocumentReference.type | [XDS typeCode](https://fhir.ch/ig/ch-epr-term/ValueSet-DocumentEntry.typeCode.html), see table below |
| DocumentReference.category | [XDS classCode](https://fhir.ch/ig/ch-epr-term/ValueSet-DocumentEntry.classCode.html), see table below |
| DocumentReference.securityLabel | [XDS confidentialityCode](https://fhir.ch/ig/ch-epr-term/ValueSet-DocumentEntry.confidentialityCode.html)  | 


See the [cara emed-service-guide](https://cara-ch.github.io/emed-service-guide/transactions/) for Document formatCode, DocumentEntry.classCode and DocumentEntry.typeCode:


See [mtp-submit.json](pmp-pharm/mtp-submit.json) for a Provide Document Bundle message example.

The Provide Document Bundle message is sent to the base URL as defined in FHIR. See http://hl7.org/fhir/R4/http.html for the definition of “HTTP” access methods and “base”.

```
POST https://test.ahdis.ch/mag-pmp2/fhir/
Accept: application/fhir+json;charset=UTF-8
Content-Type: application/fhir+json;charset=UTF-8
Authorization: Bearer PHN...

```

The server returns a HTTP Status code appropriate to the processing outcome, conforming to the transaction specification requirements as specified in http://hl7.org/fhir/R4/http.html#transaction


### Logs

You can access any logs also directly at https://pmp.posttenebrassilico.ch/pmp2/mhd/logs.

### Copy cubernetes log from testinstance

kubectl cp mag-pmp-84ccc7fdbd-jc7wl:logs ./pmplogs/

kubectl cp mag-pmp-5796cd7d5f-gjjqz:logs ./pmplogs/


kubectl cp mag-pmp-5796cd7d5f-8wvp6:logs ./pmplogs/
kubectl logs --follow mag-pmp-5796cd7d5f-8wvp6

kubectl exec --stdin --tty mag-pmp-84ccc7fdbd-jc7wl -- /bin/sh
