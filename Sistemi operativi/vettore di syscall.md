Durante la fase di boot linux inizializza il vettore di syscall con la coppia
- Indirizzo della funzione system_call()
- PSR opportuno per l'esecuzione della system_call()

system_call() costituisce il punto di entrata unico per tutti i servizi di sistema di [[Linux]]
- `sys_read`
- `sys_write`
- `sys_open`
- `sys_close`
