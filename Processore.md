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
- PC + offset_ext, indirizzo di destinazione del salto o BTA(branch target address)

Il segnale per controllare questo mux <font color=> lo otteniamo facendo un [[AND]] l'uscita zero dell'ALU e il Branch

![[Pasted image 20221025171849.png|650]]

Ora, come controlliamo l'ALU? la risposta è l'[[unità di controllo]]



>[!oss] ## Tempo di esecuzione delle istruzioni
>![[Pasted image 20221025175406.png]]
>Se eseguiamo una istruzione per ciclo di clock, allora il ciclo di clock non può durare meno della più lunga istruzione da eseguire, detta percorso critico, ossia 800 ps in [[RISC-V]]
>

Nel caso di implementazione a monociclo eseguiamo una istruzione singola per ciclo di clock, che va iniziata e completata entro la fine di questo ciclo, tuttavia non è una strategia efficace dal punto di vista delle risorse, ci basti pensare che così facendo, considerando un ciclo di clock di durata $T=800\ ps$ avremo una frequenza $f =\frac{1}{T} = 1,250\ Ghz$. Ma, basta una veloce riflessione sui processori di mercato, per sapere che è almeno un terzo della performance media. Inoltre non sfruttiamo il fatto che alcune istruzioni possono richiedere quasi metà del tempo del percorso critico.
Come soluzione a questo problema introduciamo il [[pipelining]] 
