# Struttura base del processore

![[Pasted image 20221025150659.png]] 

Memoria istruzioni separata dalla [[memoria]] dati e [[Register file]] con banchi da 32 registri a 64 bit. Due porte di lettura ed una in scrittura.

Alcune istruzioni ([[istruzioni]] di formato I, S, B) hanno necessità di estendere l'immediato a 64 bit, questo viene fatto dal modulo di estensione segno, che inoltre shifta a sinistra il formato B, il modulo prende per ingresso tutta l'istruzione in quanto ha bisogno di sapere quale istruzione si sta eseguendo (vengono ricostruite in modo diverso)

Aggiungiamo poi un MUX al secondo ingresso dell'alu per scegliere se il secondo input sia un secondo operando o l'offset esteso ed un mux all'ingresso della ingresso del register file con segnale di selezione MemToReg