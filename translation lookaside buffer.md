Una memoria cache che tiiene traccia delle traduzioni NPV ed NPF utilizzate di recente per la [[memory mapping]]. Quindi contiene:
- Tag o etichetta: NPV
- Dati: NPF
- Valid bit: indica se la corrispondenza è valida
- Dirty bit: Indica se la pagina fisica è stata modificata
- Access bit: indica se la pagina è stata utilizzata di recente (Per la politica LRU)

#todo slide 32