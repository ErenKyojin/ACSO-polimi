La tecnica di i-node permette di mappare [[blocco#Blocchi logici]] e [[blocco#Blocco nel volume]] mediante una lista.
Ogni file ha associato un i-node ed ogni i-node contiene 64 Byte di informazioni, gli i-node dei file in un disco sono memorizzati in sequenza e formano la i-list, inoltre ogni i-node è accessibile tramite indice.



# Informazioni contenute nell'i-node

- Tipo di file:
	- **d**: directory
	- **b**: file speciale per device a blocchi
	- **c**: file speciale per device a caratteri
-  Proprietario del file (**owner**) e gruppo (**group**) ([[Protezione#Gruppi di utenti]])
- bit di protezione: **control access list** ([[Protezione#Controll access list]])
- **Numero di link** al file fisico cioè allo stesso i-node
- **Dimensione** in blocchi del file e dimensioni del blocco
- **Puntatori ai blocchi dell'area dati**: 13 indirizzi referenziano in modo diretto o indiretto i blocchi dati
- **Data ora** dell'*ultimo accesso* al file
- **Data e ora** dell'*ultima modifica* dell'i-node

## rappresentazione di un i-node


| i-node                 |
| ---------------------- |
| Mode                   |
| Owner, group           |
| Timestamp              |
| Size                   |
| Number of blocks       |
| Number of references   |
| </br> </br> </br> Direct blocks (10) </br> </br> </br> </br>     |
| Single indirect blocks |
| Double indirect blocks |
| Triple indirect blocks |


## Allocazione indicizzata

I primi 10 indirizzi su disco sono i puntatori ai blocchi del file su disco (indirizzamento diretto di 10 blocchi).

Per file piú grandi l'i-node contiene l'indirizzo di un blocco chiamato **single indirect block**, questo blocco contiene 128 indirizzi da 4 byte. (indirizzamento indiretto di 128 blocchi).

L'inode mette a disposizione un altro indirizzo, **detto double indirect block**, che contiene l'indirizzo di un blocco che contiene una lista di 128 single indirect block.

Esiste anche un **triple indirect block** nel caso in cui la doppia indicizzazione non sia sufficiente e sia necessario un altro livello di indicizzazione: indirizzamento indiretto triplo di 128x128x128 blocchi.

![[Rappresentazione inode.canvas]]
# I-list

Quando viene creato il file system da associare ad un [[volumi|volume]] attraverso il comando `mkfs` viene allocata la lista di dimensione fissa contenente gli i-node, detta i-list, questa lista è costituita da una serie di i-node utilizzati o liberi (che sono tali se il tipo di file indicato è `0`). Le posizioni degli i-node sono riportate nella free i-node list, contenuta nel superblocco. 

## Spazio libero
L'inizio della lista concatenata dei blocchi liberi (free list) è contenuto nel superblock:
![[Lista dei blocchi liberi.canvas]]