Three test patients are setup in the CARA PMP with an EPRS_PID which is out of test
data of the reference environment. This allows to get an Assertion from the validator.

| First Name |  Last name  | Gender  | DOB     | EPR-SPID (2.16.756.5.30.1.127.3.10.3) | MPI-PID (2.16.756.5.30.1.191.1.0.2.1)  | CHUV (2.16.756.5.30.1.196.3.2.1) |
|------------|--------------|---------|---------|---------------------------------------|--------------------------|-------------------------------------------|
| BERGAN     | OVIE         | Male    | 3/29/02  | 761337610435209810                    | 713d79be-058e-4f55-82a8-e1f81f5e0047               |  MAGMED001 |
| Léo Gérard | Avdic        | U       | 10/15/80| 761337610436974489                    | 07a07f53-2bd1-4a8d-8b02-f7e639120da1               |  MAGMED002 | 
| Marie-Christelle Victoire  | Aschwanden-Stocker   |  Female | 8/20/95  | 761337610430891416 | f733750f-4b04-4bf5-9eac-abdaddf3d0a2         |  MAGMED003 |

MAGMED001: One MTP item according to Use Case [8.2.1](http://build.fhir.org/ig/hl7ch/ch-emed/usecase-german.html#erstbesuch-beim-hausarzt), but with morning coded as AC instead of Morn
