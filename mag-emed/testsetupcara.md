
Testsetup Cara for PMP
======================

You can access all data via https://test.ahdis.ch/matchbox/#/mag, you need to configure https://test.ahdis.ch/mag-pmp-int/fhir for the Mobile Access Gateway and
https://test.ahdis.ch/matchbox/fhir for FHIR Server in https://test.ahdis.ch/matchbox/#/settings. Settings are stored in browser for the next tim.

| First Name |  Last name  | Gender  | DOB     | EPR-SPID (2.16.756.5.30.1.127.3.10.3) | MPI-PID (2.16.756.5.30.1.191.1.0.2.1)  | CHUV (2.16.756.5.30.1.196.3.2.1) | usage |
|------------|--------------|---------|---------|---------------------------------------|--------------------------|-------------------------------------------|----------|
| Jett Flynn| Sesztáková        | male       | 1993-01-27 | 761337615758291047                    | c55f4ca7-bd4e-4134-8dcd-56b793ade958             |  MAGMED006 | chuv - demo   |
| Leandra Corina  | Behluli-Qazimi         | female    | 2002-12-21  | 761337611932009095                    | 7a4ec59f-a024-4cfb-bc04-3339c53cb9ac               |  MAGMED005 | chuv - export |
| Romuald René Guy  | MUELLER-PATTI         | male    |1993-09-2  | 761337614574943741                    |    50987ab8-3344-4349-8aaa-cc3bc9d9dec8               |  MAGMED007 | chuv - no appc doc |
| Loris Bertrand  | PALOLA        |   male   | 1995-05-23  | 761337617206922169                    |  68e0258d-20c6-4f6c-8740-00e9e0f0d29f                 |  MAGMED010 | documedis - patient  |
| Trong San  | NEFF-WINGEIER        |      |   | 761337611735842172                    | e7963774-9098-445f-9cab-5d52234b52c3   |  MAGMED011 | documedis - patient |
| BRUNO KAKOB| Aegerter-Bischoff | | 23.11.1983 | 761337613917063504 | 64370848-bed5-46c4-972f-05b410b59235 |  CHUV001 | 
| NABIHA| KRAFT-BRUHIN | | 22.06.1980 | 761337610392231008 |    bac643ea-6692-4016-b434-6a022b64b5a0 |  CHUV002 | 
 | TOLOMEY JOHN| Monney-Margueron | | 01.04.1978 | 761337617150124497 | 1abb1e0f-86e1-4a9e-8ae4-94f532cec483 | CHUV003 | 
 | SALOME ANJA| Klemenz | | 15.09.1988 | 761337619872617110 | eebf95b0-d408-44e9-b1be-6a941ea65325 |  CHUV004 | 
 | FU-HUI| MURATORE-SCHIAVONE | | 14.06.1972 | 761337610975948651 | b199886e-982f-41a2-b79d-c7fe58c25266  | CHUV005 | 
 | Filippa Aurelia| STEINER-BAECHLER | | 18.02.1990 | 761337616538595232 | c1d1b2f0-377d-4eb4-918a-4632e4c95c7c | CHUV006 | 
 | SAFIRA| SEGMUELLER | | 05.09.1969 | 761337614430418338 |  02add961-9bcf-4ebe-82f1-2f2eeabddc41  | CHUV007 | 
 | Urs Syed | ACIOLI PEREIRA | | 12.06.2005 | 761337610360664012 | 46d8e9d7-3a7f-4ab1-b5ee-2f87175a6490  | CHUV008 | 
 | YANEK SOLAR| WEBER-LEDERGERBER | | 29.05.1991 | 761337612107906324 |22701467-5f85-4818-8cd5-202d86c4decc |  CHUV009 | 
 | SIMONE KEREN | Stauffacher | | 12.05.1973 | 761337614443482272 | 23f31e1b-c483-4f87-8996-9413415552a1  | CHUV010 | 
 | DANAIL DIMITROV	 | Kitchaleun	| | 1.02.1988 |	761337611206906525 | 76be7dfe-d8be-4901-b8f9-b20c76db0435 | HCI001 |
 | ETIENNE ALEKSANDER	 | ACKERMANN-GROSSENBACHER	| | 18.02.1967|	761337610343729455 |  3f6f46d9-0912-4b9f-8d0b-1da03153f095 | HCI002 |
 | Dominique Jean Didier	 | HUBER-GUSCETTI	| | 01.01.2010 |	761337617347225136 | 80d4c907-a928-42bf-8a98-a381496b5e74 | HCI003 |
 | Jérôme Jean Patrice Pierre | 	KONE-FRIEDLI	| | 07.04.1980 |	761337614643047219 | 6aa579e0-4f0f-4b01-8184-76b606641ba6 | HCI004 |



| First Name |  Last name  | Gender  | DOB     | EPR-SPID (2.16.756.5.30.1.127.3.10.3) | MPI-PID (2.16.756.5.30.1.191.1.0.2.1)  | EPRIK (urn:oid:2.16.756.5.30.1.999.90) | usage |
|------------|--------------|---------|---------|---------------------------------------|--------------------------|-------------------------------------------|----------|
| Véronique | Nelly Lüscher-Lienhard        | female       | 2008-10-27 | 761337613909176847                    | 0f3d4999-18f9-4aaa-8938-f5db052f9964             |  CARAPMP001 | caa - demo   |



1. Patient has to be setup in CARA, patient should be visible via PDQm Queries, e.g:

  - you need to set also https://test.ahdis.ch/mag-pmp_int/fhir in settings for FHIR Server
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
if there are any pmp problems check also: https://ws-pmp-int.cara.ch/pmp2/mhd/logs
if logs are reverted: https://www.browserling.com/tools/text-reverse

### HP setup

https://epr.cara.int.post-ehealth.ch/



