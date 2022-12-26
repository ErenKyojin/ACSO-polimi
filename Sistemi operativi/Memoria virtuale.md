La [[memoria]] virtuale nasce per separare i concetti di 
- spazio di indirizzamento: ossia numero di parole indirizzabili, che dipende solamente dal numero di bit dell'indirizzo
- dimensione effettiva della memoria fisica: Numero di byte che costituiscono la memoria fisica $\leq$ spazio di indirizzamento
La memoria principale è detta memoria fisica ed i suoi indirizzi sono detti indirizzi fisici. La memoria virtuale ineve la CPU genera un indirizzo virtuale che viene tradotto da una combinazione di elementi hardware e software in un indirizzo fisico. Inoltre è presente un meccanismo che traduce indirizzi virtuali in indirizzi fisici. Questo meccanismo è detto [[memory mapping]], ed il più usato è la rilocazione dinamica tramite paginazione, dove l'unità più piccola è la [[pagina]].

Essenzialmente quindi la memoria virtuale permette di non doversi preoccupare di quali indirizzi assegnare ne al programmatore ne al linker, che possono ipotizzare di partire dall'indirizzo zero e avere tutta la memoria virtuale a disposizione. Sarà il sistema operativo ad occuparsi di tradurre da  memoria virtuale a memoria fisica




![[Pasted image 20221129084453.png|500]]


## Paginazione

0 0 0 0 1 1 1 | 1 0 0 0 1 0 0 0 0
--- | ---
numero pagina virtuale (NPV) | spiazzamento nella pagina

In questo esempio abbiamo 64 kB / 512 Byte = $2^7$ = 128 virtuali e quindi 7 bit per il VPN e 9 per l'offset.

è analogo l'indirizzo per pagine fisiche (NPF)


### [[Tabella delle pagine]]


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


## Gestione delle [[pagina#Pagine non reisdenti in memoria|pagine virtuali non residenti]] in memoria

Come già detto il numero di pagine virtuali può eccedere la dimensione della memoria fisica, in questo caso cosa succede alle pagine escluse? Vengono salvate su disco
![[pagine non residenti.canvas]]

La scelta di quali salvare su disco (più lento in accesso) è invece più complessa e ci sono varie possibilità, vengono comunque salvate in un'area di memoria detta swap file e gli viene impostato il bit di validità a 0 (così da generare un interrupt di **[[page fault]]**)


## On demand
Il metodo di paginazione su richiesta (oppure **on demand paging**) carica le pagine in memoria fisica solo quando necessario.

Nel caso di esecuzione di un nuovo processo:
- La tabella delle pagine del processo ha tutti i valid bit a 0, quindi nessuna pagina si trova in memoria, ed anche il TLB ha tutti i valid bit a 0
- Quando la CPU prova ad accedere alla prima istruzione si verifica un **page fault** e la prima pagina di codice viene portata in memoria e registrata nella tabella delle pagine e nel TLB
- Ogni volta che si identifica un indirizzo in un pagina non ancora in memoria si verifica un **page fault**



## Working set di ordine $k$
Basato sulla località degli accessi, consiste nell'insieme delle pagine refernziate durante gli ultimi $k$ accessi in memoria, se $k$ è abbastanza grande, per il principio di località il set di un programma varia molto lentamente.
Quindi mantenendo in memoria le pagine a cui abbiamo avuto accesso più di recente diminuiamo, per il principio di località, le possibilità di un page fault.

Il numero di pagine $R$ residenti in memoria di ogni processo viene ottenuto da una stima del working set in configurazione con l'obiettivo di bilanciare page fault e numero di processi attivi:
 - R grande $\implies$ pochi page fault, pochi processi
 - R piccolo $\implies$ più page fault, più processi
A partire dall'inizio di esecuzione di un programma si carica il working set dopo R page fault


## Politica di sostituzione delle pagine

### - Casuale
...

### - LRU (least recently used)
Sostituiamo la pagine meno utile nel prossimo futuro, ossia quella usata meno di recente (principio di località)

>[!oss]
Può essere poco efficiente in caso di working set R leggermente maggiore delle pagine salvate in memoria

### FIFO (first in first out)
Si sostituisce sempre la pagine caricata meno di recente

