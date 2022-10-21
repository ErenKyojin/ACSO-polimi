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


## Formato R
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



## Formato I
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




## Formato S
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


## [[ISTRUZIONI DI FLUSSO]]

>[!tldr]-
| FORMATO | ISTRUZIONE                                                         |
| ------- | ------------------------------------------------------------------ |
| B o SB  | beq, bne, bge, blt                                                 |
| U       | lui, auipc                                                         |
| J o UJ  | jal                                                                   |

Istruzioni che ci permettono di "saltare" attraverso il codice.


## Formato B
| imm(12)(10:5) | rs2   | rs1   | funct3 | imm (4:1)(11) | OPCODE |
| ------------- | ----- | ----- | ------ | ------------- | ------ |
| 7 bit         | 5 bit | 5 bit | 3 bit  | 5 bit         | 7 bit  | 

 **imm = offset:** distanza di salto, in positivo o in negativo, rispetto al [[program counter]], in termini di half word, quindi va aggiunto uno 0 nel bit meno significativo per ottenere la distanza in byte.

>[!oss]
>Non è incluso il bit 0, che è dato per scontato essere 0, in quanto il valore del bit meno significativo indirizza i byte (essendo l'indirizzamento della memoria a byte)



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


## Formato J
Formato per Imm da 20 bit:

| imm[20] | imm[10:1] | imm[11] | imm[10:12] | rd    | OPCODE |
| ------- | --------- | ------- | ---------- | ----- | ------ |
| 1 bit   | 10 bit    | 1 bit   | 8 bit      | 5 bit | 7 bit  | 

JALR invece:

imm[12] | rs1 | funct3 | rd | OPCODE
---| --- | --- | --- | ---
12 bit | 5 bit | 3 bit | 5 bit | 7 bit


## Costanti su 32 bit

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


>[!LUI]
> load upper immediate, carica il primo immediato da 20 bit nei 20 bit più significativo della metà inferiore di un registro da 64, un tipo di istruzione U

## formato U

imm[31:12] | rd | OPCDOE
--- | --- | ---
20 bit | 5 bit | 7 bit

>[!esempio]
>```armasm
>lui rd cost20             ;rd = cost20
>auipc rd off20            ;rd = pc + off20
>```

Registro della lui:

63:32 | 31:12 | 11:0
--- | --- | ---
ext segno | imm 20 bit + imm 12 bit | x00000

Registro dopo LUI:
0111 1110 0001 1110 0000 | 000 0000 0000


0111 1110 0001 1110 0000 | 0000 0000 0000 +
1111 1111 1111 1111 1111 | 1000 0111 0111 =

0111 1110 0001 1101 1111 | 1000 0111 0111


# Esecuzione delle istruzioni e struttura base del processore [[RISC-V]]

## Fasi generiche

### Fase 1
Inviare il contenuto del [[program counter]] ad una memoria che contiene le istruzioni [[memoria istruzioni]] per prelevare l'istruzione e preparare l'indirizzo dell'istruzione successiva (PC + 4)

![[Pasted image 20221020174837.png]]

Add incrementa il program counter. 
È la fase di lettura dell'istruzione da 32 bit dalla memoria istruzioni.


### Fase 2
Leggere uno o due registri dal [[Register file]] decodificando i campi dell'istruzione per selezionare indirizzi e registri a quale accedere.


Le fasi successive dipendono dalla singola istruzione:

### Fase 3
Esecuzione dell'istruzione utilizzando l'ALU per:
- Per eseguire l'istruzione aritmetico logica
- Per il calcolo dell'indirizzo di memoria dati per istruzione di load o store
- Per il confronto tra due registri nelle istruzioni di salto condizionato


### Fase 4 (esclusiva della Load)
Lettura del dato dalla memoria dati, solo nel caso di istruzione di load

### Fase 5
Scrittura del risultato nel registro destinazione del register file oppure nella memoria dati o modifica del program counter in base all'esito del salto condizionato


![[Pasted image 20221020181634.png]]






## Esecuzioni
Di seguito le esecuzioni di ogni tipo:
### Tipo R

Op rd, rs1, rs2

Prelievo istruzioni, incremento PC | Lettura rs1, rs2 | OP ALU sui dati | scrittura nel registro destinazione rd
--- | --- | --- | ---

Esecuzione dell'istruzione in 4 passi:
1. Prelievo istruzione della memoria istruzione e ingremento del PC
2. Lettura dei 2 registri sorgente rs1 e rs2 dal register file tramite i bit [19-15], [24-20]
3. Operazione dell'[[Unità aritmetico logica]] con operandi letti dal register file utilzzando i campi funct3 e funct7 per decodificare la funzione
4. Scrittura del risultato nel banco dei registri utilizzando i bit [11-7] dell'istruzione per selezionare il registro destinazione



### Tipo I
ld rd, offset12(rs1)

prelievo istruzioni, incremento PC | Lettura rs1 | OP ALU (rs1 + off) | Prelievo dati M(rs1+off) | Scrittura in rd
--- | --- | --- | - | --- 

1. Prelievo di istruzione dalla memoria istruzioni e incremento PC
2. Lettura del registro base rs1 dal banco dei registri indirizzato dai bit [19-15]
3. Operazione dell'alu per calcolare la somma del valore letto dal registro base e dell'offset esteso in segno da 12 a 64 bit
4. Prelievo del dato nella memoria dati utilizzando come indirizzo di lettura il risultato dell'ALU
5. Scrittura del dato proveniente dalla memoria nel registro destinazione rd indirizzato dai bit [11-7] 

>[!oss] 
>Esecuzione più lunga

>[!Esecuzione delle istruzioni di load:]
>
Si usa il register file per accedere al registro base e per scrivere nel registro destinazione, usiamo il modulo estensione segno per generare l'offset su 64 bit estendendo quello a 32.
A questo punto l'ALU a 64 bit calcola l'indirizzo di memoria sommando il valore del registro base all'offset esteso in segno.
Memoria dati da cui legge con segnali di controllo memRead.

### Tipo S

sd rs2, offset12(rs1)

prelievo istruzioni, incremento PC | lettura registri rs1 e rs2 | OP ALU (rs1 + off) | scrittura dato M(rs1 + off) 
--- | --- | --- |--- 

1. Prelievo istruzione dalla memoria istruzioni e incremento PC
2. Lettura del registro base (rs1) dai bit [19-15] e del registro sorgente rs2 dai bit [24-20] dal banco dei registri
3. Operazione dell'ALU per calcolare la somma del valore letto dal registro base e dell'offset esteso in segno da 12 bit a 64 bit
4. Scrittura del dato proveniente dal registro sorgente rs2 nella memoria dati utilizzando come indirizzo di scrittura il risultato dell'ALU

>[!Esecuzione delle istruzioni di store:]
>
Si usa il register file per accedere al registro base e al registro sorgente, usiamo il modulo estensione segno per generare l'offset su 64 bit estendendo quello a 32.
A questo punto l'ALU a 64 bit calcola l'indirizzo di memoria sommando il valore del registro base all'offset esteso in segno.
Memoria dati da cui scrive con memWrite


### Tipo B
beq rs1, rs2, offset12

Prelievo istruzione, incremento PC | Lettura registri rs1, rs2 | OP ALU (rs1- rs2), (PC + off) | Scrittura nel PC
--- | --- | --- | ---

1. prelievo istruzione dalla memoria istruzioni e incremento del program counter
2. Lettura dei registri sorgenti rs1 ed rs2 dal register file usando [19-15] e [24-20]
3. Operazione dell'ALU per effettuare la sottrazione tra i valori letti dal register file. Il valore del PC iniziale viene sommato all'offset su 64 bit (estensione a segno dell'offset a 12 bit). L'offset ext deve essere shiftato a sinistra di una posizione per riportarlo al byte essendo espresso in half word.
   Rappresenta l'indirizzo didestinazione del salto
4. L'uscita zero dell'ALU è usata per decidere il valore da scrivere nel PC: PC + 4 o PC + offset_ext