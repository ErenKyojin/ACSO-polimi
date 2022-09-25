# istruzioni di scorrimento
Scorrimento logico dei bit a sinistra e a destra di una costante intera positiva $k$ compresa tra 1 e 63:
```armasm
slli rd, rs1, k ; rd <-- rs1 << k, shift left k bit, ossia moltiplica per 2^k 
slrd rd, rs1, k ; rd <-- rs1 >> k, shift right k bit, ossia moltiplica per k^{-2} bit
```

>[!esempio]
>```armasm
>slli  s0, s0, 2    ; shift left due bit
>```
>
>$s0$ iniziale: $0000\quad ...\quad 0000\quad0000\quad0000\quad0000\quad0011\quad1010$
>$s0$ finale:   $\ \ 0000\quad ... \quad 0000 \quad0000\quad0000\quad0000\quad1110\quad10\fbox{00}$

