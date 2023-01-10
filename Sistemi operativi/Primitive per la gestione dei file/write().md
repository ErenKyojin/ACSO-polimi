
Aggiunge dati ad un file già creato/aperto, è necessario fornire descrittore ottenuto tramite [[open()]] o [[creat()]] ed un puntatore ai dati da scrivere. Restituisce il numero di caratteri effettivamente scritti alla fine dell'esecuzione della primitiva


```C
int read(int fd, char buffer[], int num_byte);
```


Byte_scritti = write(fd, buf, num_byte)

- Byte_scritti restituisce il numero di caratteri scritti
- fd: è il descrittore del file
- buf: indirizzo dell'area che contiene i dati da scrivere
- num_byte: numero di byte da scrivere


Il [[Sistemi operativi/File System]] mantiene un indicatore alla posizione nel file in cui deve essere effettuata la lettura/scrittura successiva



