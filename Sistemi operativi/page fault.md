Un'interrupt di page fault si verifica quando non si trova la pagina fisica corrispondente all'indirizzo virtuale, ed indica che la pagina è salvata su disco e li va ripresa.


## Gestione dei page fault

Quando la [[Memoria virtuale|MMU]] genera un page fault si attiva una routine detta PFH

- Se (NPV non appartiene alla memoria virtuale del processo) allora -> segmentetion fault
- Altrimenti se (NPV appartiene alla memoria virtuale del processo ma l'accesso non è protetto) allora -> segmentation fault
- Altrimenti se (l'accesso è leggittimo ma NPV non in memoria fisica) allora viene invocata la routine che carica in memoria fisica la pagina virtuale dal file di backing store (demand paging)


## Gestione dei page fault con COW

SE NPV non appartiene alla memoria virtuale del processo 
	ALLORA segmentation fault
SE invece NPV è allocata in pagina PFx ma viola le protezioni
	SE si tratta di una violazione di accesso in scrittura a pagina con protezione di tipo R di una VMA scrivibile
		SE(PFx.ref_count > 1)
			ALLORA copia PFXin una pagina fisica privata PFz decrementando di ref_count PFx in page cache, assegnando NPV a PFz e scrivendo in PFz
		ALTRIMENTI abilita NPV in scrittura
	ALTRIMENTI 