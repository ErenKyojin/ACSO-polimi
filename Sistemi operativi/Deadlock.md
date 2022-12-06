Quando un [[Thread]] $1$ attende l'azione di un altro thread $2$ e contemporaneamente il thread $2$ aspetta l'azione del thread $1$ per proseguire si ha un deadlock, o attesa circolare, che non ha via d'uscita.
La soluzione al deadlock è il [[mutex#thread favorito]]

In particolare si genera un deadlock quando due thread devono bloccare due risorse A e B con due mutex diversi ma le bloccano in ordine inverso

>[!esempio]
>t1 blocca $A$ ed attende di poter bloccare $B$
>t2 blocca $B$ ed attende di poter bloccare $A$


>[!multi-column]
>
>>[!c]
>>```c
>>#include <pthread.h> <stdio.h>
>>pthread_mutex_t mutexA, mutexB;
>>
>>void *lockApoiB (void* arg){
>>pthread_mutex_lock(&mutexA); //ist1
>>... //iniz 1
>>pthread_mutex_lock(&mutexB); //ist2
>>... //iniz fin 2
>>pthread_mutex_unlock(&mutexB); //ist3
>>...//fin 1
>>pthread_mutex_unlock(&mutexA); //ist4
>>return NULL;
>>}
>>
>>void *lockBpoiA (void* arg) {
>>pthread_mutex_lock(&mutexB); //ist5
>>...
>>pthread_mutex_lock(&mutexA); //ist6
>>...
>>pthread_mutex_unlock(&mutexA); //ist7
>>...
>>pthread_mutex_unlock(&mutexB); //ist8
>>return NULL;
>>}
>>```
>>Percorso che genera deadlock ist1 -> ist 5 -> ist 2 !(esempio, ce ne sono altri)
>
>>[!c] main

