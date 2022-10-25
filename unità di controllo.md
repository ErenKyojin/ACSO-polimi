Genera comandi relativi all'operazione da svolgere in funzione dell'OP code all'ingresso dell'ALU in base ai seguenti bit:

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
--- | --- | 