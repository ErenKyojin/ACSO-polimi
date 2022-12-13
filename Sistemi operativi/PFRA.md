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

Ad ogni pagine viene associato il flag **ref** che serve per raddioppiare il numero di accessi necessari per spostarla da una lista all'altra

Inoltre definiamo una funzione Controlla_lista (attivata da kswapd) che esegue una scansione di entrambe le liste:
1. scansiona **active list** e sposta alcune pagine inattive
2. **scansione inactive list** partendo dalla testa