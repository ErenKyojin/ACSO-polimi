# assembler
Linguaggio simbolico che utilizza un assemblatore per convertire il codice assembly in linguaggio macchina (ossia [[codice binario]]). È basato su codici mnemonici che corrispondono a codici binari, inoltre sostituisce ogni riferimento simbolico degli indirizzi con la forma binaria.

Per capire i comandi [[assembler]] è utile capire come funziona la [[macchina di von neumann]], inoltre è importante capire che l'assembler e i suoi comandi dipendono dall'[[architettura]].


## Assemblaggio
L'assemblaggio si occupa di espandere le [[pseudo istruzioni]]

### passo 1 - tabella dei simboli:
Compiliamo la tabella dei simboli:

Simbolo | Indirizzo | Tipo di segmento
 --- | --- | ---
 Label_VAR | indirizzo rilocabile | dati (D)
 Label_IND  | indirizzo rilocabile | testo (T)


>[!multi-column]
>
>>[!assembly] pre-assemblaggio
>>.
>>.
>>.
>>```armasm
>>	.eqv const, 0x12345678
>>	.data
>>Y:  .dword 0
>>     .text
>>B:  bne a2, zero, E
>>	la  t0, y
>>	sd  a1, 0(t0)
>>E:  li  t1, const
>>```
>
>>[!assembly] post-assemblaggio
>>dimensione testo: ?
>>dimensione dati: ?
>>testo:
>>```armasm
>>0    bne a2, zero, 8
>>4    auipc
>>8    addi
>>C    sd
>>10   lui %hi(const)
>>14   addi %lo(const)
>>```
>>
>>Dati:
>>
>>0 | 0
>>---|---
>>Tabella dei simboli:
>>
>>Simbolo | indirizzo | tipo di segmento
>>--- | --- | ---
>>B | 0 | T
>>E | 10 | T
>>Y | 0 | D
>

Sappiamo come risovlere Il load immediate finale in quanto coinvolge solamente la costante, load adress invece è impossibile da risolvere, non sappiamo ancora come saranno gestiti gli indirizzi dal [[Linker]].

>[!error]
>per l'istruzione `bne`, il simbolo viene risolto come 
>$$\frac{l1-PC}{2}$$
>Nell'esempio sopra E viene tradotto come $\frac{10}{2}=8$ (10 è in base esadecimale), questo perchè deve saltare 4 istruzioni, ossia 8 half word.

### passo 2 - tabella di rilocazione:


>[!multi-column]
>
>>[!assembly] pre-assemblaggio
>>.
>>.
>>.
>>```armasm
>>	.eqv const, 0x12345678
>>	.data
>>Y:  .dword 0
>>     .text
>>B:  bne a2, zero, E
>>	la  t0, y
>>	sd  a1, 0(t0)
>>E:  li  t1, const
>>```
>
>>[!assembly] post-assemblaggio
>>dimensione testo: 0x18
>>dimensione dati: 0x08
>>testo:
>>```armasm
>>0    bne a2, zero, 0 0 8
>>4    auipc t0, 0 0 0 0 0
>>8    addi t0, t0, 0 0 0
>>C    sd a1, 0(t0)
>>10   lui 1 2 3 4 5
>>14   addi 6 7 8
>>```
>>
>>Dati:
>>
>>0 | 0
>>---|---
>>Tabella dei simboli:
>>
>>Simbolo | indirizzo | tipo di segmento
>>--- | --- | ---
>>B | 0 | T
>>E | 10 | T
>>Y | 0 | D
>>
>>Y simbolo da rilocare
>>Tabella di rilocazione:
>>
>>|  | 
>> ---| --- | ---
>>4 | auipc | %pcrel_HI (y)
>>8 | addi | %pcrel_LO (y)

Si procede infine con la fase di [[Linker|linking]]
