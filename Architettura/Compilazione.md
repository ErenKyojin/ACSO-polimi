# compilazione

>[!esempio]
>Da C a simbolico
>
> Programma C
>```c
>typedef long long int LONG;
>LONG a;
>LONG b = 3;
>a = b+1
>```
>Che in assembly viene convertito in:
>```armasm
>A: .zero 8
>B: .dword 3
>
>la t0, B
>ld t1, 0(t0)
>addi t1, t1, 1
>la t0, A
>sd t1, 0(t0)
>```


[[esempi di conversione]]
