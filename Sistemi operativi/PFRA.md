Determina quando e quante pagine deallocare ed è invocato in:

- **Invocazione diretta** se un processo richiede **requiredPages** e
	*freePages - requiredPages < minFree*
- Attivazione periodica tramite kswapd ([[kernel swap daemon]]), funzione che viene attivata regolarmente e che invoca PFRA se **freePages < maxFree*


E dealloca toFree = maxFree - ...


# Quali pagine deallocare?

Per PFRA ci sono diversi tipi di pagine:

- **Non deallocabili** 
	- Pagine statiche del SO dichiarate non deallocabili
	- Pagine allocate dinamicamente dal SO
	- Pagine appartenenti alla sPila dei processi
- **Mappatae sui file eseguibile dei processi** (codice, costanti)
- **Pagine anonime** che richiedono una swap area su disco
	- pagine dati
	- pagine della uPila
	- pagine dello Heap
- **Pagine mappate su file** (buffer/cache) 


Prima di tutto dealloca le pagine non utilizzate da nessun processo (ref_count = 1) in ordine di NPF

## Meccanismi chiave

Se non è sufficiente, l'algoritmo utilizzato da PFRA si basa su principio LRU (least recently used), quindi dobbiamo:
1. mantenere informazioni relative all'accesso delle pagine
2. avere un algoritmo efficiente per scegliere le pagine meno usate

Per gestire queste informazioni usiamo due liste:
- **active list**: contiene tutte le pagine accedute di recente e queste non posso essere deallocate
- **inactive list** pagine inattive da molto tempo che sono candidate per essere deallocate

### Spostare pagine tra le liste


[[x64]] non tiene traccia del numero di accessi alla memoria, quindi linux approssima questo dato con il bit di accesso A alla pagine nel TLB:
- **A** posto ad 1 ogni volta che si accede alla pagine
- **A** azzerato periodicamente

Ad ogni pagine viene associato il flag **ref** che serve per raddioppiare il numero di accessi necessari per spostarla da una lista all'altra.


#### Controlla_lista
Inoltre definiamo una funzione Controlla_lista (attivata da kswapd) che esegue una scansione di entrambe le liste:
1. scansiona **active list**  partendo dalla coda ed eventualmente sposta alcune pagine inattive.
	1.  A = 1
		- azzera A
		- ref = 1 $\implies$ sposta P in testa alla active
		- ref = 0 $\implies$ ref = 1
	2. A = 0
		- ref = 1 $\implies$ ref = 0
		- ref = 0 $\implies$ P in testa alla inactive con ref = 1

2. scansione **inactive list** partendo dalla testa spostando eventualmente alcune pagine alla active (non scansiona quelle appena spostate).
	1. A = 1
		- azzera A
		- se ref = 1 $\implies$ sposta P in coda alla active con ref = 0
		- se ref = 0 $\implies$ ref = 1
	2. A = 0
		- se ref = 1 $\implies$ ref = 0
		- ref = 0 $\implies$ P in coda alla inactive

La pagina viene scansionata solo utilizzando **A** e **ref**




#### Allocare nuove pagine
Funzioni che allocano nuove pagine:
- richieste da un processo, poste nella lista active con ref = 1
- richieste da un processo figlio appena creato e poste nella lista active o inactive nello stesso ordine o con lo stesso ref del processo padre

#### Eliminazione delle pagine dalle liste
Funzioni che eliminano dalle liste le pagine swapped out o deallocate definitivamente per la terminazione di un processo
