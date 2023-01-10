
# Blocco cache
Il blocco (o cache line) è la minima quantità di informazioni in cui è quantizzata la [[Cache]], per sfruttare la [[principio di località#Località spaziale|località spaziale]] il blocco di cache è un multiplo della word di [[memoria]]:


 | **Blocco:** | word 3 | word 2 | word1 | word 0
--- | --- | ---  | --- | ---
*off* | 11 | 10 | 01 | 00

Con off spiazzamento della parola rispetto al blocco

Quindi il **Numero di blocchi in cache** $n$ si traduce come: 
$$n = \frac{\text{dim cache}}{\text{dim blocco}}$$
# Blocchi del [[volumi|volume]]
Il blocco è 'unita di informazione trasferita con un solo accesso al disco, multiplo del settore, viene scritto o lezzot in una zona di memoria centrale di pari dimensione (detta buffer, gestita dal gestore del buffer), quando il file system richiede la lettura di un blocco interagisce con il gestore del buffer che se necessario interagisce col disk driver




# Blocchi logici
Il file è visto dal [[Sistemi operativi/File System]] come una sequenza di blocchi logici numerati a partire dal blocco 0, le operazioni sui file fanno riferimento.

>[!esempio]
>Ricerca del byte 520:
>- Blocco = $floor(\dfrac{520}{512}) = 1 \implies$ blocco 1
>- Offset: 520 % 512 = 8 $\implies$ offset di 8 byte
>
>Quindi il byte cercato si trova all'ottavo byte del blocco uno.
