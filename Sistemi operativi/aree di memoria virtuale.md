---
alias: VMA
---
Le aree di memoria virtuale (o VMA) sono diverse aree in qui salvare diversi dati di un processo.


è un sistema che porta diversi vantaggi rispetto a salvare tutti i dati nella stessa area indiscriminatamente, ad esempio è possibile:

- Gestire diversi [[pagina#Diritti d'acesso|diritti d'accesso]] delle aree:
	- **READ_ONLY**
	- **READ_WRITE**
	- **EXECUTE**

- Consentire crescita diverse e indipendente di aree (ad esempio pila ed heap)
- Gestire un'area di memoria condivisa tra processi



Ogni VMA è delimitata da un NPV iniziale ed un NPV finale ed è composta da un numero intero di pagine virtuali consecutive con caratteristihe di accesso alla memoria omogenee.



# Aree virtuali di un processo

- Codice (**C**): area che contiene le istruzioni e le costanti definite nel codice
- Costanti per la rilocazione dinamica (**K**): area che contiene parametri determinate dal [[Linker]] per il collegamento con librerie
- Dati statici (**S**): Area destinata per dati inizializzati allocati durante tutta l'esecuzione del programma
- Dati dinamici (**D**): Dati allocati dinamicamente su richiesta (malloc)
- Aree per memory mapped files (**M**): Aree che permottono di mappare file o librerie su una porzione di memoria virtuale
- Librerie dinamiche e pila





## Crescita delle aree dati dinamiche
Mentre la **stack** cresce automaticamente quando necessario, l'heap cresce tramite inocazione esplicita di alcuni [[kernel#Servizi di sistema|servizi di sistema]], per incrementare l'heap su linux si utilizza la funzione
```c
*void sbrk (int incremento)
```

che incrementa l'heap di un valore `incremento` e ritorna l'indirizzo iniziale della nuova area, se `incremento` vale 0 ritorna quindi il valore corrente della cima dell'heap 




# VMA mappate su file
Una VMA si puó mappare su un file detto "[[backing store]]", definito in vm_area_struct da

- `Struct file * vm_file`: individua il file utilizzato come **backing store**
- `unsigned long vm_pgoff`: page offset all'interno del file

Nelle aree C, K ed S viene associato il file .exe come backing store con offset il punto dell'eseguibile in cui inizia il corrispondente segmento codice o dati


---

>[!esempio] Mappa di memoria di un processo in esecuzione (cat /proc/NN/maps)
>
>| start-end page            | perm  | offset | device | i-node | file-name        |
>| ------------------------- | ----- | ------ | ------ | ------ | ---------------- |
>| 00400 - 00401             | r-xp  | 000000 | 08:01  | 394275 | .../user.exe     |
>| 00600 - 00601             | r- -p | 000000 | 08:01  | 394275 | .../user.exe     |
>| 00601 - 00602             | rw -p | 001000 | 08:01  | 394275 | .../user.exe     |
>| 7fff f7a1 c - 7fff f7bd 0 | r-xp  | 000000 | 08:01  | 271666 | .../libc-2.15.so |
>| 7fff f7bd 0 - 7fff f7dc f | ---p  | 1b4000 | 08:01  | 271666 | .../libc-2.15.so |
>| 7fff f7dc f - 7fff f7dd 3 | r- -p | 1b3000 | 08:01  | 271666 | .../libc-2.15.so |
>| 7fff f7dd 3 - 7fff f7dd 5 | rw-p  | 1b7000 | 08:01  | 271666 | .../libc-2.15.so |
>| ...                       |       |        |        |        |                  |
>| aree M                    |       |        |        |        |                  |
>| ...                       |       |        |        |        |                  |
>| 7fff fffd d - 7fff ffff e | rw-p  |        |        |        | [stack]                 |
>
>linux costruisce la struttura delle aree virtuali del processo in base alla struttura definita dall'eseguibile, possiamo vedere che
>- L'area di pila é stata allocata con dimensione iniziale di 34 pagine, é anonima, quindi non ha un file associato
>- I file coinvolti sono sullo stesso dispositivo (08:01) l'eseguibile del programma e della libc sono diversi ed hanno quindi [[i-node]] differenti
>- L'area D è assente, viene creata in presenza di dati statici non inizializzati nell'eseguibile
>

---
## Classificazione di VMA
- Le VMA possono essere mappate su file o anonime
- Le VMA possono essere shared o private

>[!oss]
>Tutte le combinazioni sono valide ma ANONYMOUS | SHARED
>Quindi consideriamo:
>- VMA **mappate su file**: o **private** o **shared**
>- VMA **anonime**: implicitamente **private**
>
(che si traduco rispettivamente nei tipi)
- **MAP_PRIVATE**
- **MAP_SHARED**
- **MAP_ANONIMOUS**


## Creazione di VMA

>[!def]
>```C
>#include <sys/map.h>
>void *map(void *addr, size_t length, int port, int flags, int fd, off_t offset)
>```
>
>- addr: suggerisce l'indirizzo virtuale iniziale
>- length: dimensione dell'area
>- prot: protezione, PROT_READ, PROT_WRITE, PROT_EXEC
>- flags: con 3 opzioni, MAP_SHARED, MAP_PRIVATE, MAP__ANONIMOUS
>- fd: descrittore del file da mappare
>- offsett; la prima pagine dell'area all'interno del file



>[!esempio]
>Uso mmap per  creazion di VMA v1 di un processo P mappato su file F
>
>```c
>#include <sys/map.h>
>#define PAGESIZE 1024*4
>char * base;
>fd = open("./F, O_RDWR"); //apre il file F
>base = mmap(NULL, PAGESIZE * 3, PROT_READ, MAP_SHARED, fd, PAGESIZE);
>```

Per evitare che un processo rilegga da disco una pagina già caricata si usa la [[page cache]]


## VMA anonime
Le aree di tipo anonimo sono utilizzate dal sistema operativo per **pila** ed **heap**, cioè per l'area dati dinamici dei processi, le aree di tipo anonimo non hanno un file associato e la loro definizione non alloca memoria fisica (sono infatti mappati sulla [[pagina#zero page]])
- La lettura di una pagina trova la zeropage e non richiede l'allocazione di nessuna pagina fisica
- La scrittura di una pagina innesca il meccaniscmo copy on write che richiede l'allocazione di una nuova pagina fisica (come per le VMA private)

## VMA mappate sull'eseguibile (C,K,S)
C, K ed S sono mappate sull'eseguibile e sono tutte VMA PRIVATE
- **C** e **K** non sono scrivibili e rimangono condivise
- Le pagine dei dati statici **S** devibi essere di tipo PRIVATE perchè le scritture non devono modificare ovviamente l'eseguibile e non devono essere osservabili se più processi sfruttano lo stesso programma.
  Saranno duplicate al momento della scrittura tramite copy on write

>[!oss]
>Se due processi eseguono lo stesso programma contemporaneamente le pagine di codice (C) saranno condivise, il secondo processo troverà tali pagine già lette e presenti nella PageCache, ed è addirittura possibile risalire al codice della pagecache


## VMA per memory mapped files (M)
Il linker utilizza le VMA per realizzare la condivisione delle pagine fisiche delle librerie condivise (come glibc) e lo fa utilizzando il tipo MAP_PRIVATE, così:
- Il codice che non viene mai scritto e rimane sempre condiviso
- Le pagine sulle quali un processo scrive sono riallocate al processo tramite il meccanismo di copy on write e non più condivise con gli altri processi e file

## VMA di pila
- VMA anonime
- Dimensionamento iniziale
- un flag GROWSDOWN attivo che significa che la pila cresce automaticamente verso il basso quando viene acceduta la pagina di growsdown, ossia l'ultima pagina disponibile.

Le pagine vengono allocate in base alle richieste d'accesso, quindi con un sistema on demand, la prima pagina non è mai allocata, anche quando viene riempita. Esiste un meccanismo di crescita automatica delle VMA di pila ma non di decrescita (le pagine rimangono allocate quando la pila decresce e veranno semplicemente sostituite tramite sovrascrittura da una futura ricrescita)

## VMA dati dinamici (D)
L'area cresce grazie al servizio `brk()`
- `malloc` deve richiedere al sistema operativo di allocare nuovo spazio tramite l'invocazione del servizio di sistema `brk()` o `sbrk()` che sono funzioni di libreria che invocano lo stesso servizio