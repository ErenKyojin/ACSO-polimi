Una memoria cache che tiiene traccia delle traduzioni NPV ed NPF utilizzate di recente per la [[memory mapping]]. Quindi contiene:
- Tag o etichetta: NPV
- Dati: NPF
- Valid bit: indica se la corrispondenza è valida
- Dirty bit: Indica se la pagina fisica è stata modificata
- Access bit: indica se la pagina è stata utilizzata di recente (Per la politica LRU)

#todo slide 32


Il TLB è rappresentato come una tabella in cui ogni entry è rappresentata dal formato
[[NPV]]: NPF -D: A:
Con i bit Dirty access che si comportano come nel modo reale in ogni [[Cache]]:
- A = 1 ad ogni accesso alla pagina e D = 1 ad ogni scrittura nella pagina
- Se un accesso non è presente nel TLB (TLB miss) carichiamo l'entry dal TLB
- La pagina iniziale della pila viene scritta, quindi D = 1

Non si verifica mai saturazione del TLB per ipotesi