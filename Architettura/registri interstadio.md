Sono dei registri tra i diversi stadi della [[pipelining|pipeline]], e ad ogni stadio abbiamo un registro di ingresso ed un registro di uscita con elementi funzionali per eseguire le operazioni dello stadio

```mermaid
graph LR
	A1[Registro 1] --> A2([Logica combinatoria]) --> A3[Registro 2]
```
>[!esempio] Load in pipeline
> #todo


>[!oss]
In ogni registro interstadio sono memorizzati dati relativi ad istruzioni diverse

Nel registro IF/ID è salvato il registro destinazione, vogliamo fare in modo di propagarlo anche agli altri registri (ID/EX, EX/MEM, MEM/WB) in quanto write back deve conoscere in quale registro salvare i dati, per questo motivo è necessario modificare la struttura del [[Processore]] aggiungendo un'uscita che attraversa tutti gli interstadi per comunicare il [[registro]] di destinazione.

>[!esempio] store in pipeline
#todo 


Un'altra cosa che dobbiamo propagare sono i segnali di controllo dell'[[unità di controllo]], a partire dallo stadio IF/ID