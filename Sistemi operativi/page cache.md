La page cache evita che un processo rilegga da disco una pagina che già è stata caricata in memoria fisica.
Il meccanismo su cui si basa si chiama page cache index, che ricerca una pagina in base al descrittore che contiene la coppia <identificatore file, offset> su cui è mappata ed altre informazioni come il ref_count (uguale al numero di processi che mappano la pagina + 1)

## Creazione

## Accesso
Quando un processo vuole accedere ad una pagina virtuale mappata su un file il sistema svolge le seguenti operazioni:

1. Determina il descrittore (F, 1) con:
	- **F** file nella VMA
	- **1** Page offset, somma dell' offsets della VMA rispetto al file e dell'offerta dell'indirizzo di pagina richiesto rispetto all'indirizzo della VMA 
2. Se la pagina è indicizzata nella page cache $\implies$ la pagina virtuale viene mappata sulla pagina fisica, aggiornando **ref count** del page cache index e la **PT** del processo
3. Se la pagina non è indicizzata alloca una pagina fisica in memoria e vi ci carica la pagina leggendola dal file, aggiorna la page cache index, il ref_count e la PT del processo


## Scrittura 

### in VMA SHARED

I dati vengono scritti sulla pagina fisica condivisa tramite la page cache quindi viene modificata la pagina fisica e marcata dirty, i processi che mappano tale pagina fisica vedono immediatamente le modifiche, la pagina modificata viene riscritta su file


>[!oss]
>La VMA deve essere abilitata in scrittura, quindi
>```c
>base = mmap(mapaddress1, PAGESIZE * 3, PROT_WRITE, MAP_SHARED, fd, PAGESIZE) //PROT_WRITE al posto di PROT_READ
>```


### in VMA PRIVATE
Meccanismo detto copy-on-write (COW) è necessario intercettare le scritture su pagine di VMA PRIVATE
1. Inizialmente bisogna porre la protezione delle pagine come **read (R)**, questo in modo da generare un [[page fault]] per violazione i protezione
2. Il gestore di page fault scoprirà questa situazione che richiederà l'allocazione di una nuova pagina fisica
3. La scrittura in una pagina virtuale di una VMA di tipo PRIVATE allocata in una pagina fisica PFx si basa sul meccanismo COW:
	- PFx viene duplicata, allocando una nuova pagina fisica privata per P
	- La nuova pagina non risulta più mappata su F
	- La nuova pagina non appartiene alla page cache e non risulta più condivisa dagli eventuali processi che le condividevano
	- La scrittura effettuata da P viene applicata solo alla pagina fisica privata PFz
	- La pagina fisica originale PFx ed il file F sono **inalterati**

>[!oss]
>Per creare la VMA del processo P di tipo private bisogna:
>```c
>base = mmap(mapaddress1, PAGESIZE * 3, PROT_WRITE, MAP_PRIVATE, fd, PAGESIZE); //PROT_WRITE, MAP_PRIVATE
>```


