---
alias: banco di registri
---
Il register file, o banco di registri, è la struttura in cui vengono organizzati i [[registro|registri]], in [[RISC-V]] sono 32 registri da 64 bit ciascuno.
Ogni registro identificato da un indirizzo di 5 bit, le operazioni possibili sui singoli registri sono:
- Lettura: i 64 bit memorizzati nel  register file nel registro inidirizzato vengono presentati in uscita
- Scrittura: i 64 bit acquisiti in ingresso nel register file all'registro indirizzato come destinazione

Queste operazioni avvengono attraverso le porte di lettura e scrittura, nel risc-V ci sono due [[porta di lettura|porte di lettura]] e una [[porta di scrittura]].


