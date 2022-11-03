Il blocco (o cache line) è la minima quantità di informazioni in cui è quantizzata la [[Cache]], per sfruttare la [[principio di località#Località spaziale|località spaziale]] il blocco di cache è un multiplo della word di [[memoria]]:


 | **Blocco:** | word 3 | word 2 | word1 | word 0
--- | --- | ---  | --- | ---
*off* | 11 | 10 | 01 | 00

Con off spiazzamento della parola rispetto al blocco

Quindi il **Numero di blocchi in cache** $n$ si traduce come: 
$$n = \frac{\text{dim cache}}{\text{dim blocco}}$$
