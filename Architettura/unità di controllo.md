Genera comandi relativi all'operazione da svolgere in funzione dell'OP code all'ingresso dell'[[Unità aritmetico logica|ALU]] in base ai seguenti bit:

- 2bit ALUop, codificati dai bit di codice operativo
- i campi funz3 e funz7 estensioni del codice operativo per finalizzare le operazioni dell'ALU nelle istruzioni di tipo R

Se ALUOp = 00 i campi funz8 e funz3 sono indifferenti
Se ALUOp = 10 ([[istruzioni#Formato R]]) serve il bit 30 di funz7 e i bit 12-14 di funz3

Codice operativo | ALUOp | Operazione eseguita dall'istruzione | Funz7 | Funz3 | OP ALU | ingresso controllo ALU 
--- | --- | --- | --- | --- | --- | --- |
ld | 00 | ld 1 doppia parola | X|X |Somma | 0010
sd | 00 | st 1 doppia parola | x | x |  somma | 0010
beq | 01 | salto condizionato | x | x | sottraz | 0110
R | 10 | add | $0^7$ | $000$ | somma | 0010
R | 10 | sub | $01 (0)^5$ | $000$| sottraz | 0110
R | 10 |and | $0^7$ | $111$ | AND | 0000
R | 10 | or | $0^7$ |$110$ | OR | 0001

>[!esempio] Struttura del processore con unità di controllo
>![[Pasted image 20221025173623.png|600]]


## Segnali di controllo

Nome | effetto se non asserito | Effetto se asserito
--- | --- | ---
RegWrite | Nullo | Dato scritto nel [[Register file]], nel registro individuato dal numero del registro in lettura
ALUSrc | Il secondo operando ALU proviene dalla seconda uscita del Register File (RS2) | Il secondo operando dell'ALU è l'estensione dei 12 bit dell'immediato
PCSrc | [[program counter\|PC]] = PC + 4 | PC = PC + off
MemRead | Nullo |  Il dato della [[memoria]] nella posizione puntata dall'indirzzo diventa il dato sostituito con il presente sulla linea "dato scritto" 
MemWrite | Nullo | Il contenuto della memoria nella posizione puntata dall'indirizzo viene sostituito con il dato presente sulla linea dato scritto
MemToReg | Il dato invieato al register file per la scrittura proviene dall'ALU | il dato inviato al register file per la scrittura proviene dalla memoria dati

E per ogni istruzione avremo le seguenti uscite:

Istruzione | ALUSrc | MemToReg | RegWrite | MemRead | MemWrite| Branch | ALUOp1| ALUOp2
--- | --- | --- | --- | --- | --- | --- | ---
R | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0
ld | 1 | 1 | 1 |1 | 0 | 0 | 0 | 0 
sd | 1 | x | 0 | 0 | 1 | 0 | 0 | 0
beq |0 | x | 0 | 0 | 0 | 1 | 0 | 1




