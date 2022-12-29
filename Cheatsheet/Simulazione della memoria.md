Negli esercizi sulla memoria viene semplificato di molto il sistema di gestione della memoria

## [[Mappa di memoria]]
La mappa di memoria (accessibile su linux col comando `cat /proc/[PROCESS PID]/maps`)viene viene semplificata come

| VMA | Start address | dim | R/W | P/S | M/A | mapping |
| --- | ------------ | --- | --- | --- | --- | ------- |
| C   | 000000400    | 2   | R   | P   | M   | <X,0>   |
| K   | 000000600    | 1   | R   | P   | M   | <X,2>   |
| P   | 7FFFFFFFC    | 3   | W   | P   | A   | <-1,0>  | 


VMA: [[aree di memoria virtuale]] in cui è indicato il tipo
Start address: Indirizzo della prima pagina dell'area di memoria
Dim: dimensione dell'area di memoria
R/W: permessi di read write
P/S: area privata o condivisa
M/A: area mappata su file o anonima
mapping: file su cui è mappata e offsett nella forma <FILE, OFF>

## [[memoria]] fisica
La memoria fisica viene rappresentata con una tabella che contiene tutti gli indirizzi fisici (NPF), la pagina con NPF = 0 è la zero page e si indica con \<ZP>

Per rappresentare gli indirizzi virtuali NPV che riempiono la memoria fisica usiamo invece la notazione `PAn` con:
- `P` che specifica il processo
- `A` che specifica un tipo di area virtuale
	- **C** codice eseguibile
	- **K** costanti
	- **S** dati statici
	- **D** dati dinamici
	- **M** memoria mappata
	- **T** pila di un thread
	- **P** pila di main
- `n` il numero della pagina

>[!esempio] Esempio Qc0: prima pagina del codice del processo Q 
>

>[!important] Convenzioni
> - Viene allocata sempre la prima pagina fisica libera disponibile
> - Se una pagina virtuale è mappata su file viene indicato il file aggiungendo uno slash e la coppia file offset (esempio Pc1 / <X,1>)



## [[Tabella delle pagine| page table]]





