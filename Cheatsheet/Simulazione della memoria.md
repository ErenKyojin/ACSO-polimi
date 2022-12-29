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
La memoria fisica viene rappresentata con una tabella che contiene tutti gli indirizzi fisici (NPF), la pagina con NPF = 0 si


## [[Tabella delle pagine| page table]]


[[Thread]]


