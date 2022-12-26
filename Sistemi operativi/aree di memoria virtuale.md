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
Una VMA si puó mappare su un file detto "backing store", definito in vm_area_struct da

- `Struct file * vm_file`: individua il file utilizzato come **baking store**
- `unsigned long vm_pgoff`: page offset all'interno del file

Nelle aree C, K ed S viene associato il file .exe come backing store con offset il punto dell'eseguibile in cui inizia il corrispondente segmento codice o dati


---

>[!esempio] Mappa di memoria di un processo in esecuzione (cat /proc/NN)
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
>- L'area di pila é stata allocata con dimensione iniziale di 34 pagine
>

---