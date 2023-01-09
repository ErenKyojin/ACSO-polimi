Determina quando e quante pagine deallocare ed è invocato in:

- **Invocazione diretta** se un processo richiede **requiredPages** e
	*freePages - requiredPages < minFree*
- Attivazione periodica tramite kswapd ([[kernel swap daemon]]), funzione che viene attivata regolarmente e che invoca PFRA se **freePages < maxFree*


E dealloca toFree = maxFree - freePages + requiredPages

## Parametri
- **freePages** numero di pagine libere in memoria fisica
- **requiredPages** numero di pagine che vengono richieste per una certa attività da parte di un processo o del SO
- **minFree** numero minimo di pagine libere sotto il quale non si vorrebe scendere *livello critico*
- **maxFree** numero di pagine libere al quale PFRA tenta di riportare freePages *livello obiettivo*


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
- **Pagine mappate su file** (buffer/cache) appartenenti ai buffer/cache

## Processo decisionale
Prima di tutto dealloca le pagine non utilizzate da nessun processo (ref_count = 1) in ordine di NPF

Se non è sufficiente, l'algoritmo utilizzato da PFRA si basa su principio LRU (least recently used), quindi dobbiamo:
1. mantenere informazioni relative all'accesso delle pagine
2. avere un algoritmo efficiente per scegliere le pagine meno usate

Per gestire queste informazioni usiamo due liste:
- **active list**: contiene tutte le pagine accedute di recente e queste non posso essere deallocate
- **inactive list** pagine inattive da molto tempo che sono candidate per essere deallocate

### Spostare pagine tra le liste


[[x64]] non tiene traccia del numero di accessi alla memoria, quindi linux approssima questo dato con il **bit di accesso A** alla pagine nel TLB:
- **A** posto ad 1 ogni volta che si accede alla pagine
- **A** azzerato periodicamente

Ad ogni pagina viene associato il flag **ref** che serve per raddioppiare il numero di accessi necessari per spostarla da una lista all'altra (negli esercizi il ref si indicherà sinteticamente scrivendo le pagine con lettere maiuscole se = 1 e con lettere minuscole se = 0 )







#### Allocare nuove pagine
Funzioni che allocano nuove pagine:
- richieste da un processo, poste nella lista active con ref = 1
- richieste da un processo figlio appena creato e poste nella lista active o inactive nello stesso ordine o con lo stesso ref del processo padre

#### Eliminazione delle pagine dalle liste
Funzioni che eliminano dalle liste le pagine swapped out o deallocate definitivamente per la terminazione di un processo

### Deallocazione delle pagine in inactive

Per deallocare pagine virtuali della lista inactive, bisogna prima considerare se sia adatta


# OOMK
In sistemi carichi il PFRA può non risolvere la situazione, in tal caso invoca il OOMK (out of memory killer) che eselzione un processo e lo limina
Viene invocato quando la memoria libera è estremamente poca e PFRA non ha migliorato la situazione, in particolar modo ha una funzione `select_bad_process()` che fa una scelta inteligente del processo:
- Processo con molte pagine occupate
- Poco lavoro svolto
- Poca priorità
- Nessun privilegio di root
- Non gestisca componenti hardware