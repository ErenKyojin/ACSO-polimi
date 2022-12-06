Porta di lettura 1: l'indirizzo del [[registro]] da leggere è usato come segnale di controllo del [[MUX]] 32:1 della prima porta
Porta di lettura 2: l'indirizzo del registro da leggere è usato come segnale di controllo del [[MUX]] 32:1 della prima porta
![[Pasted image 20221017171518.png]]


Le due porte di lettura sono indipendenti come lo sono anche i due mux.


# Porte di lettura con [[buffer tri-state]]
Tutte i registri condividono la stessa linea di uscita, quindi vengono usate le linee di registro come linee di enable per il buffer della porta di lettura considerata
![[Pasted image 20221017173847.png]]

La scrittura avviene sul fronte di salita del ciclo, e quindi la lettura fornisce il valore scritto al ciclo precedente