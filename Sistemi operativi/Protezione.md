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

Tuttavia le liste di accesso possono diventare molto grandi, sono a singolo file e richiedono un tempo di accesso ai file medio maggiore. Linux utilizza quindi un approccio piú semplificato, dividendo tutto in classi:

#### Classi di utenti
Gli utenti sono identificati in base a:
- Username: identificativo dell'utente
- Group: identificativo del gruppo

#### Gruppi di utenti
Gli utenti sono raggruppati: 
- Owner: proprietario del file
- Group: Gruppo del proprietario del file
- All: tutti gli utenti

#### Classi di operazione
- Read: lettura
- Write: scrittura
- Execute: esecuzione

#### classi di file
Ogni file ha associato
- Owner
- Group
- Control access list

## Controll access list
Tre gruppi di bit, ogni gruppo si riferisce ad una classe di utenti, ed ogni bit di un gruppi si riferisce ad un;operazione

| owner | group | all |
| ----- | ----- | --- |
| rwx   | rwx   | rwx |  

| rwx | r<font color = 4a4a4a>~~w~~</font>x | r<font color = 4a4a4a>~~w~~</font>x |
| --- | ----------------------------------- | ----------------------------------- |
| 111 | 101                                 | 101                                 |
| 7   | 5                                   | 5                                    |



