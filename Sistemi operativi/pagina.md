4 Kb di memoria, quindi 12 bit di offset



Se il numero di pagine virtuali dei processi eccede il numero di pagine disponibili nella memoria, allora alcune pagine devono risiedere su disco, se l'accesso alla memoria appartiene ad una pagina non residente si genera un [[Interrupt]] di segnalazione errore **page fault**.

Lo spazio su disco per contenere le pagine virtuali è detto swap file ed è gestito dal [[sistema operativo]]

Se la pagina è su disco ha un bit di validità impostato a 0.

| valido | pagina fisica o indirizzo su disco |
| ------ | ---------------------------------- |
| 1      | -> mem                             |
| 1      | -> mem                             |
| 1      | ->mem                              |
| 1      | ->mem                              |
| 0      | -> disc                            |
| 1      | -> mem                             |
| 1      | ->mem                              |
| 0      | -> disc                            |
| 1      | -> mem                             |
| 1      | -> mem                             |
| 1      | ->mem                              |
| 0      | -> disc                            |
| 1      | -> mem                             |

