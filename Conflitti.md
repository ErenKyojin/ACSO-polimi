
Nonostante l'efficienza della [[pipelining|pipeline]] l'esecuzione in parallelo di più istruzioni può portare a problemi di tipo:

- **Strutturale**: un'[[istruzioni|istruzione]] prova ad accedere ad una risorsa già in uso da un'istruzione precedente
- **Sui dati**: un'istruzione usa un risultato di un'istruzione precedente non ancora elaborato (ossia ancora in pipeline)
- **Sul controllo**: Prendere una decisione sulla prossima istruzione da eseguire prima di valutare la condizione

# Conflitti strutturali

Questo problema in [[RISC-V]] non esiste, in primis la [[memoria]] istruzioni è separata dalla memoria dati, inoltre il banco dei registri è usato nello stesso clock sia in scrittura che in lettura con la temporizzazione. Non c'è mai una sovrapposizione delle risorse

# Conflitti dati (o data hazard)

Se le istruzioni nella pipeline hanno dipendenze sui dati possono nascere problemi di conflitto sui dati.

>[!esempio]
>Vediamo questo esempio dove abbiamo più dati che dipendono dal risultato nel registro $x2$
>
>```armasm
>sub x2, x1, x3
>and x12, x2, x5
>or x13, $6, x2
>add x14, x2, x2
>sw x15, 100(x2)
>```
>
> #todo grafico
> La seconda istruzione prova ad accedere a x2 quando la sub è ancora in fase di EX
> La terza istruzione prova ad accedere a x2 quando la sub è ancora in fase di MEM
> La quarta avviene in contemporanea col write back di x2, quindi ha il valore corretto
> La quinta avviene dopo la fase di write back


## Soluzione

Per questo problema possiamo usare 4 diverse soluzioni:
#### + Tecniche in static time:
- Inserimento di istruzioni [[pseudo istruzioni|no operation]] (NOP)
- Scheduling delle istruzioni in modo da cambiare l'ordine delle istruzioni mantenendo invariato il risultato ma evitando che possano avvenire conflitti

#### + Tecniche in runtime
- Inserimento di bolle o stabili nella pipeline
- Propagazione dei dati in avanti (forwarding o bypassing)



### inserimento NOP

Soluzione semplice ma poco efficiente, tornando all'esempio di prima



>[!multi-column]
>
>>[!Error] collisioni
>>
>>```armasm
>>sub x2, x1, x3
>>and x12, x2, x5
>>or x13, $6, x2
>>add x14, x2, x2
>>sw x15, 100(x2)
>>```
>
>>[!success] nessuna collisione
>>```armasm
>>sub x2, x1, x3
>>nop
>>nop
>>and x12, x2, x5
>>or x13, $6, x2
>>add x14, x2, x2
>>sw x15, 100(x2)
>>```

L'aggiungere NOP è semplice quanto inefficace, essenzialmente sprechiamo 2 cicli di clock in pipeline


### Scheduling

Piuttosto che sprecare cicli di clock con istruzioni nop utilizziamo quando possibile il rescheduling delle istruzioni:

>[!multi-column]
>
>>[!error] collisioni
>>
>>```armasm
>>sub x2, x1, x3
>>and x12, x2, x5
>>or x13, $6, x2
>>add x14, x2, x2
>>sw x15, 100(x2)
>>add x4, x10, x11 ; A
>>and x7, x8, x9 ; B
>>```
>
>>[!success] 
>>
>>```armasm
>>sub x2, x1, x3
>>add x4, x10, x11 ; A
>>and x7, x8, x9 ; B
>>and x12, x2, x5 
>>or x13, $6, x2
>>add x14, x2, x2
>>sw x15, 100(x2)
>>```

### Bolle o Stalli
Se vogliamo invece intervenire a livello di runtime possiamo inserire stalli nella pipeline, blocchiamo quindi il flusso fino a quando non c'è una risoluzione del conflitto, di fatto è equivalente a inserire due istruzioni nop.
Per implementarlo a livello hardware dobbiamo:
1. conservare per due cicli di clock i valori nel registro IF/ID, ossia il [[program counter]] e l'[[istruzioni|istruzione]] 
2. fare in modo che nell'intestazione ID/EX tutti i valori di ingresso siano 0 così da bloccare l'esecuzione


