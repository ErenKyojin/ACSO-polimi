Incluso nella libreria `<pthread.h>` è una variabile di tipo `sem_t`
Per le operazioni è considerato simile ad un `unsigned int`, viene inizializzato come `sem_init()`
>[!esempio]
>`sem_init(&sem1,0,0)`


`sem_wait(...)` decremento il valore del semaforo:
- se sem > 0  (pre decremento) allora il thread decrementa il semaforo e prosegue l'esecuzione
- se sem == 0 (pre decremento) allora il thread che ha chiamato sem_wait() rimane bloccato fino ad una chiamata a sem_post() che fa diventare il semaforo > 0 nuovamente

`sem_post(...)` incrementa il valore del semaforo


Il valore del semaforo rappresenta il numero di risorse disponibili, quando uguali a zero non ce ne sono


>[!esempio]
>Due thread stampano `abc` e `xyz` rispettivamente, noi vogliamo farli stampare esattamente `axbycz`
>- tf1 stampa x, y, z
>- tf2 stampa a, b, c
>
>Sfruttiamo due semafori: 
>1. **Sem1** blocca tf1 x,y,z
>2. **Sem2** blocca tf2 a,b,c
>
> inizializziamo i semafori a 0
>
> il primo thread che esegue tf1 esegue subito una `sem_wait(&sem1)`
> e si blocca, il secondo thread che esegue tf2 stampa `a`, esegue una `sem_post(&sem1)` per sbloccare il primo thread e prosegue con una `sem_wait(&sem2)` per bloccarsi, viene quindi stampata la x e si continua in questo ciclo
>
>