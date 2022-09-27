# istruzioni di confronto
Istruzioni per il confronto di due variabili, ad esempio:

>[!esempio] verifica se `rs1 < rs2`
>```armasm
>slt rd, rs1, rs2  ; set on less than, assegna ad rd 1 se rs1 < rs2, altrimenti assegna 0
>```


### confronto tra variabile e costante

```armasm
slti rd, rs1, 8 ; set on less than
```

Prima estende in segno la costante `8` a 64 bit dai 12 di partenza, poi assegna a `rd` il valore 1 se `rs1 < 8`, altrimenti 0.

slt/slti eseguono confronti signed, per confronti unsigned sltu/sltui 


