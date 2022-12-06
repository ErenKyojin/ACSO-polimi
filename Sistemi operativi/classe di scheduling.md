Ogni politica ha un diversa classe di scheduling, le tre più importanti

nome | politica | priorità
--- | --- | ---
SCHED_FIFO | first in first out | massima
SCHED_RR | round robin | media
SCHED_NORMAL | completely fair scheduler | minima

Il [[sistema operativo]] gestisce le task secondo la politica della classe di appartenenza:
- FIFO task eseguite per intero non appena selezionati
- RR task eseguiti a turno in modo strettamente circolare
- NORMAL task gestiti con preemption e priorità dinamica in base al tempo virtuale

## soft real time

Le classi SCHED_FIFO e SCHED_RR sono usate per task soft realtime, sono basate sul concetto di priorità statica, ossia entrambe sono assegnate alla creazione e non più variate con valori $\in [1,99]$



# SCHED_FIFO
Classe di scheduling non preemptive, quando un task entra in esecuzione non ha limiti di tempo, continua fino a quando
- non entra in attesa
- fino alla terminazione naturake


# SCHED_RR
#todo

# SCHEDULING NORMAL
Completely fair scheduler (CFS) ha il seguente obiettivo per ogni CPU:

>[!oss]
>Dati $N \geq 1$ task tutti assegnati ad una CPU di potenza 1 dedicare a ciascun task una CPU virtuale di potenza $1 / N$, ovviamente idealmente non è realizzabile con un numero di CPU $< N \implies$ assegnare un opportuno quanto di tempo in base all'evoluzione della task. Se la CPU è multi core ad ogni CPU ha la propria [[runqueue]]


Ha come obiettivi
1. determinare la durata del quanto di tempo
2. assegnare un peso a ciascun task
3. tornare rapidamente in esecuzione quando un processo in attesa viene risvegliato.


>[!oss]
>è essenzialmente un round robin con in aggiunta il tempo virtuale per l'evoluzione di ogni task

## Durata del quanto
Ad ogni task si assegna un peso `t.LOAD` iniziale che quantifica l'importanza della task

Il numero di task nella runqueue ad ogni istante è denotato con NRT $\geq 1$ e la runqueue comprende i task pronti ed il task corrente.

NRT = task pronti + 1 (task curr)

Ad ogni task si assegna un quanto di tempo `t.Q` di durata
$$
Q = \frac{PER}{NRT}
$$
Con PER periodo di scheduling.

Tuttavia con questa formula non stiamo considerando il **PESO** delle task (che in questo caso è = 1 per ogni task), se consideriamo il peso abbiamo:
t.LOAD peso del task t
 $$
RQL = \sum t.LOAD
$$
$$t.LC = t.LOAD / RLQ$$
t.load peso del task
rqload peso di tutte le task nella runqueue
t.LC rapporto tra il pesto del task t rispetto alla somma dei pesi di tutti i task

$$
T.q = PER \times t.LC
$$
## Gestione della runqueue
i Task pronti vengono mantenuti in una coda ordinata chiamata RB, e lo scheduler ha le seguenti regole:
1. il task in testa a **RB** viene estratto e diventa **CURR**
2. **CURR** eseguito fino a quando scade **Q**
3. **CURR** sospeso e reinserito in fondo a **RB**
4. Si torna al passo 1


I task sono eseguiti a turno per la durata di un quanto Q = PER / NRT




