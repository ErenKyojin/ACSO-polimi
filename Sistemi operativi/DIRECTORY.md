Le directory sono dei [[File]] (d) caratterizzati da nome e diritti d'accesso, ogni directory contiene informazioni sui file e sulle directory che contiene.
Una directory fornisce le corrispondenze tra nome di file/directory e file/directory stesse su disco, con una entry per ogni file/directory, ed è quindi essenzialmente una tabella.

>[!Esempio]
`<nome_file/nome_dir, riferimento>`
>
> | nome_file / nome_dir | Riferimento [[i-node]] (posizione file su disco) |
> | --- | ---|
> | . (curr dir) | 3|
> | .. (dir padre)| 2 |
> | usr | 4 |
> | nome_file_1 | 7|
> | nome_file_2 | 8 |
> | ... | ...
>  


## Operazioni
Come per quanto riguarda i file, anche per le directory ci sono molteplici operazioni possibili
- Ricerca file
- Creazione file
- Rimozione file
- Elenco file
- Rinonima di un file
- Coppia di un file

## Organizzazione
Contenere tutti i file in un'unica directory è una scelta molto semplice quanto problematica, la ricerca diventa inefficente, non possono essere presenti nomi uguali e bisogna gestire gli accessi per ogni singolo file, si utilizza quindi un organizzazione su due livelli:
- Directory principale  contiene un elenco di directory (`root`)
- Directory utente: cotneine i file di un singolo utente (`home`)

I singoli utenti possono gestire i file solo nella propria directory, per il root invece deve farlo un amministratore di sistema (root, admin, superuser)

![[Directory a due livelli.canvas]]


Estensione della directory a due livelli è la directory ad albero, per accedere ai file si usa il pathname (o assoluto o relativo), si definisce inoltre il **cwd** (current working directory), se un file non è nella directory corrente si usa il pathname assoluto o si cambia la directory corrente:

Comandi per la gestione della cwd:
- `cd <dir>`, change dir, cambia la cwd nella directory specificata 
- `pwd`, print working dir


![[Directory ad albero.canvas]]
