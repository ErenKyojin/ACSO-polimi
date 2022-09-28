# Operatori

### [[OR]]
![[Pasted image 20220928093958.png|200]]

0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 1

Scritta come tabella di verità:
A | B | out
--- | --- | ---
0 | 0 | 0
0 | 1 | 1
1 | 0 | 1
1 | 1 | 1

### Prodotto ([[AND]])
![[Pasted image 20220928094015.png|200]]

0 0 = 0
0 1 = 0
1 0 = 0
1 1 = 1

### Negazione
!1 = 0
!0 = 1

Grazie a questi tre operatori logici possiamo costruire qualsiasi [[funzione logica]]

# Proprietà
Proprietà | AND | OR
--- | --- | ---
identità | 1 x A =A | A + 0 = A
elemento nullo | 0 x A = 0 | 1 + A = 1
Idempotenza | A x A = A | A + A = A
Inverso | A x !A = 0 | A + !A = 1
Commutativa | A x B = B x A | A + B = B + A
Associativa | (A x B) x C = A x (B x C) | (A + B) + C = A + (B + C)
Distributiva | A x ( B + C) = (A x B) + (A x C) | A + (B x C) = (A + B) x (A + C)
Assorbimento | A x ( A + B) = A | A + A B = A
[[De morgan]] | !(A x B) = !A + !B | !(A+B) = !A x !B

Notare che de morgan ci permette di fare una conversione tra AND (o NAND) e OR (o NOR)

!(A x B) = NAND
!(A + B) = NOR


### NOR
![[Pasted image 20220928094159.png|200]]
!or


### XOR
XOR = !AB + A!B

Riconosce la diversità => 1 <==> A != B
![[Pasted image 20220928094301.png|200]]


### XNOR
AB + !A!B
Riconosce l'identità => 1 <==> A == B
![[Pasted image 20220928094431.png]]


>[!oss]
>Lo XNOR è equivalente a questo circuto
>![[Pasted image 20220928094757.png]]

