Lista che contiene i puntatori ai descrittori dei [[processo|processi]] in attesa di un certo evento:
- In una waitqueue vengono inseriti i descrittori dei processi posti in attesa di uno stesso evento
- L'indirizzo della waitqueue è l'identificatore dell'evento
- Una nuova waitqueue viene creata in modo dinamico ogni volta che un processo viene messo in attesa


creazione statica:  `DECLARE_WAIT_QUEUE_HEAD nome_coda`
ed ogni `wait_queue_head_t` può avere zero o più elementi accodati `wait_queue_t` tipicamente solo un elemento per coda.


>[!important]
Tutti i processi nella stessa waitqueue sono in attesa dello stesso evento, ed i processi in una waitqueue saranno risvegliati da una wake up e spostato nella [[runqueue]]
