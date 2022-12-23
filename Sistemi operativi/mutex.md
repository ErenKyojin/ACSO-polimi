Un tipo speciale di [[Thread|pthread]] che ha attiva la mutua esclusione, si dichiara con `pthread_mutex_t`
si inizializza tramite `pthread_mutex_init`
Si blocca e sblocca tramite:
- `pthread_mutex_lock`
- `pthread_mutex_unlock`


# Come funzionano i mutex?

Proviamo a risolvere una [[sequenze critiche|sequenza critica]] senza mutex:
Creiamo una variabile globale blocca intera:
- blocca == 1 sequenza bloccata già in esecuzione
- blocca == 0 sequenza sbloccata può essere eseguita da parte di un thread

>[!multi-column]
>>[!C] mutex lock?
>>```c
>>while(blocca == 1)
>>{
>>	blocca = 1;
>>}
>>```
>
>>[!c] mutex unlock?
>>```c
>>blocca = 0
>>```

>[!error]
>Se entrambi i thread escono dalla while con esecuzione di istruzioni successive, allora una variabile non è sufficente


## n variabili per n thread

$blocca_{n}$ rappresenta l'intenzione del thread $n$ di accedere alla sequenza critica
>[!multi-column]
>>[!c] `void spam(arg)`
>>```c
>>{
>>	if( (int) arg == 1)
>>		while (blocca2 = 1);
>>	if( (int) arg == 1)
>>		while (blocca1 = 1);
>>	//inizio sequenza critica
>>
>>...
>>
>>	if((int) arg == 1) blocca1 = 0;
>>	if((int) arg == 2) blocca2 = 0;
>>	return null;
>>}
>>//fine sequenza critica
>>```
>

>[!success] mutua esclusione garantita

>[!error] [[Deadlock]]

## thread favorito
Aggiungiamo una variabile che ogni thread la imposterà sul valore di un altro thread per rende l'altro thread preferenziali le per entrare nella sequenza, l'ultimo che la esegue resterà in attesa


>[!c]
>```c
>int favorito = 1, blocca1 = 0, blocca2 = 0;
>
>void spam(void * arg){
>	if ((int) arg == 1){
>	blocca1 = 1;
>	favorito = 2;
>	while (blocca1 == 1 && favorito == 1);
>	}
>	if ((int) arg == 2){
>	blocca2 = 1;
>	favorito = 1;
>	while (blocca1 == 1 && favorito == 1);
>	
>	...
>	
>	if ((int) arg == 1 ) blocca1 = 0;
>	if ((int) arg == 2) blocca2 = 0;
>	}
>}
>```

