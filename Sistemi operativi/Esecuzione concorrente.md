---
alias: esecuzione parallela
---
Date due task A e B nel codice di un programma sono concorrenti se non possiamo prevedere quale verrà svolta prima, ossia non possiamo prevedere la sequenza di esecuzione. 
L'opposto è [[Esecuzione sequenziale]]


## Simulata
Se ci si trova su un ambiente mono [[Processore]] con [[processo|processi]] eseguiti "a turni"

## Reale
Se in un sistema multi processore i processi o i [[Thread]] sono in esecuzione contemporaneamente su processori diversi


A prescindere i processi e i thread sono concorrenti, ed anche nel caso di esecuzione concorrente reale è possibile sfruttare anche il simulato.


[[Granularità]] poche istruzioni in multi threading su un mono processore o centinaia/migliaia di istruzione per multi threading su multi processore 


# POSIX
Modello di implementazione dello standard parallelo, è incluso nel file header `<pthread.h>`

## pthread
Ogni pthread ha un: 
- `pthread_t` identifica univocamente il thread
- `pid_t` identifica univocamente il pid

Tutti i thread dello stesso processo avranno lo stesso PID, quindi ogni thread avrà come identificatore il processo a cui appartiene che identifica un [[thread group]].


## Creazione di un pthread
`pthread_create()` simile a `fork()`, ma `pthread_create()` vuole come parametro il nome della funzione che deve eseguire, partendo a prescindere dall'inizio di questa:

`pthread_create(&tID1, NULL, &tf1, void(*) n);`

1. Indirizzo di una variabile pthread_t per l'ID del thread (thread_ID)
2. Puntatore agli attributi del thread
3. Indirizzo della funzione eseguita dal thread (thread_function)
4. Indirizzo dell'argomento che si vuole passare alla (thread function)


Terminazione di un `pthread_join` simile a `waitid()`



>[!multi-column]
>
>>[!c]
>>```c
>>#include <pthread.h> <stdio.h>
>>
>>void* tf1 void(* tID){
>>	...
>>}
>>
>>int main(void){
>>	pthread_t tID1, tID2;
>>	pthread_create (&tID1, NULL, &tf1, (void *) 1);
>>	pthread_create (&tID2, NULL, &tf1, (void *) 2);
>>	pthread_join (tID1, NULL);
>>	pthread_join (tID2, NULL);
>>	return 0;
>>}
>>``` 
>
>>[!C]
>>```C
>>void * tf1 (void * tID){
>>	
>>	int conta = 0
>>	cont++;
>>	printf("sono il thread n: %d; conta = %d\n",(int) tID, conta);
>>	return NULL;
>>}
>>```


# Thread o Processi
- Thread usano meno risorse $\implies$ più efficiente del processo
- Thread può danneggiare con errori altri thread $\implies$ processi più protetti
- Processi più flessibili (tramite [[exec]])
- Condivisione dei dati tra thread molto più semplice, tra processi è complicata


>[!failure]
>Impossibile determinare quale istruzione viene eseguita prima, ossia non è deterministico




>[!esempio] slide 5 (1.3)


[[sequenze critiche]]


