Esiste una tabella delle pagine per ogni processo in esecuzione e contiene una riga per ogni pagina virtuale del processo, in queste tabeille il numero di pagina virtuale (NPV) si può utilizzare come indirizzo nella tabella delle pagine del processo, alternativamente la tabella può essere associativa sul contenuto di NPV (o sulla coppia (PID, NPV)) associato al corrispondente NPV 

In [[x64]] esiste il registro CR3 che contiene l'indirizzo del punto di partenza della tabella delle pagine in memoria.

>[!multi-column]
>
>>[!memoria virtuale]
>>
>> ## P
>>numero di pagina | contenuto delle pagine
>>--- | ---
>>0x00000 | AAAA
>>0x00001 | BBBB
>>0x00002 | CCCC
>>0x00003 | DDDD 
>>
>> ## Q
>> numero di pagina | contenuto delle pagine
>> --- | ---
>> 0x00000 | RRRR
>> 0x00001 | SSSS
>> 0x00002 | TTTT
>> 0x00003 | UUUU
>> 0x00004 | VVVV
>
>>[!tabellle Pagine]
>>
>>## P
>>NPV </br> -------------| NPF </br> -------------
>>--- | ---
>>0x00000 | 0x00004
>>0x00001 | 0x00005
>>0x00002 | 0x00006
>>0x00003 | 0x00007
>>
>> ## Q
>> NPV </br> ------------ | NPV </br> ------------
>> ---|----
>> 0x00000 | 0x00008
>> 0x00001 | 0x00009
>> 0x00002 | 0x0000A
>> 0x00003 | 0x0000B
>> 0x00004 | 0x0000C
>
>>[!memoria fisica]
>>numero di pagina | contenuto delle pagine
>>--- | ---
>>0x00000 | SO
>>0x00001 | SO
>>0x00002 | SO
>>0x00003 | SO
>>0x00004 | AAAA
>>0x00005 | BBBB
>>0x00006 | CCCC
>>0x00007 | DDDD
>>0x00008 | RRRR
>>0x00009 | SSSS
>>0x0000A | TTTT
>>0x0000B | UUUU
>>0x0000C | VVVV
>>0x0000D | N/D
>>0x0000E | N/D
>>0x0000F | N/D
>>.... | ....
>

Le tabelle sono allocate in memoria alla creazione del processo



# Implementazione in [[x64]]

Essendo lo [[Spazio virtuale]] così grande dividiamo i 48 bit di indirizzo in 12 bit di offset e 36 bit di NPV a loro volta divisi in 4 gruppi da 9 bit.

| PGD | PUD | PMD | PT  | Offset |
| --- | --- | --- | --- | ------ |
|     |     |     |     |        |

- **Offset** ci indirizza all'interno della pagina
- **PT, page table** Indirizza una pagina specifica
- **PUD**, Page upper directory
- **PGD**, Page global directory
- **Registro CR3** indica la base della page global directory

>![[Page walk.canvas|page walk]]

Quindi il processore che genera un indirizzo virtuale deve attraversare tutta la gerarchia per arrivare all'indirizzo della pagina fisica, quindi servono **5 accessi** in memoria fisica (includendo quello per l'offset), per velocizzare il processo si usa il [[translation lookaside buffer|TLB]]



>[!esempio] ### Decomposizione di un indirizzo virtuale
>
><p style = "text-align:center">0x0000 <font COLOR = gree>7FFF B0D4 2<font COLOR = red>118 </font></font></p>
>
>- **OFFSET**: <font COLOR = red>0x118</font>, binario 0001 0001 1000 = 280
>- **NPV**: <font COLOR = gree> 0x7FFF B0D4 2 </font>
> - Indice **PT** i 9 bit meno significativi, quindi 1 0100 0010 = 322
> - Indipce **PMD** i 9 bit successivi. Quindi 11 0000 110 = 390
> - Indice **PUD** i 9 bit successivi. Quindi 111 1111 10 = 510
> - indice **PGD** 0111 1111 1 = 255
> 
> Con la notazione PGD : PUD : PMD : PT l'indirizzo è -> 255 : 510 : 390 : 322


Possiamo così tradurre indirizzi iniziali:

- Indirizzo iniziale **codice** -> 0:0:2:0
- Indirizzo iniziale **dati** -> 0:0:3:0
- Indirizzo iniziale della **pila del primo thread T0** -> 0000 7FFF F77F F000
- Indirizzo iniziale della **pila del processo** -> 0000 7FFF FFFF E000