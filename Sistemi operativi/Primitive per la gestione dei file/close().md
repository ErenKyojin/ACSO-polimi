Chiude un descrittore di file aperto, elimina il descrittore dalla [[Sistemi operativi/File System#Tabella dei descrittori dei file aperti per processo]]. Decrementa il numero di riferimenti al file nella tabella globale e solo se non vi sono altri riferimenti elimina l'elemento dalla tabella globale dei file aperti ed il corrispondente puntatore alla tabella degli i-node.


### Prototipo
```c
int close(int fd)
```
- fd descrittore di file aperto
- restituisce un intero:
	- 0 = successo
	- -1 = errore di chiusura

### utilizzo
```c
close(fd);
```