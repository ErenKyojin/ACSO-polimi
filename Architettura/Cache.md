La [[memoria]] DRAM rallenta il [[Processore]] in quanto l'accesso ai dati impiega più tempo dell'esecuzione delle istruzioni, vogliamo migliorare l'architettura implementando una memoria che appaia più veloce ma con dimensioni uguali.
Questo attraverso il [[principio di località]], la soluzione a questo problema è una [[gerarchia di memoria]]


La minima quantità di informazioni in cui è quantizzata la cache è il [[blocco]]

## HIT / MISS

>[!success]
Se il dato richiesto dal processore è in uno dei blocchi presenti si dice che la richiesta ha avuto successo **(hit)**

>[!failure]
>Se il dato non è nel livello superiore si dice che la richiesta fallisce **(miss)**
>
> In caso di miss:
> - stallo del processore
> - richiesta del blocco contenente il dato alla memoria principale
> - copia del blocco in cache
> - ripetizione dell'accesso in cache (hit garantita)

## Entry
La cache è divisa in posizioni (o righe) dette entry e che contengono:

1. **Valid bit** che indica se l'entry ha o meno dati validi (all'accensione vengono tutti impostati a 0)
2. **Etichetta (o tag)** che contiene il valore che identifica l'[[memoria#Indirizzo di memoria|indirizzo di memoria]] corrispondente ai dati nella entry
3. **Dati** che contiene un copia dei dati (blocco o cache line)

 V | TAG | DATI
 --- | --- | ---



# Architettura della cache
>[!error]
Dato un indirizzo di un blocco nella memoria principale, qual è la sua posizione nella cache?
>
>>[!success]
>>Vogliamo sviluppare delle corrispondenze biunivoche che ci permettono di far corrispondere ad un [[memoria#Indirizzo di memoria|indirizzo di memoria]] di un blocco uno specifico indirizzo in cache di un altro blocco, possiamo farlo sviluppando diverse architetture


## - Cache a indirizzamento diretto
>[!esempio]
>Memoria: 32 blocchi
>Cache: 8 blocchi
>
>Dove possiamo mettere il blocco 12?
> $12  = 4\mod 8$

Quindi in cache a indirizzamento diretto possiamo inserire un blocco solo all'indirizzo uguale al modulo dell'indirizzo di memoria(M) rispetto alla dimensione della cache (C):

$$
M = I \mod C 
$$
### Indirizzamento
Dati N bit per l'indirizzo di memoria dobbiamo dividerlo in 4 campi:
 | Tag                 | Indice | Sp. parola | Sp. byte |
 | ------------------- | ------ | ---------- | -------- |
 | N - (M + K + B) bit | M bit  | K bit      | B bit    | 

- Lo spiazzamento del byte indica il byte da individuare nella parola selezionata 
	Se la memoria non è indirizzata al byte B = 0
- Lo spiazzamento (offset) della parola nel blocco indica la parola desiderata all'interno del blocco
	Se il blocco contiene una sola parola K = 0
- L'indice: indica l'indirizzo del blocco in Cache
- Etichetta (Tag): Si confronta con il campo etichetta del blocco di cache selezionato dall'indice

>[!esempio]
>- Indirizzo di memoria N = 32 bit
>- Dimensione cache = 4K Byte
>- Dimensione blocco = 1 parola $\implies$ K = 0
>- Dimensione Della parola = 32 bit = 4 Byte = $2^2$ Byte $\implies B = 2$ bit
>- Numero di blocchi = Dim cache / Dim blocco = 4K byte / 4 Byte = 1K blocchi = 2^10 blocchi $\implies 10$ bit
>- Tag = (32 - 10 - 0 - 2) bit = 20 bit


## - Cache completamente associativa
Il blocco può essere inserito ovunque nella cache, dobbiamo quindi esaminare ogni blocco della cache tramite tag, non esiste il campo indice e abbiamo solo tag e offset, ed il tag coincide con l'indirizzo

>[!esempio]
> - N = 32 bit
> - Dim cache = 256 Byte
> - Dim blocco = 128 bit = 16 Byte
> - Numero di blocchi = Dim cache / dim blocco = 16 blocchi
> - Tag = 32 - 2 - 2 = 28 bit

## - Cache set associativa a $n$ vie

>[!esempio] esempio a 2 vie
>Memoria: 32 blocchi
>Cache: 8 blocchi
>
> Dove possiamo mettere il blocco 12?
> $12 = 0 \mod 4$
>
>Ovunque nel set 0
>
>Quindi raggruppiamo a due a due tutti i blocchi in 4 set da due blocchi

Nella cache set associativa ad $n$ vie dividiamo la cache in insiemi di $n$ blocchi:

<center>
numero di blocchi = dim cache / dim blocco
</center>
<center>
numero di set = dim cache / (n * dim blocco)
</center>

Ogni blocco di memoria è un unico insieme della cache di indirizzo:
 $$\text{ind set = ind blocco$_{mem}$ $\mod{(\text{num set})}$}$$
 L'indirizzo è assolutamente analogo a quello della cache ad indirizzamento diretto, ed in effetti:
>[!oss]
>La cache set associativa ad $n$ vie è essenzialmente equivalente ad avere $n$ cache ad accesso diretto




>[!oss]
>All'aumentare dell'associatività diminuisce la percentuale di miss rate:
 >
 > | n | miss rate |
 > --- | --- |
 > 1 | 10.3 %
 > 2 | 8.6 %
 > 4 | 8.3 %
 > 8 | 8.1 %
 Ma anche il costo aumenta, andare oltre all'8 è superfluo, l'incremento di efficienza è minimo per un aumento consistente dei costi
 >
 > Inoltre all'aumentare dell'associatività diminuiscono i bit di indice e aumentano i bit di tag
 

### Politiche di miss
 
  