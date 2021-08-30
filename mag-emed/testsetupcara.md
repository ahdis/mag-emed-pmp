Three test patients are setup in the CARA PMP with an EPRS_PID which is out of test
data of the reference environment. This allows to get an Assertion from the validator.

| First Name |  Last name  | Gender  | DOB     | EPR-SPID (2.16.756.5.30.1.127.3.10.3) | MPI-PID (2.16.756.5.30.1.191.1.0.2.1)  | CHUV (2.16.756.5.30.1.196.3.2.1) |
|------------|--------------|---------|---------|---------------------------------------|--------------------------|-------------------------------------------|
| BERGAN     | OVIE         | Male    | 3/29/02  | 761337610435209810                    | assignedByCara               |  MAGMED001 |
| Léo Gérard | Avdic        | U       | 10/15/80| 761337610436974489                    | assignedByCara               |  MAGMED002 | 
| Marie-Christelle Victoire  | Aschwanden-Stocker   |  Female | 8/20/95  | 761337610430891416 | assignedByCara         |  MAGMED003 |

CARAMED001: One MTP item according to Use Case [8.2.1](http://build.fhir.org/ig/hl7ch/ch-emed/usecase-german.html#erstbesuch-beim-hausarzt)
CARAMED002: MTP item canceled with [PADV](http://build.fhir.org/ig/hl7ch/ch-emed/usecase-german.html#kontrolle-hausarzt) 
CARAMED003: CARA’s scenario [documents 1-15](https://github.com/hl7ch/hl7ch-cda/tree/master/projects/Cara/v2020-11-20-WIP)