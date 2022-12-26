



# Spazio di indirizzamento virtuale di un processo
La [[Memoria virtuale]] di un processo linux non è un unico spazio di indirizzamento lineare indifferenziato, è diviso in [[aree di memoria virtuale]] o VMA indipendenti ed omogenee:

1. Codice
2. Dati statici
3. Dati dinamici (heap)
4. Memoria condivisa
5. Librerie dinamiche
6. Pila