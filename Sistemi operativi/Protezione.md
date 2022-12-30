---
alias: diritti d'accesso
---
I Dati memorizzati nel file di un file system necessitano di protezione, viene definita quindi una politica d'accesso, di cui le piú banali sono:
- Accesso a tutti i file da parte ogni utente
- Ogni utente puó accedere solo ai propri file


Si definiscono delle regole di accesso ai file in base a:
- L'identità degli utenti
- La proprietà dei file
- L'operazione richiesta (lettura, scrittura, esecuzione, eliminazione)

## Liste di accesso
L'accesso e le operazioni consentite dipendono dall'identità dell'utente, ogni file ha quindi una lista d'accesso che indica che operazioni sono consentite e che operazioni non lo sono, il sistema operativo controlla la lista di accesso per verificare se
- Il richiedente è previsto
- Il richiedente ha il permesso di compiere quel tipo di operazione

Tuttavia le liste di accesso possono diventare molto grandi, sono a singolo file e richiedono un tempo di accesso ai file medio maggiore.

Gli utenti sono identificati in base a:
- Username: identificativo dell'utente
- Group: 