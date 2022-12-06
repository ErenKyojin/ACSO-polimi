Definiamo una sequenza, che è un'insieme di istruzioni eseguite da un [[Thread]]
$$
ti_{j}
$$
Istruzione $j$ eseguita dal thread $i$.
- Relazione temporale tra istruzioni
	- nello stesso thread $ti_{1} < ti_{2} < ti_{3} < \dots < ti_{n}$
	- tra thread diversi $t1_{1} < t1_{2} < t2_{1} < \dots < ti_{n}$

Sequenza critica, ossia sequenze di istruzioni eseguite dai thread paralleli che non devono essere mescolate affinchè il risultato sia corretto.

Eseguiamo quindi la sequenza tra i vari thread in modo che
- Se un qualsiasi thread comincia l'esecuzione della sequenza tutta la sequenza viene eseguita dal thread prima di essere eseguita da qualsiasi altro thread

>[!esempio]
>Dati due conti bancari `contoA` e `contoB` vogliamo realizzare una funzione `trasferisci` che prelevi da `contoB` e depositi sul `contoA`, la somma dei due conti dovrà essere invariata (proprietà #invariante)
>1. `contoA` nella variabile locale `cA`
>2. `contoB` nella variabile locale `cB`
>3. Aggiorna `contoA` a `contoA + importo`
>4. Aggiorna `contoB` a `contoB + importo`
>
> val | inizio | t1.1 | t1.2 | t1.3 | t2.1 | t2.2 | t2.3 | t2.4 | t1.4
> ---| --- |--- |--- | --- | --- | --- | --- |--- | --- | 
> contoA | 100 | | | 110 | | |130 | | 
> contoB | 200 | | | | | | | 180 | 190
> cA (in t1) | | 100 | | | | | |
> cB (in t1) | | 200 | | | | | |
> cA(in t2) | | | | 110 | | | | |
> cB (in t2) | | | | |200 | | | |

>[!multi-column]
>
>>[!failure]
>>```c
>>#include <pthread.h> <stdio.h>
>>int contoA = 100, contoB = 200;
>>int totale;
>>
>>void * trasferisci (void *arg) {
>>int importo = * ((int *) arg);
>>int cA, cB;
>>//inizio sequenza critica
>>cA = contoA;
>>cB = contoB;
>>contoA = cA + importo;
>>contoB = cB + importo;
>>return NULL;
>>}
>>
>>int main(void){
>>pthread_t tID1, tID2;
>>int importo1 = 10, importo2 = 20;
>>pthread_create (&tID1, null, trasferisci, &importo1);
>>pthread_create (&tID2, NULL, trasferisci, &importo2);
>>pthread_join(tID1, NULL);
>>pthread_join(tID2, NULL);
>>totale = contoA + contoB;
>>printf("contoA = %d,  contoB=%d\n", contoA, contoB);
>>printf("tot: %d",totale);
>>return 0;
>>}
>>```
>
>
>>[!success]
>>```c
>>#include <pthread.h> <stdio.h>
>>int contoA = 100, contoB = 200;
>>int totale;
>>//dichiarazione mutex
>>pthread_mutex_t conti;
>>
>>void * trasferisci (void *arg) {
>>int importo = * ((int *) arg);
>>int cA, cB;
>>//inizio sequenza critica, quindi lockiamo
>>pthread_mutex_lock(&conti);
>>
>>cA = contoA;
>>cB = contoB;
>>contoA = cA + importo;
>>contoB = cB + importo;
>>//fine sequenza critica, sblocchiamo il mutex
>>pthread_mutex_unlock(&conti)
>>return NULL;
>>}
>>
>>int main(void){
>>pthread_t tID1, tID2;
>>int importo1 = 10, importo2 = 20;
>>//inizializziamo il mutex
>>pthread_mutex_init(&conti, NULL);
>>pthread_create (&tID1, null, trasferisci, &importo1);
>>pthread_create (&tID2, NULL, trasferisci, &importo2);
>>pthread_join(tID1, NULL);
>>pthread_join(tID2, NULL);
>>totale = contoA + contoB;
>>printf("contoA = %d,  contoB=%d\n", contoA, contoB);
>>printf("tot: %d",totale);
>>return 0;
>>}
>>```

Sfruttiamo [[istruzioni atomiche]], se tutte le istruzioni sono atomiche (ossia singole ed indivisibili) allora ogni ordinamento delle istruzioni da un risultato corretto.

>[!multi-column]
>>[!bug]
>> Il problema è che istruzioni atomiche in C possono non essere atomiche in assembly, in generale istruzioni atomiche di alto livello non è detto che lo siano anche a livello basso
>
>
>>[!success] [[mutex]]

