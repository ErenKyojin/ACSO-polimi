# Variabili
- Globali, allocati in memoria a inidirizzi 
- Locali, contenuti nei registri o nella stack
- Dinamiche: contenute in memoria


Le variabili globali sono allocate a partire dall'indirizzo di [[memoria]] 0x0000 0000 1000 0000

 >[!esempio]
 >```armasm
 >A: .dword ;a: indirizzo 0x0000 0000 1000 0000
 >B: .dword ;b: indirizzo 0x0000 0000 1000 0008
>```
>Infatti tra una double word e l'altra ci sono 8 Byte di distanza

>[!esempio]
>>[!multi column]
>>>[!c]
>>>```c
>>>long b,c;
>>>long A[20];
>>>```
>>
>>>[!assembly]
>>>```armasm
>>>B: .dword ;indirizzo 100
>>>C: .dword ;indirizzo 108
>>>A: .zero 160 ;indirizzo base 200
>>>A[0]: 200
>>>A[1]: 208 ;200 + 8*1
>>>A[19]: 352 ;200 + 8*19
>>>```



## Allineamento

Variabili poste in indirizzi specifici in base al tipo

VAR | ALIGN | Commento
--- | --- | ---
Byte | 0,1,2,3,4 | Possiamo usare qualsiasi indirizzo
HW | 0,2,4,6 | Indirizzi pari
W | 0, 4, 8, 12| indirizzi multipli di 4
DW | 0, 8, 16, 24| indirizzi multipli di 8

Esistono anche delle istruzioni di allineamento per casi specifici



## Dichiarazione
Si dichiarano le variabili tramite le [[Direttive]] di compilazione, sotto la tabella con la maggior parte della dichiarazione dei tipi:

>[!abstract]
>>[!multi-column]
>>>[!c]
>>>```c
>>>//LONG 64 bit
>>>char c = 'a';
>>>short int h;
>>>int i = 1;
>>>LONG d = 2;
>>>LONG *p1 = NULL;
>>>char *p2
>>>LONG vet[10]
>>>char str[10]
>>>```
>>
>>>[!assembly]
>>>```armasm
>>>.data
>>>C: .byte 65
>>>H: half
>>>I: .word 1
>>>D: .dword 2
>>>P1: .dword 0
>>>p2: .dword
>>>VET: .zero 80
>>>STR: .zero 10
>>>```

>[!esempio]
>>[!multi-column]
>>
>>>[!c]
>>>```c
>>>int a;
>>>a = 1;
>>>```
>>
>>>[!assembly]
>>>```armasm
>>>A: .word
>>>li t0, 1
>>>la t1, A
>>>sw t0, (t1)
>>>```
>
>