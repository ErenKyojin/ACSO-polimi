Per interrompere un [[link()]] creato tra due file, ossia eliminare un riferimento ad un file specificato tramite nome.

Nel caso in cui esista un solo link al file e nessun processo lo ha aperto, il numero dei link diventa 0 ed il file viene essenzialmente eliminato dal [[Sistemi operativi/File System]] (diventa inaccessibile ed i blocchi dati associati vengono rilasciati), in questo caso bisogna:
- deallocare l'[[i-node]] dal file system (e quindi veien aggiunto alla free i-node list)
- deallocare i blocchi dati sul dispositivo fisico (che viene quindi aggiunto alla lista dello spazio disponibile *free list*)

Nel caso in cui invece esiste un solo link al file ma almeno un processo ha aperto al file la unlink non viene eseguita fino a quando l'ultime file descriptor è stato chiuso con una [[close()]]


### Prototipo

```c
int unlink(char *nome_file)
```


### utilizzo
```c
unlink(nome_file)
```