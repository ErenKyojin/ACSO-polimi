Linux gestisce i file system a livello logico attraverso dispositivi logici detti [[volumi]], un [[file]] è visto dal file system come una sequenza di [[blocco#Blocchi logici]]

Per mappare da blocchi logici a blocchi fisici e viceversa utiliziamo la tecnica di [[i-node]]

# Struttura gerarchica del file system
Un file system è organizzato in:
- **PARTIZIONI** che contengono insiemi di file correlati
- **[[DIRECTORY]]** ogni partizione è divisa in directory che contengono informazioni sui file o sulle directory stesse dipendenti dalla prima
	- *root directory*: directory accessibile direttamente dal file system, si indica con `/`
- **FILE** che contengono i dati o i programmi

Inoltre sono importani le nozioni di:
- **Pathname assoluto**: la concatenazione deei nomi delle directory dal root fino al file, ad esempio `/usr/nome_file`
- **Pathname relativo**: Il nome del file nella directory a cui appartiene, ad esempio `nome_file`

---
# Struttura fisica del file system

Il file system accede ai dispositivi fisici tramite l'invocazione di comandi messi a disposizione dal disk driver, e la memoria viene rappresentata e gestitia come un dispositivo logico detto volume (un vettore di blocchi logici multiplo di 512 Byte, il blocco viene trasferito in memoria con un unica operazione)

Inoltre l'hard disk è diviso in [[traccia|tracce]] e [[settore|settori]].

L'operazione di formattazione predispone tracce e settori per la lettura e la **scrittura**

![[Pasted image 20221231105048.png|500]]

## Prestazioni:
- Il tempo di accesso è sugli ordine dei ms
	- **Seek time**, la testina deve arrivare alla traccia giusta, impegando dai 5 ai 15 ms
	- **Latency**, il disco deve ruotare fino a portare il dato nella posizione giusta, dipende dalla velocità di rotazione (5400 - 10800 RPM $\to$ 5.4 - 2.7 ms)

- Il transfer rate del disco varia dipendentemente alla densità di registrazione e alla velocità di rotazione, va dai 5 ai 20 MB/s

# Strutture dati del file system

## Tabella dei descrittori dei file aperti per processo

Esiste una tabella per ogni [[processo]] attivo nel sistema. Indice dell tabella è il descrittore del file (fd), ed ogni entry contiene un puntatore relativo al file

>[!oss]
>Per convenzione ogni precosse ha 3 descrittori aperti automaticamente, associato ai primi tre elementi della tabella:
>- stdin (0)
>- stdout (1)
>- stderr (2)
>  

>[!esempio] fd1
>
>0 | stdin
>--- | ---
>1 | stdout
>2 | stderr
>3 | ...
>4 | ...

-------


## Tabella globale dei file aperti
Tabella globale del sistema operativo con una riga per ogni file aperto nel sistema, l'indice della tabella sono i puntatori provenienti dalle tabelle dei descrittori dei file paerti dei processi, ogni entry contiene:
- Offset nel file: posizione corrente nel file per il prossimo accesso, sono i byte rispetto all'orogine del file 
- Modalità di apertura: Read, write, RW
- Numero di riferimenti: Da parte dei processi a questo file se dovesse essere condiviso (esempio: fork )
- Puntatore corrispondente: i-node nella tabella degli i-node

-------

## Tabella degli i-node (detta in-core i-node)
Tabella globale del sistema che contiene una copia in memoria degli i-node relativi al volume (detti in-core i-node).

Ogni entry della tabella contiene una copia in memoria degli i-node statici presenti su disco nella i-list.
Ogni entry della tabella contiene il contatore al numero di riferimenti che indica il numero di istanze del file che sono attivi.

>[!esempio]
>Due processi P0 e P1 aprono il file F, P0 ottiene il descrittore fd1 mentre P1 il descrittore fd7, nella tabella globale dei file aperti ognuno di questi descrittori avrà un riferimento, ma nella tabella degli i-node il file F avrà due riferimenti

Oltre alla copia delle informazioni presenti nel corrispondente i-node statico sono presenti informazioni riguardanti lo stato dell'i-node.

-----


![[Esempio strutture dati filesystem (1).canvas]]
##