------
Per mantenere queste politiche è necessario avere
- Bit di accesso: posto a 1 quando si accede ad una pagina e resettato a 0 in modo periodico dal sistema operativo
- Bit di modifica: posto a 1 quando una pagina subisce un accesso in scrittura (questo indica quali pagine vanno salvate su disco in caso di deallocazione da memoria a disco)

## Dimensionamento delle pagine (frammentazione)

Ad ogni programma viene sempre assegnato un numero intero di pagine, rimangono aree di memoria assegnate ma non occupate,

>[!esempio]
>un programma ha bisogno di 6.34 pagine, gliene vengono assegnate 7, sprechiamo 2/3 di una pagina.
>

Si può ovviare in parte a questo problema scegliendo pagine più piccole, tuttavia più diminuisce la dimensione delle pagine, più dovranno essere grandi e complessi i sistemi di controllo della memoria (ossia il TLB e la tabella delle pagine), inoltre il tempo di ricerca di una pagina su disco è di due ordini di grandezza maggiore al tempo di trasferimento, quindi non conviene ridurre le dimensioni delle pagine


# [[aree di memoria virtuale]]
La memoria virtuale di un processo non viene considerato un'unico spazio di indirizzamento lineare ad uso differenziato, viene diviso in **aree di memoria virtuale (VMA)** che permettono di distinguere i diritti d'accesso delle aree, permettono che solo alcune aree crescano in modo dinamico e gestiscono un area condivisa

| 0000 0000 0000 0000       | C            |
| ------------------------- | ------------ |
| 0000 0000 0040 0000       | K            |
| 0000 0000 0060 0000       | S            |
| Aree virtuali di processo | BSS          |
| ...                       | D            |
| ...                       | $\downarrow$ |
| ...                       | M            |
| ...                       |              |
| 0000 7FFF F77F FFFF       | T            |
|                           |              |
| 0000 7FFF FFFF FFFF       | P            |


Ogni area è definita con una struct




## Meccanismo generale
Esistono due criteri per classificare le VMA:
- Mappate su file o anonime
- Private o condivise

Anche se il caso anonime e condivise non esiste, abbiamo quind tre casi effettivi:
- MAP_SHARED
- MAP_PRIVATE
- MAP_ANONIMOUS



#### Aree mappate su file - sola lettura
Un file linux è una sequenza di byte, un file diviso in pagine è un modo di indirizzare le posizioni del byte all'interno della pagina

---



# [[mappa di memoria]]

# [[NPV]]

# [[translation lookaside buffer]]

_________


>[!esempio] Read("Pk0", "Ps0, "Pd0", "Pd1", Write("Pp1", "Pp2", "pp3")
>Processo: P
>VMA:
>
> | | | | | | | |
| --- | ---       | --- | --- | --- | --- | ---    |
| --- | --------- | --- | --- | --- | --- | ------ |
| C   | 000000400 | 2   | R   | P   | M   | <X,0>  |
| K   | 000000600 | 1   | R   | P   | M   | <X,2>  |
| S   | 000000601 | 1   | W   | P   | M   | <X,3>  |
| D   | 000000602 | 2   | W   | P   | A   | <-1,0> |
| P   | 7FFFFFFFC | 3   | W   | P  | A   | <-1,0>       |
>
>PT:
>
|     |     |
| --- | --- |
| c0  |     |
| c1  | 1 R |
| k0  |     |
| s0  |     |
| d0  |     |
| d1  |     |
| p0  | 2 W |
| p1  |     |
| p2  |     |
>
>NPV di PC e SP: c1 e p0
>
>-------
>Memoria fisica (9 pagine libere):
>
|     |       |     |     |              |
| --- | ----- | --- | --- | ------------ |
| 00  | \<ZP> | -   | 01  | Pc1 / \<X,1> |
| 02  | Pp0   | -   | 03  |              |
| 04  |       | -   | 05  |              |
| 06  |       | -   | 07  |              |
| 08  |       | -   | 09  |              |
| 10  |       | -   | 11  |              |
>
> -----
> Stato del TLB:
> 
 |     |        |     |     |     |        |     |  
 | --- | ------ | --- | --- | --- | ------ | --- | 
 | Pc1 | 01 - 0 | 1   | -   | Pp0 | 02 - 1 | 1   |   
 |     |        |     |     |     |        |     |  
 