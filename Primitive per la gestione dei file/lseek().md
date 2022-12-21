Riposiziona l'indicatore di lettura o scrittura di un file aperto


### prototipo
```c
long lseek(int fd, long offset, int base)
```

modifica la posizione corrente nel file fd e la restituisce come long int, la nuova posizione corrente nel file new_offset viene calcolata sommango all'argomento `offset` il valore di `base` con:
- base = 0: inizio file
- base = 1: posizione corrente nel file
- base = 2: fine file