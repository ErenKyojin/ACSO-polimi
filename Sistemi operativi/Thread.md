Detti [[processo|processi]] leggeri, permettono l'esecuzione concorrente pur essendo meno pesanti sulla [[memoria]] rispetto ai processi.

Un thread è comunque interno ad un processo, può essere svolto in parallelo con altri thread nello stesso processo, i thread sfruttano solo il [[segmenti|segmento]] di stack, mentre codice e dati saranno condivisi con altri thread e processi.

Se vogliamo sincronizzare i due thread usiamo i [[semafori]]

## thread e [[aree di memoria virtuale|VMA]]
I thread condividono la stessa struttura di aree virtuali e tabella delle pagine del processo padre, c'è quindi una condivisione assoluta della memoria tra il processo padre i propri thread, ogni modifica di memoria eseguita da un thread ricardà su tutti gli altri, per ogni thread viene allocata una pila di 2048 pagine (8 MB) seguita da una pagina di inteposizione in sola lettura.
La pila del primo thread inizia al NPV 7FFF F77F F e si sviluppa verso indirizzi piú bassi. La sua VMA è compresa tra
- 7FFF F6FF F (6FFF ] 800 = 77FF)
- 7FFF F77F F

La pila del secondo thread inizia logicamente al NPV 7FFF F6FF E e si sviluppa verso indiirizzi piú bassi