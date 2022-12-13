Sistema operativo open surse adatto a PC, server, sistemi embedded/real time ed android.

Utilizza un meccanismo time sharing, assegnando ad ogni [[processo]] un quanto di tempo da "spendere" in esecuzione sul processore per poi attivare la [[preemption]] (alternativamente sospensione volontaria) fino ad un'eventuale interruzione del processo.
Il [[kernel]] è l'unica eccezione a questa regola (non preemptable).


è in grado di fare gestione delle risorse:
- Gestione del processore -> **[[kernel]]**
- Gestione della memoria centrale -> **[[gestore della memoria]]**
- Gestione delle periferiche -> **[[gestore del device driver]]**
- Gestione della memoria di massa -> **[[gestore del file system]]**


basato su architettura [[x64]]

# [[Commutazione di pila]]
