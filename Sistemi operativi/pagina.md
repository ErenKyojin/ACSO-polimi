4 Kb di memoria, quindi 12 bit di offset


## Pagine non reisdenti in memoria
Se il numero di pagine virtuali dei processi eccede il numero di pagine disponibili nella memoria, allora alcune pagine devono risiedere su disco, se l'accesso alla memoria appartiene ad una pagina non residente si genera un [[Interrupt]] di segnalazione errore **page fault**.

Lo spazio su disco per contenere le pagine virtuali è detto [[swap file]] ed è gestito dal [[sistema operativo]]

Se la pagina è su disco ha un bit di validità impostato a 0.backing store

| valido | pagina fisica o indirizzo su disco |
| ------ | ---------------------------------- |
| 1      | -> mem                             |
| 1      | -> mem                             |
| 1      | ->mem                              |
| 1      | ->mem                              |
| 0      | -> disc                            |
| 1      | -> mem                             |
| 1      | ->mem                              |
| 0      | -> disc                            |
| 1      | -> mem                             |
| 1      | -> mem                             |
| 1      | ->mem                              |
| 0      | -> disc                            |
| 1      | -> mem                             |


## Protezione delle pagine

La [[Memoria virtuale#Memory managment unit]] è in grado di riconoscere l'accesso da parte di un programma ad un'area di memoria a cui non dovrebbe poter accedere, questo viene fatto conforntando l'NPV incriminato con la tabella di tutte le pagine appartenenti al processo, se questo NPV non ne fa parte l'unità di memorià genera un [[Interrupt]] di violazione


## Diritti d'acesso
Inoltre ad ogni pagina virtuale sono associati dei bit di protezione che descrivono la modalità di accesso alla pagina:
- **R**, modalità di read only
- **W**, modalità di write
- **X**, modalità di esecuzione (nel caso in cui la pagina contenga codice)

Anche in questo caso, se i diritti d'acesso vengono violati si genera un iterrupt di violazione memoria


# Pagine in [[x64]]

In x64 tutta la memoria è paginata, anche la [[tabella delle pagine]] stessa, ogni pagina è 4K byte, ossia ha uno spiazzamento interno di 12 bit (offset), mentre il numero di pagina virtuale è $2^{48} / 2^{12} = 2^{36}$ bit per il NPV, quindi l'indirizzo è:

NPV (36 bit) $\qquad\qquad$| offset (12 bit)
--- | ---


In particolare la tabella delle pagine deve contenere le informazioni di $2^{36}$ pagine, è residente in memoria fisica e mappa tutto lo spazio di indirizzamento ([[user space]] e [[Kernel space]])

# ZeroPage
Pagina fisica inizializzata a zero