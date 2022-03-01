

Two test patients are setup in the CARA PMP with an EPRS_PID which is out of test
data of the reference environment. This allows to get an Assertion from the validator.


New in 2022:

| First Name |  Last name  | Gender  | DOB     | EPR-SPID (2.16.756.5.30.1.127.3.10.3) | MPI-PID (2.16.756.5.30.1.191.1.0.2.1)  | CHUV (2.16.756.5.30.1.196.3.2.1) | usage |
|------------|--------------|---------|---------|---------------------------------------|--------------------------|-------------------------------------------|----------|
| Jett Flynn| Sesztáková        | male       | 1993-01-27 | 761337615758291047                    | c55f4ca7-bd4e-4134-8dcd-56b793ade958             |  MAGMED006 | demo   |
| Leandra Corina  | Behluli-Qazimi         | female    | 2002-12-21  | 761337611932009095                    | 7a4ec59f-a024-4cfb-bc04-3339c53cb9ac               |  MAGMED005 | export |
| Romuald René Guy  | MUELLER-PATTI         | male    |1993-09-2  | 761337614574943741                    |    50987ab8-3344-4349-8aaa-cc3bc9d9dec8               |  MAGMED007 | no appc doc |



1. Patient has to be setup in CARA, patient should be visible via PDQm Queries, e.g:

  - select in Settings of app  the Mobile Access Gateway, e.g. http://localhost:9090/mag-pmp/fhir for the FHIR Server and Mobile Access Gatway, by clicking on the patient you get the detailed information
  - you need to register your local id for your organization (e.g. MAGMED005), this can be either via PMIR Feed (should be deprecated) or via the new PIXm Feed (in development)
  - if the patient is registered, you should be able to query it in the MAG Mobile Access Gateway - Patient Identifiers, enter the local id MAGMED005 and you should get via the PIXm Query back the MPI-ID, the EPR-SPID and the targetID


2. Setup for CARA PMP

- The relation between the EPRS-PID and MPI-PID needs to be configured for the PMP (send an email with the data to quentin), for the current setup we use for simulated Patient access a constructed SAML assertion
- To check select 'Patient in the Mobile Access Gateway - Authenticate' Patient and perform a Query, if you get back: `The patient ID in the search query does not match the auth` the simulated patient access is not working
- You need to upload an APPC document that the Patient participates in the PMP, see pmp-pharm\*-appc.xml
- If you click on Query Medication List you should get one entry


if there are any pmp problems check also https://sct-form.hcuge.ch/sharedtreatmentplan/mhd/logs





