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
>>>```