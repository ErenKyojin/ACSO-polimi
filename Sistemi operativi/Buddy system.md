Linux si basa sul concetto di buddy system: divide la [[memoria]] fisica in blocchi di pagine contigue con dimensione potenza di 2 detta **ordine** del blocco.


>[!esempio]
Avendo un sistema con 64KB di memoria fisica e configurando la dimensione di ordina 0 a 4KB in questo caso
>- Allochiamo fino a 16 blocchi in ordine 0 oppure
>- Alocchiamo un singolo blocco di ordine 4, infatti: $2^4 * 4$ KB $64$ KB

