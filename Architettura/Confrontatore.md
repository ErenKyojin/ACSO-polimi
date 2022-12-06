---
Alias: comparatore
---
# Confrontatore o comparatore

Ha due gruppi di ingressi, A e B, e tre uscite: uguaglianza, minoranza e maggioranza,
Confronta $A$ E $B$ e attiva l'uscita corrispondente.

>[!esempio] Confrontatore a 4 ingressi (2A e 2B)
>
>A0 | A1 | B0 | B1 | A < B | A = B | A > B
>--- | --- | --- | --- | --- |--- |---
>0 | 0 | 0 | 0 | 0 | 1 | 0
>0 | 0 | 0 | 1 | 1 | 0 | 0
>0 | 0 | 1 | 0 | 1 | 0 | 0
>0 | 0 | 1 | 1 | 1 | 0 | 0
>0 | 1 | 0 | 0 | 0 | 0 | 1
>0 | 1 | 0 | 1 | 0 | 1 | 0
>0 | 1 | 1 | 0 | 1 | 0 |0
>0 | 1 | 1 | 1 | 1 | 0 | 0
>1 | 0 | 0 | 0 | 0 |  0 | 1
>1 | 0 | 0 | 1 | 0 | 0 | 1
>1 | 0 | 1 | 0 | 0 | 1 | 0
>1 | 0 | 1 | 1 | 1 | 0 | 1
>1 | 1 | 0 | 0 | 0 | 0 | 1
>1 | 1 | 0 | 1 | 0 | 0 | 1
>1 | 1 | 1 | 0 | 0 | 0 | 1
>1 | 1 | 1 | 1 | 0 | 1 | 0
