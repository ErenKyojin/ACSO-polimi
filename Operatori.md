# Operatori

### OR
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 1

### Prodotto (AND)

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
!(A + B) = OR
