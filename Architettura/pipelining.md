Tecnice utili a migliorare le prestazioni basata sulla sovrapposizione dell'esecuzione di più istruzioni appartenenti ad un flusso di esecuzione sequenziale


Il lavoro svolto in una CPU pipeline per eseguire un'[[istruzioni|istruzione]] è diviso in passi, detti stadi di pipeline, che richiedono una frazione del tempo necessario al completamento, questi stadi sono sovrapponibili e formano le pipeline. Possiamo immaginarci il pipelining come una catenza di montaggio, che di fatto non migliora il tempo a eseguire una singola istruzione, però aumenta quante istruzioni eseguiamo in un'intervallo di tempo, cioè il [[throughput]] delle istruzioni.



>[!esempio]
>![[Pasted image 20221025183252.png]]


Il tempo necessario per far avanzare un'istruzione di uno stadio di pipeline è idealmente un ciclo di [[clock]] in modo sincrono, con una durata di 200ps, ossia la durata dello stadio più lento (A cui si devono adattare tutte le istruzioni). Grazie alla pipeline abbiamo un'accelerazione equivalente al numero di stadi, ossia 5 volte tanto rispetto ad un processore senza pipeline.

# Pipelining in [[RISC-V]]
RISC-V usa una pipeline a 5 stadi in quanto la load, che come abbiamo visto nel [[Processore|processore]] è la più lenta, ha bisogno di tutti e 5 gli stadi. Quindi abbiamo un **architettura pipeline a 5 stadi da 200 ps**
Notiamo che in realtà sul singolo ciclo perdiamo, la load che è la più lunga passa da 800ps a 1000ps (5 stadi da 200ps) tuttavia il troughput milgiora di 4 volte:
- in monociclo: 1 istruzione di load ogni 800ps
- in pipeline: 1 istruzione di load ogni 200ps

## Fasi di esecuzione delle istruzioni

vediamo di seguito l'esecuzione di alcune istruzioni:
### - Aritmetico logice `op rd, rs1, rs2`

Prelievo istruzione, incremento PC | Lettura rs1, rs2 | OP ALU (rs1 op rs2)|$\mspace{ 70mu }$ | scrittura in rd
--- | --- |--- | --- | ---

### - Load `ld rd, offset12(rs1)`

Prelievo istruzione, incremento PC | lettura registro rs1 | OP ALU (rs1 + off_ext) | prelievo M(rs1+off_ext) | Scrittura in rd
--- | --- | --- | --- | --- 
### - Store `sd rs2, offset12(rs1)`
Prelievo istruzione, incremento PC | lettura rs1, rs2 (sorgente) | OP ALU (rs1+off_ext) | Scrittura dato M(rs1+off_ext) | $\mspace{ 70mu }$|
--- | --- | --- | --- | ---

### - Salto condizionato `beq rs1, rs2, off12`
prelievo istruzione, incremento PC | lettura rs1, rs2 | OP ALU (rs1-rs2) & (PC + off_ext) | scrittura nel PC | $\mspace{ 70mu }$|
--- | --- | --- | --- | ---


Le fasi di esecuzione sono

1. (**IF**): Instruction Fetch, prelievo istruzione
2. (**ID**): Instruction Decode, decodifica istruzione e lettura registri
3. (**EX**): Execution, esecuzione
4. (**MEM**): Memory access, acesso alla memoria dati
5. (**WB**): Write back, riscrittura registri

Notiamo come abbiamo 5 fasi di esecuzione, ma alcune istruzioni ne usino solo 4, per questo gli spazi vuoti nelle istruzioni sopra.


## Fasi di esecuzione nel processore

Vogliamo scomporre il processori in 5 stadi di esecuzione, ognuno che corrisponde ad una fase, è necessario quindi introdurre i registri di pipeline che separano i diversi stadi essendo in esecuzione ad ogni ciclo 5 istruzioni diverse

>[!oss]- Registri di pipeline
>
>![[Pasted image 20221025193607.png]]
>
>![[Pasted image 20221025193739.png]]

Questi registri sono detti [[registri interstadio]] e propagano i dati necessari attraverso  gli stadi.


[[Conflitti]]

