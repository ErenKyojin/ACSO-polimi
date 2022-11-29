La [[memoria]] virtuale nasce per separare i concetti di 
- spazio di indirizzamento: ossia numero di parole indirizzabili, che dipende solamente dal numero di bit dell'indirizzo
- dimensione effettiva della memoria fisica: Numero di byte che costituiscono la memoria fisica $\leq$ spazio di indirizzamento
La memoria principale è detta memoria fisica ed i suoi indirizzi sono detti indirizzi fisici. La memoria virtuale ineve la CPU genera un indirizzo virtuale che viene tradotto da una combinazione di elementi hardware e software in un indirizzo fisico. Inoltre è presente un meccanismo che traduce indirizzi virtuali in indirizzi fisici. Questo meccanismo è detto [[memory mapping]], ed il più usato è la rilocazione dinamica tramite paginazione, dove l'unità più piccola è la [[pagina]].




![[Pasted image 20221129084453.png|500]]


## Paginazione

0 0 0 0 1 1 1 | 1 0 0 0 1 0 0 0 0
--- | ---
numero pagina virtuale (NPV) | spiazzamento nella pagina

In questo esempio abbiamo 64 kB / 512 Byte = $2^7$ = 128 pagine virtuali e quindi 7 bit per il VPN e 9 per l'offset


### Tabella delle pagine
Esiste una tabella delle pagine per ogni processo in esecuzione e contiene una riga per ogni pagina virtuale del processo, in queste tabeille il numero di pagina virtuale (NPV) si può utilizzare come indirizzo nella tabella delle pagine del processo, alternativamente la tabella può essere associativa sul contenuto di NPV (o sulla coppia (PID, NPV)) associato al corrispondente NPV 


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
>> NPV </br> - | NPV </br> -
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


# Memory managment unit
La tabella delle pagine è una struttura dati del [[sistema operativo]] residente in memoria che può assumere grandi dimensioni, inoltre ogni accesso a memoria è in realtà eseguito tramite due accessi:
1. Accesso alla tabella della pagine per tradurre l'indirizzo virtuale in indirizzo fisico
2. Accesso all'indirizzo fisico del dato

Per ottimizzare il processo sfruttiamo, per mantenere in memoria le tabelle NPV to NPF, una cache (**[[translation lookaside buffer]]** o TLB)  in un meccanismo hardware detto **memory managment unit** o MMU.