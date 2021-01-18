Six test patients are setup in the CARA PMP with an EPRS_PID which is out of test
data of the reference environment. This allows to get an Assertion from the validator.

| First Name |  Last name  | Gender  | DOB     | EPR-SPID (2.16.756.5.30.1.127.3.10.3) | MPI-PID (2.999.756.42.2)  | local I4MI (1.3.6.1.4.1.21367.2017.2.5.83) |
|------------|--------------|---------|---------|---------------------------------------|--------------------------|-------------------------------------------|
| BERGAN     | OVIE         | Male    | 3/29/0  | 761337610435209810                    | CARAMED001               |  MAGMED001 |
| Léo Gérard | Avdic        | U       | 10/15/80| 761337610436974489                    | CARAMED002               |  MAGMED002 | 
| Marie-Christelle Victoire  | Aschwanden-Stocker   |  Female | 8/20/95  | 761337610430891416 | CARAMED003         |  MAGMED003 |
| Gebhard August  | Antonyova  | Male  | 10/14/95  | 761337610423590456 | CARAMED004                               |  MAGMED004 | 
| Alessandra Monica  | Amrein-Brunner  | Unknown  | 6/8/13 | 761337610455909127 | CARAMED005                       |  MAGMED005 |
| Salome Anja |  Ebibi-Limani | Female  | 8/16/76  | 761337610445502987 | CARATEST001                              |  MAGTEST001 |

CARAMED001: One MTP item according to Use Case [8.2.1](http://build.fhir.org/ig/hl7ch/ch-emed/usecase-german.html#erstbesuch-beim-hausarzt)
CARAMED002: MTP item canceled with [PADV](http://build.fhir.org/ig/hl7ch/ch-emed/usecase-german.html#kontrolle-hausarzt) 
CARAMED003: CARA’s scenario [documents 1-15](https://github.com/hl7ch/hl7ch-cda/tree/master/projects/Cara/v2020-11-20-WIP)