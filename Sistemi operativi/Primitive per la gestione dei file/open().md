Apertura di un file ordinario, sulla base del nome del file viene trovato su discoe viene restituito un intero che rappresenta il file descriptore da usare in una seguente chiamata di sistema


### Prototipo
```c
int open(const char *file_name, int flags mode_t mode);
```

- flags: tipo o modalità di apertura del file
	- O_RDONLY lettura
	- O_WRONLY scrittura
	- O_RDWR lettura e scrittura

- mode gestisci i permessi di accesso

### Utilizzo

```c
fd = open(file_name, O_RDONLY | O_WRONLY | O_RDWR, mode);
```