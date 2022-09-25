# Memoria
Memoria indirizzabile al singolo byte ed è divisa in parole:
 - Una parola $32$ bit contiene $4$ byte
 - Una parola doppia $64$ bit contiene $8$ byte

Gli indirizzi di memoria sono a 64 bit, espresso con indirizzamento a byte, e lo spazio di indirizzamento è di 16 exabyte ($2^{64}$ Byte).
Visto che le istruzioni occupano 32 bit hanno indirizzi allineati alla parola, multipli di 4 byte.

### Come assegnamo gli indirizzi ai byte?

>[!def] #### big endian
>
>...|...|...|...|indirizzo
>---|-|-|-|-|
>0|1|2|3|0
>4|5|6|7|4
>...|...|...|...|8
>Alla parola viene assegnato l'indirizzo del byte più significativo
>
0|1|2|3
-|-|-|-
0000 0000|0000 0000| 0000 0000 | 0000 0110




>[!def] #### little endian
>
>|...|...|...|...|indirizzo
>---|---|---|---|---
>3|2|1|0|0
>7|6|5|4|4
>...|...|...|...|8
>Alla parola viene assegnato l'indirizzo del byte meno significativo
>
>3|2|1|0
>-|-|-|-
>0000 0000|0000 0000| 0000 0000 | 0000 0110

