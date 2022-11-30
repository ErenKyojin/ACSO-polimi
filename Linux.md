Sistema operativo open surse adatto a PC, server, sistemi embedded/real time ed android.

Utilizza un meccanismo time sharing, assegnando ad ogni [[processo]] un quanto di tempo da "spendere" in esecuzione sul processore per poi attivare la [[preemption]] (alternativamente sospensione volontaria) fino ad un'eventuale interruzione del processo.
Il [[kernel]] è l'unica eccezione a questa regola (non preemptable).


è in grado di fare gestione delle risorse:
- Gestione del processore -> **[[kernel]]**
- Gestione della memoria centrale -> **[[gestore della memoria]]**
- Gestione delle periferiche -> **[[gestore del device driver]]**
- Gestione della memoria di massa -> **[[gestore del file system]]**


basato su architettura [[x64]]

# Commutazione di pila
Affinchè il sistema operativo funzioni la pila usata durante il funzionamento del modo S deve essere diversa da quella usata durante il funzionamento del modo U


## sPila e uPila
Rispettivamente pila del modo S e del modo U, e lo stack pointer deve essere cambiato adeguatamente al modo attivo

---

Nel cambio da modo U a modo S dobbiamo commutare la pila **prima** del salvataggio di informazioni:
- L'indirizzo di ritorno a modo U deve essere salvato su sPila
- Nel ritorno da S ad U l'indirizzo di ritorno sarà prelevato da sPila (prima di commutare ad uPila)

User stack pointer e System stack pointer due strutture dati ad accesso hardware nella memoria S:
- SP al momento del passaggio U -> S deve essere salvato in USP (SP -> USP)
- SSP contiene il valore del puntatore alla sPila da caricare in SP al momento del passaggio dal modulo S



## Commutazione di pila con [[SYSCALL]] e [[SYSRET]]
SYSCALL:
- Salva SP corrente in USP
- Salva SSP in SP
- Salva RA in sPila
- Salva PSR del chiamante (in modo U) su sPila
- Carica in PC e PSR i valori del [[vettore di syscall]]


SYSRET:
- Carica in PSR il PSR(u) presente in sPila (torna ad essere modo U)
- Carica in PC il valore dell'RA su sPila
- Carica in SP il valore presente in USP (sp punta ad uPila)


# [[Interrupt]] ed [[IRET]]

## CASO 1
L'interrupt interrompe un processo U
```mermaid
graph LR
	A((U)) -->|interrupt| B((S))
	B --->|iret| A
```

L'interrupt:
- Salva SP in USP (ora USP punta ad uPila)
- Salva SSP in SP (ora SP punta a sPila)
- Salva su sPila il return address del programma interrotto
- Salva su sPila il PSR del programma interrotto (modo U)
- Carica in PC e PSR i valori del [[vettore di interrupt]] (il modo di funzionamento passa ad S)

L'IRET:
- carica in PSR il valore di PSR presente in sPila
- carica in PC il valore dell'indirizzo di ritorno al programma interrotto presente in sPila
- Carica in SP il valore presente in USP (SP punta nuovamente ad uPila)


## CASO 2
L'interrupt interrompe il [[sistema operativo]]
```mermaid
graph LR
	A((U)) --->|SYSCALL| B((S)) --->|interrupt| C((S))
	C --->|IRET| B --->|SYSRET| A
```

Interrupt:
- Salva su sPila l'indirizzo di tirò o al codice di sistema interrotto
- Salva su sPila il valore del PSR del codice di sistema interrotto (modo S)
- PC e PSR caricati dal [[vettore di interrupt]]

IRET:
-  Carica in PSR il valore del PSR presente in sPila
- Carica in PC il valore dell'indirizzo di ritorno al codice di sistema interrotto presente in sPila

>[!important]
Le ipotesi fatte fino ad ora falliscono considerando la [[processo#sPila dei processi]]



