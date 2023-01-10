Duplica un descrittore associato ad un file aperto, si aggiune quindi un riga nella [[Sistemi operativi/File System#Tabella dei descrittori dei file aperti per processo|tabella dei file aperti]] da quel processo che punto allo stesso file aperto nella tabella globale

### prototipo
```c
int dup(int old_fd);
```

### utilizzo:
```c
fd1 = open(...);
fd2 = dup(fd1);
```

La posizione corrente nel file è comunque la stessa per i due o più descrittori e si incrementa il numero dei riferimenti al file nella tabella globale, non si incrementa il numero dei riferimenti all'i-node del file nella tabella degli i-node.