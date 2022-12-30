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
Tabella globale del sistema che contiene una copia in memoria degli i-node relativi al volume.

Ogni entry della tabella contiene una copia in memoria degli i-node statici presenti su disco nella i-list.
Ogni entry della tabella contiene il contatore al numero di riferimenti che indica il numero di istanze del file che sono attivi.

Oltre alla copia delle informazioni presenti nel corrispondente i-node statico sono presenti informazioni riguardanti lo stato dell'i-node

-----


![[Esempio strutture dati filesystem (1).canvas]]
