Negli esercizi sulla memoria viene semplificato di molto il sistema di gestione della memoria

## 1. [[Mappa di memoria]]
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

## 2. [[memoria]] fisica
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

A maiuscolo => REF = 1 ([[PFRA]]) altrimenti 0
>[!esempio] Esempio Qc0: prima pagina del codice del processo Q 
>

>[!important] Convenzioni
> - Viene allocata sempre la prima pagina fisica libera disponibile
> - Se una pagina virtuale è mappata su file viene indicato il file aggiungendo uno slash e la coppia file offset (esempio Pc1 / <X,1>)


## 3. [[Tabella delle pagine| page table]]

La page table del processo viene rappresentata come PT entries, rappresentate come
\<NPV : NPF protezione>

## 4. NPV dei registri PC e SP
Il NPV è attribuito ai registri PC e SP
- Ogni volta che viene acceduta una pagina di pila il suo NPV diventa NPV dello SP
- Ogni volta che viene acceduta una pagina di codice il suo NPV diventa il NPV corrente del PC




# Svolgimento esercizi

Prima di tutto, bisogna seguire processi logici diversi in base ad ogni evento:


## fork
P crea processo Q


1. Copiare tutte le pagine e porle in read only
2. La pagina in cima alla pila (indicata dallo stack pointer), in questo caso per [[Copy on write]] bisogna avere una pagina diversa per ogni processo, quindi il processo padre P è 


## mmap()
crea aree di memoria di tipo M 

## sbrk(n)
crea n pagine di heap (tipo D)


Pagine di pila P e dati dinamici D mappate sulla zero page in read (e poi eventualmente spostate con copy on write)

