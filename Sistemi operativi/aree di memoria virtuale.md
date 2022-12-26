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
*void sbrk (int incremento)