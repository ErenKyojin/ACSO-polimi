Creazione di un file ordinario, aggiunge un nuovo file al [[Sistemi operativi/File System]], e restituisce un intero che rappresenta il descriptor da usare in una seguente chiamata di sistema:

### Prototipo

```c
int creat(const char *file_name, mode_t mode);
```

- mode gestisce la modalità di accesso

### Chiamata
```c
int fd = creat(file_name, mode);
```

- fd: file descriptor

------

>[!oss]
>Se `file_name` esiste allora il contenuto del file viene cancellato e la dimensione diventa 0


>[!oss]
>Per file speciali si usa `mknod` e per le directory si usa `mkdir`


