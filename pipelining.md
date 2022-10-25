Tecnice utili a migliorare le prestazioni basata sulla sovrapposizione dell'esecuzione di più istruzioni appartenenti ad un flusso di esecuzione sequenziale


Il lavoro svolto in una CPU pipeline per eseguire un'[[istruzioni|istruzione]] è diviso in passi, detti stadi di pipeline, che richiedono una frazione del tempo necessario al completamento, questi stadi sono sovrapponibili e formano le pipeline. Possiamo immaginarci il pipelining come una catenza di montaggio, che di fatto non migliora il tempo a eseguire una singola istruzione, però aumenta quante istruzioni eseguiamo in un'intervallo di tempo, cioè il [[throughput]] delle istruzioni.

```mermaid
graph 20, LR
	1a[IF] --> 1b[ID] --> 1c[EX] --> 1d[MEM]  --> 1e[WB]
	1e --> 2a --> 2b --> 2c --> 2d --> 2e 
```