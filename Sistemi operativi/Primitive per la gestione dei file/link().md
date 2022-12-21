Permette di creare un alias, aumenta di uno il numero di riferimenti all'i-node, l'opposto è l'[[unlink()]], per associare un nuovo nome ad un file già esistente. Crea una nuova entry nella directory che contiene il file.


### prototipo
```c
int link(char *nome_file, char *nuovo_nome_file)
```
Restituisce un intero (esito dell'operazione)

### utilizzo

```c
link(old_file_name, new_file_name);
```
