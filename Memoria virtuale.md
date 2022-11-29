La [[memoria]] virtuale nasce per separare i concetti di 
- spazio di indirizzamento: ossia numero di parole indirizzabili, che dipende solamente dal numero di bit dell'indirizzo
- dimensione effettiva della memoria fisica: Numero di byte che costituiscono la memoria fisica $\leq$ spazio di indirizzamento
La memoria principale è detta memoria fisica ed i suoi indirizzi sono detti indirizzi fisici. La memoria virtuale ineve la CPU genera un indirizzo virtuale che viene tradotto da una combinazione di elementi hardware e software in un indirizzo fisico. Inoltre è presente un meccanismo che traduce indirizzi virtuali in indirizzi fisici. Questo meccanismo è detto [[memory mapping]], ed il più usato è la rilocazione dinamica tramite paginazione, dove l'unità più piccola è la [[pagina]].




![[Pasted image 20221129084453.png|500]]