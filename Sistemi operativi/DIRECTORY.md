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

Per creare una directory si usa la funzione `mkdir()`
