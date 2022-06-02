
Testsetup Cara for PMP
======================

You can access all data via https://test.ahdis.ch/matchbox/#/mag, you need to configure https://test.ahdis.ch/mag-pmp/fhir for the Mobile Access Gateway and
https://test.ahdis.ch/matchbox/fhir for FHIR Server in https://test.ahdis.ch/matchbox/#/settings. Settings are stored in browser for the next tim.

| First Name |  Last name  | Gender  | DOB     | EPR-SPID (2.16.756.5.30.1.127.3.10.3) | MPI-PID (2.16.756.5.30.1.191.1.0.2.1)  | CHUV (2.16.756.5.30.1.196.3.2.1) | usage |
|------------|--------------|---------|---------|---------------------------------------|--------------------------|-------------------------------------------|----------|
| Jett Flynn| Sesztáková        | male       | 1993-01-27 | 761337615758291047                    | c55f4ca7-bd4e-4134-8dcd-56b793ade958             |  MAGMED006 | chuv - demo   |
| Leandra Corina  | Behluli-Qazimi         | female    | 2002-12-21  | 761337611932009095                    | 7a4ec59f-a024-4cfb-bc04-3339c53cb9ac               |  MAGMED005 | chuv - export |
| Romuald René Guy  | MUELLER-PATTI         | male    |1993-09-2  | 761337614574943741                    |    50987ab8-3344-4349-8aaa-cc3bc9d9dec8               |  MAGMED007 | chuv - no appc doc |
| Loris Bertrand  | PALOLA        |   male   | 1995-05-23  | 761337617206922169                    |  68e0258d-20c6-4f6c-8740-00e9e0f0d29f                 |  MAGMED010 | documedis - patient  |
| Trong San  | NEFF-WINGEIER        |      |   | 761337611735842172                    | e7963774-9098-445f-9cab-5d52234b52c3   |  MAGMED011 | documedis - patient |

1. Patient has to be setup in CARA, patient should be visible via PDQm Queries, e.g:

  - you need to set also https://test.ahdis.ch/mag-pmp/fhir in settings for FHIR Server
  - you need to register your local id for your organization (e.g. MAGMED005)
    seaarch patient with pdq https://test.ahdis.ch/matchbox/#/patients (for this 
  - then you can get the EPRS-PID (2.16.756.5.30.1.127.3.10.3) and MPI-PID (2.16.756.5.30.1.191.1.0.2.1)
  - perform a PIXm Query with sourceIdentifier system 2.16.756.5.30.1.127.3.10.3 and add the sourceIdentifier value from above in https://test.ahdis.ch/matchbox/#/mag
  - click on getPatient
  - on opening box add local PID system in sourceIdentifier.system and PID value in sourceIdentifier.value
  - select PIXm Feed add Identifier 
  - if you the patient is registered, you should be able to query it in the MAG Mobile Access Gateway - Patient Identifiers, enter the local id MAGMED005 and you should get via the PIXm Query back the MPI-ID, the EPR-SPID and the targetID


2. Setup for CARA PMP

- Authenticate as Patient 
- To check select 'Patient in the Mobile Access Gateway - Authenticate' Patient and perform a Query, if you get back: `The patient ID in the search query does not match the auth` the simulated patient access is not working then relation between the EPRS-PID and MPI-PID needs to be configured for the PMP (send an email with the data to quentin), for the current setup we use for simulated Patient access a constructed SAML assertion and this step should not be necessary anymore
- You need to upload an APPC document that the Patient participates in the PMP, see pmp-pharm\*-appc.xml, you need to replace the uuid's for a new patient and add the EPPR-SPID
- If you click on Document References you should see the APPC document
- If you click on Query Medication List you should get one entry

### trouble shooting
if there are any pmp problems check also https://sct-form.hcuge.ach/sharedtreatmentplan/mhd/logs currently: https://pmp.posttenebrassilico.ch/pmp/mhd/logs
if logs are reverted: https://www.browserling.com/tools/text-reverse

### HP setup

https://epr.cara.int.post-ehealth.ch/



