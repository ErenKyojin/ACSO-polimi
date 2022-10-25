# Struttura base del processore

![[Pasted image 20221025150659.png|600]] 

Memoria istruzioni separata dalla [[memoria]] dati e [[Register file]] con banchi da 32 registri a 64 bit. Due porte di lettura ed una in scrittura.

Alcune istruzioni ([[istruzioni]] di formato I, S, B) hanno necessità di estendere l'immediato a 64 bit, questo viene fatto dal modulo di estensione segno, che inoltre shifta a sinistra il formato B, il modulo prende per ingresso tutta l'istruzione in quanto ha bisogno di sapere quale istruzione si sta eseguendo (vengono ricostruite in modo diverso)

Aggiungiamo poi:
- un [[MUX]] (mux A) al secondo ingresso dell'alu per scegliere se il secondo input sia un secondo operando o l'offset esteso con <font color="teal">**segnale di selezione ALUSrc**</font>
- un [[MUX]] (mux C) all'ingresso della ingresso del register file per scegliere se il risultato da scrivere nel registro destinazione è l'uscita dell'ALU o il dato letto dalla memoria dati (in caso di load) con <font color=teal>**segnale di selezione MemToReg**</font>
![[Pasted image 20221025162636.png|600]]

Inoltre per l'[[istruzioni#Esecuzioni#Tipo B|esecuzione di istruzioni di tipo B]] ossia salto condizionato, dobbiamo aggiungere un MUX (mux B) per decidere il valore da scrivere nel program counter:
- PC + 4
- PC + offset_ext