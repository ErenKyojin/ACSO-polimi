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