### Forwarding
Sistema in runtime più efficiente, osserviamo il caso esempio in cui abbiamo due [[istruzioni#Formato R]] di seguito e dipendenti:

>[!esempio]
>Consideriamo le due istruzioni:
>```armasm
>add s0, t0, t1
>sub t2, s0, t3
>```
>Fino ad ora abbiamo dato per scontato che il valore calcolato alla prima istruzione fosse accessibile in s0 dopo la fase di write back, ma in realtà già a partire dall'uscita dell'ALU, ossia l'uscita del [[registri interstadio|registro interstadio]] EX, il valore è già disponibile. Ossia al termine della fase ID dell'istruzione successiva. Aggiungiamo quindi un percorso EX/EX che porta il risultato salvato in EX/MEM all'ingresso dello ALU nello stadio EX

Quindi propaghiamo in avanti i dati nei registri interstadio prima che si arrivi alla fase di write back, ossia alla scrittura del dato nel [[Register file]].
La propagazione in avanti avviene solo in base allo stato del segnale RegWrite nell' interstadio che deve occuparsi della propagazione (Quindi a partire da EX/MEM) per le istruzioni R e load.

Grazie al forwarding è possibile evitare l'utilizzo di stalli o quantomeno ridurne il numero anche in caso di conflitto. Tuttavia bisogna introdurre un nuovo [[MUX]] all'ingresso dell'ALU per ogni registro interstadio (ossia ID/EX, EX/MEM, MEM/WB) ed avere altrettanti segnali di controllo.


## Rilevamento dei conflitti
Il rilevamento avviene durante la fase EX, se c'è richiesta di un registro che non è ancora stato salvato da un'istruzione precedente, per farlo devono verificarsi queste condizioni:
 
- **Conflitto in EX**:
	  EX/MEM.registroRd = ID/EX.registroRs1 || EX/MEM.registroRD = ID/EX.registroRs2
	  Ed in questo caso viene attivato il percorso EX/EX
- **Conflitto in MEM**: 
	 MEM/WB.registroRd = ID/EX.registroRs1 || MEM/WB.registroRD = ID/EX.registroRs2	
	 Ed in questo caso viene attivato il percorso MEM/EX
	

A occuparsi di questi controlli è l'[[unità di propagazione]] che è contenuta nella fase EX


# Conflitti di controllo

Questi conflitti vengono dalle istruzioni di salto condizionato: `beq rs1, rs2, offset12`

Prelievo istruzione, incremento PC | Lettura rs1, rs2 | OP ALU e PC + off | scrittura nel PC | $\qquad$ |
--- | --- | --- | --- |---


La pipeline per andare avanti richiede che venga prelevata un'istruzione ad ogni ciclo di clock per iniziare ad eseguirla, ma non possiamo sapere quale sarà la prossima istruzione fino a quando il salto condizionato non è presa fino allo stadio MEM.

La condizione e l'indirizzo di destinazione del salto vengono calcolati nello stadio EX, la logica di controllo del salto nello stadio MEM, e viene aggiornato il [[program counter]] con l'indirizzo di destinazione del salto o PC + 4 in base al risultato dell'ALU sul fronte di salita del clock di MEM/WB, c'è quindi un ritardo di 3 cicli di [[clock]].

## Soluzioni

### Standard
Con la pipeline attuale abbiamo due opzioni:
* ####  via software:
	3 NOP
* #### via hardware:
	3 stalli di stadio IF

>[!esempio]-
>![[Pasted image 20221027142619.png]]


### Predizione
Oppure implementiamo la **predizione**. Si predice che il salto non venga eseguito e si procede con il prelievo della prossima istruzione (untaken branch) e si procede con il prelievo della prossima istruzione sequenziale, arrivati al caso MEM ci sono due possibili strade:

>[!multi-column]
>
>>[!success] Predizione corretta (untaken branch)
>>L'esecuzione già svolta era corretta, non sprechiamo nessun ciclo di clock
>>
>
>>[!failure] Predizione scorretta (taken branch)
>>Bisognava eseguire il salto, si procede quindi con il flushing delle 3 istruzioni già in pipeline (che altrimenti verrebbero eseguite)


### Pipeline ottimizzata
Aggiungiamo delle nuove funzioni alla pipeline che possono accelerare le decisioni, vogliamo in particolare:
- **Accelerare la decisione del salto nella pipeline**
	Passiamo dal prenderla allo stadio MEM allo stadio ID, ossia vogliamo anticipare:
	  - Il calcolo dell'indirizzo di destinazione
	  - La valutazione del confronto dei registri

#### Anticipazione calcolo indirizzo
Il PC e l'offset sono disponibili già dal primo interstadio IF/ID, quindi possiamo anticipare l'addizione allo stadio ID (prima era nel successivo stadio EX).

#### Anticipazione condizione sul salto
Necessario confrontare il contenuto dei registri letto nello stadio ID attraverso uno [[XNOR]] bit a bit nello stadio ID

>[!oss] Pipeline ottimizzata
>![[Pasted image 20221027153545.png]]


La soluzione più efficiente è però avere un misto delle ultime due, pipeline ottimizzata e predizione, infatti con la pipeline ottimizzata comunque perderemmo un ciclo di clock, mettiamo l'untaken branch nella fase IF così da caricare già un'eventuale prossima istruzione per poi scartarla.