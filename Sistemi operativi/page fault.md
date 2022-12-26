Un'interrupt di page fault si verifica quando non si trova la pagina fisica corrispondente all'indirizzo virtuale, ed indica che la pagina è salvata su disco e li va ripresa.


## Gestione dei page fault

Quando la [[Memoria virtuale|MMU]] genera un page fault si attiva una routine detta PFH

- Se (NPV non appartiene alla memoria virtuale del processo) allora -> segmentetion fault
- Altrimenti se (NPV appartiene alla memoria virtuale del processo ma l'accesso non è protetto) allora -> segmentation fault
- Altrimenti se (l'accesso è leggittimo ma NPV non in memoria fisica) allora viene invocata la routine che carica in memoria fisica la pagina virtuale dal file di backing store (demand paging)


