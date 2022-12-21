Preleva dati da un file già creato/aperto, è necessario fornire il descrittore tramite [[open()]] o [[creat()]] ed un puntatore ai dati da leggere. Restituisce il numero di caratteri effettivamente letti alla fine dell'esecuzione della primitiva (-1 se errore)

### prototipo
```c
int read(int fd, char buffer[], int num_byte)
```

### utilizzo
```c
int byte_letti = read(fd, buf, num_byte)
```

- *byte_letti:* numero di caratteri letti
- *fd:* file descriptor
- *buf:* indirizzo dell'area dati del processi che conterrà i dati letti
- *num_byte:* numero di byte da leggere

---
>[!oss]
>Il file system mantiene un indicatore alla posizione nel filei n cui deve essere eeffettuata la lettura scrittura successiva


