# Istruzioni di trasferimento
Istruzioni che si occupano del trasferimento dati tra [[memoria]] e [[registro]], in particolare:
1. Da memoria a registro - Load
2. Da registro a memoria - Store
3. Da registro a registro - Move

 Per trasferire parole doppie abbiamo:
 ```armasm
 ld ; load double (64 bit)
 sd ; store double (64 bit)
 ```
Inoltre abbiamo
- `lw/sw` per trasferire word (32 bit)
- `lh/sh` per trasferire half word (16 bit)
- `lb/sb` per trasferire byte (8 bit)



## istruzione Load
Load trasferisce una coppia della doppia parola contenuta in un indirizzo a 64 bit specifico di memoria, e lo inserisce in un registro della CPU, la memoria non viene modificata.

```asmarm
ld, rd, IND    ; rd <-- memoria[IND]
```

La CPU invia l'indirizzo della locazione desiderata  alla memoria e richiede un'operazione di lettura del contenuto della memoria.
	Le memoria effettua la lettura della doppia parola memorizzata nell'indirizzo e la invia alla CPU attraverso il registro rd