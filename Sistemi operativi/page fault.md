Un'interrupt di page fault si verifica quando non si trova la pagina fisica corrispondente all'indirizzo virtuale, ed indica che la pagina è salvata su disco e li va ripresa.


## Gestione dei page fault

Quando la [[Memoria virtuale|MMU]] genera un page fault si attiva una routine detta PFH

- Se (NPV non appartiene alla memoria virtuale del processo) allora -> segmentetion fault
- Altrimenti se (NPV appartiene alla memoria virtuale del processo ma l'accesso non è protetto) allora -> segmentation fault
- Altrimenti se (l'accesso è leggittimo ma NPV non in memoria fisica) allora viene invocata la routine che carica in memoria fisica la pagina virtuale dal file di [[backing store]] (demand paging)


## Gestione dei page fault con COW

SE NPV non appartiene alla memoria virtuale del processo 
	ALLORA segmentation fault
ALTRIMENTI SE invece NPV è allocata in pagina PFx ma viola le protezioni
	SE si tratta di una violazione di accesso in scrittura a pagina con protezione di tipo R di una VMA scrivibile
		SE(PFx.ref_count > 1)
			ALLORA copia PFXin una pagina fisica privata PFz decrementando di ref_count PFx in page cache, assegnando NPV a PFz e scrivendo in PFz
		ALTRIMENTI abilita NPV in scrittura
	ALTRIMENTI il processo va in segmentation fault
ALTRIMENTI SE l'accesso è legittimo ma NPV non è allocata in memoria
	ALLORA invoca la routine che deve caricare in memoria la pagina virtuale NPV dal file

## Gestione completa del page fault handler

SE NPV non appartiene alla memoria virtuale del processo
	ALLORA processo abortito e segnalato segmentation fault
ALTRIMENTI SE NPV è allocata in una pagina fisica PFx ma viola le protezioni
	SE (gestisci come COW)
	ALTRIMENTI processo abortito e segnalato segmentation fault
ALTRIMENTI SE Accesso legittimo ma NPV non allocato in memoria
	SE la NPV è start address di una VMA con il flag di growsdown
		ALLORA aggiuni una nuova paggina viruale NPV-1 al'area virtuale che diventa la nuova start address della VMA


