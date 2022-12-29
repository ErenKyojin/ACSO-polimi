Negli esercizi sulla memoria viene semplificato di molto il sistema di gestione della memoria

# [[Mappa di memoria]]
La mappa di memoria viene viene semplificata come


| VMA | Star address | dim | R/W | P/S | M/A | mapping |
| --- | ------------ | --- | --- | --- | --- | ------- |
| C   | 000000400    | 2   | R   | P   | M   | <X,0>   |
| K   | 000000600    | 1   | R   | P   | M   | <X,2>   |
| P   | 7FFFFFFFC    | 3   | W   | P   | A   | <-1,0>  | 
