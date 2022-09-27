# FORMATO DELLE ISTRUZIONI
Essendo [[RISC-V]] un architettura little endian, le istruzioni vanno lette dal bit meno più significativo al più significativo, ossia da sinistra verso destra

>[!tldr]-
| FORMATO | ISTRUZIONE                                                         |
| ------- | ------------------------------------------------------------------ |
| R       | add, sub, or, and, xor, slt, sll, srl, sra                         |
| I       | addi, ori, andi, xori, slti, slli, srli, srai, ld, lw, lh, lb jalr |
| S       | sd, sw, sh, sb                                                     |
| B o SB  | beq, bne, bge, blt                                                 |
| U       | lui, auipc                                                         |
| J o UJ  | jal, jalr                                                       |


# Formato R
| funct7  | rs2   | rs1   | funct3 | rd    | OPCODE  |
| ------- | ----- | ----- | ------ | ----- | ------- |
| 0000000 | 00000 | 00000 | 000    | 00000 | 0000000 |

Funct7, Funct3 ed OPCODE distinguono il comando.
rd, rs1, rs2 distinguono i [[registro|registri]].

>[!esempio] 
>```asmarm
>add t0, s1, s2
>```
>sommiamo in t0 i valori in s1 ed s2:
>
>| funct 7 | rs2 | rs1 | funct3 | rd  | OPCODE |
>| ------- | --- | --- | ------ | --- | ------ |
>|0000000         | 10010     | 01001    |  000      | 00011    |   0110011     |
>
>
>>[!oss]
>>Possiamo raggrupare i bit a gruppi di 4 per ottenere l'equivalente istruzione hex:
>>
>>|0000| 0001 | 0010 | 0100 | 1000 | 0001 | 1011 | 0011 |
>>| --- | --- | --- | ---| --- | --- | --- | --- |
>>| 0 | 1 | 2 | 4 | 8  | 1 | B | 3  


>[!esempio]
>```armasm
>sub t0, s1, s2
>```
>sottraiamo in t0 i valori in s1 ed s2.
>
>|funct7| rs2| rs1 | funct3 | rd | OPCODE
>| --- | --- | --- | --- | --- | --- |
>0<FONT COLOR = "red">1</FONT>00000| 10010|01001|000|00011|0110011|
>Il bit evidenziato è l'unica differenza tra una sub e l'equivalente add



# Formato I
Ossia i formati che coinvolgono costanti positive a 12 bit, per costanti positive maggiori vedremo in futuro il formato.

| imm          | rs1   | funct3 | rd    | OPCODE  |
| ------------ | ----- | ------ | ----- | ------- |
| 000000000100 | 01001 | 000    | 01001 | 0010011 |
| 12 bit       | 5 bit | 3 bit  | 5 bit | 7 bit   | 

>[!esempio]
>```armasm
>addi s1, s1, 4
>```
>
>Aggiunge 4 a s1, e il risultato in s1.
>
>| 000000000100 | 01001 | 000 | 010001 | 0010011 |
>| ------------ | ----- | --- | ------ | ------- |
>| 4            | s1       | funct3    | s1        | OPCODE         |

>[!esempio]
>```armasm
>ld t0, off, rb
>```
>load in t0 con offset rispetto a rb di off.
>
>32 | s3 | funct3 | t0 | OPCODE
> --- | --- | --- | --- | ---
> 000000100000 | 10011 | 011 | 00101 | 0000011




# Formato S
Formato delle istruzioni store per trasferire informazioni da un registro alla memoria: (sd, sw, sh,sb)
Il formato S, all'apparenza può sembrare particolare:

| imm (bit:11-5)  | rs2  | rs1  | funct3 | imm (bit:4-0)  | OPCODE |
| ---- | ---- | ---- | ------ | ---- | ------ |
| 7bit | 5bit | 5bit | 3bit   | 5bit | 7bit   | 

con:
- **rs1** registro dove depositare
- **rs2** registro che scrive in memoria

