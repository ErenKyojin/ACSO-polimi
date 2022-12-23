Questa memoria [[cache]] associativa contiene le righe della [[Tabella delle pagine]] riferite agli accessi più recenti, oltre al [[PID]] del processo a cui la pagina fa riferimento.

La tabella è quindi organizzata come:

| PID | NPV | NPF |
| --- | --- | --- |
|     |     |     |

Tiene traccia delle traduzioni NPV ed NPF utilizzate di recente per la [[memory mapping]]. Quindi contiene:
- Tag o etichetta: NPV
- Dati: NPF
- Valid bit: indica se la corrispondenza è valida
- Dirty bit: Indica se la pagina fisica è stata modificata
- Access bit: indica se la pagina è stata utilizzata di recente (Per la politica LRU)

#todo slide 32


>[!oss]
>Essendo il TLB una cache, se si effettua l'accesso ad un elemento non in memoria si genera un **TLB miss** che richiede di accede alla tabella delle pagine per prendere l'elemento corretto, rallentando il sistema. 
>Per ridurre le probabilità di un miss la dimensione del TLB per processo deve essere almeno uguale al numero di pagine R residenti in memoria del processo

## Accesso al TLB
Quando un processo deve traddure un NPV accede al TLB che:
- Se ha un elemento della tabella corrispondente all'NPV e al PID del processo(**TLB HIT**):
	- access bit = 1 e, se si tratta di una scrittura, anche access bit = 1

- Se invece non esiste un elemento corrispondente si hanno due casi (**TLB MISS**)
	1. **PAGE FAULT**, (valid bit = 0) se la pagina non è in memoria si aspetta che venga caricata da disco
	2. **TRUE TLB MISS**, (valid bit = 1) se la pagina è in memoria e quindi la pagina viene caricata dalla tabella



Il TLB è rappresentato come una tabella in cui ogni entry è rappresentata dal formato
[[NPV]]: NPF -D: A:
Con i bit Dirty access che si comportano come nel modo reale in ogni [[Cache]]:
- A = 1 ad ogni accesso alla pagina e D = 1 ad ogni scrittura nella pagina
- Se un accesso non è presente nel TLB (TLB miss) carichiamo l'entry dal TLB
- La pagina iniziale della pila viene scritta, quindi D = 1

Non si verifica mai saturazione del TLB per ipotesi.



