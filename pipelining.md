Tecnice utili a migliorare le prestazioni basata sulla sovrapposizione dell'esecuzione di più istruzioni appartenenti ad un flusso di esecuzione sequenziale


Il lavoro svolto in una CPU pipeline per eseguire un'[[istruzioni|istruzione]] è diviso in passi, detti stadi di pipeline, che richiedono una frazione del tempo necessario al completamento, questi stadi sono sovrapponibili e formano le pipeline. Possiamo immaginarci il pipelining come una catenza di montaggio, che di fatto non migliora il tempo a eseguire una singola istruzione, però aumenta quante istruzioni eseguiamo in un'intervallo di tempo, cioè il [[throughput]] delle istruzioni.



>[!esempio]
>![[Pasted image 20221025183252.png]]


Il tempo necessario per far avanzare un'istruzione di uno stadio di pipeline è idealmente un ciclo di [[clock]] in modo sincrono, con una durata di 200ps, ossia la durata dello stadio più lento (A cui si devono adattare tutte le istruzioni). Grazie alla pipeline abbiamo un'accelerazione equivalente al numero di stadi, ossia 5 volte tanto rispetto ad un processore senza pipeline.

# Pipelining in [[RISC-V]]
RISC-V usa una pipeline a 5 stadi in quanto la load, che come abbiamo visto nel [[Processore|processore]] è la più lenta, ha bisogno di tutti e 5 gli stadi. Quindi abbiamo un **architettura pipeline a 5 stadi da 200 ps**