>[!warning] Perchè dividere imm?
>Riprendiamo come esempio le istruzioni di tipo R:
>
>| funct7  | rs2   | rs1   | funct3 | rd    | OPCODE  |
>| ------- | ----- | ----- | ------ | ----- | ------- |
>| 7 | 5 | 5 | 3    | 5 | 7 |
>
>Ed I:
>
>| imm          | rs1   | funct3 | rd    | OPCODE  |
>| ------------ | ----- | ------ | ----- | ------- |
>| 12             |      5 |    3    |    5   |      7   |
>
>Notiamo che per ottenere l'imm nel tipo I, abbiamo usato i bit assegnati a funct7 ed rs2 nel tipo R, nel tipo S invece abbiamo fatto una scelta diversa, cioè di "sacrificare" rd, registro che si riferisce solitamente ai risultati, e mantenere i due rs1 ed rs2.
>
>Il motivo di questa scelta non è per niente casuale, in realtà basta riferirsi alla tabella riportata all'inizio per notare come tutti i comandi che utilizzano questo formato sono del tipo store, store che si occupa di estrarre dati dai registri della CPU e mandarli nella [[memoria]].
>
>Quindi scartiamo i bit riferiti ad rd in quanto, per come è costruita e "cablata" la CPU, rd è utile a ricevere dati in ingresso, mentre con una store è la CPU che invia dati alla memoria.
>


# [[ISTRUZIONI DI FLUSSO]]

>[!tldr]-
| FORMATO | ISTRUZIONE                                                         |
| ------- | ------------------------------------------------------------------ |
| B o SB  | beq, bne, bge, blt                                                 |
| U       | lui, auipc                                                         |
| J o UJ  | jal                                                                   |

Istruzioni che ci permettono di "saltare" attraverso il codice.


# Formato B
| imm(12)(10:5) | rs2   | rs1   | funct3 | imm (4:1)(11) | OPCODE |
| ------------- | ----- | ----- | ------ | ------------- | ------ |
| 7 bit         | 5 bit | 5 bit | 3 bit  | 5 bit         | 7 bit  | 

 **imm = offset:** distanza di salto, in positivo o in negativo, rispetto al [[program counter]], in termini di half word, quindi va aggiunto uno 0 nel bit meno significativo per ottenere la distanza in byte.

>[!oss]
>Non è incluso il bit 0, che è dato per scontato essere 0 per il salto



>[!esempio]
>```armasm
>beq s1, s2, 100
>```
>
> <FONT COLOR = "lime">0</FONT> <FONT COLOR = "tomato">000011 </FONT> | 10010 |01001 | 000 |<FONT COLOR="orange">0010</FONT> <FONT COLOR="cyan">0</FONT> |1100011 |
> --- | ---| ---| ---| ---| --- |
> |imm12,10:5| s1|s2|funct3 | imm4:11| OPCODE 
>
>E l'imm viene poi ricomposto come:
><center><FONT COLOR = "lime">0</FONT> <FONT COLOR = "cyan"> 0</FONT> <FONT COLOR = "tomato">000011</FONT> <FONT COLOR = "orange">0010</FONT></center>
>


# Formato J
Formato per Imm da 20 bit:

| imm[20] | imm[10:1] | imm[11] | imm[10:12] | rd    | OPCODE |
| ------- | --------- | ------- | ---------- | ----- | ------ |
| 1 bit   | 10 bit    | 1 bit   | 8 bit      | 5 bit | 7 bit  | 

JALR invece:

imm[12] | rs1 | funct3 | rd | OPCODE
---| --- | --- | --- | ---
12 bit | 5 bit | 3 bit | 5 bit | 7 bit

# formato U


# Costanti su 32 bit

Dividiamo la costante in 20 bit e 12 bit

imm[31:12] | imm[11:0]
--- | ---
HIGH 20 bit | LOW 12 bit


Quindi introduciamo la [[pseudo istruzioni|pseudo istruzione]] `li`

```armasm
li rd, cost32
```
Che viene divisa nelle due isrtruzioni
```armasm
lui rd, %hi(cost32)
addi rd, rd %lo(cost32)
```
