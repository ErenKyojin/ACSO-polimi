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


