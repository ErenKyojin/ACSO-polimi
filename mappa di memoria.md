La mappa di memoria di un processo in [[Memoria virtuale]] è una tabella rappresentata come

| VMA | start address | dim | R/W | P/S | M/A | mapping |
| --- | ------------- | --- | --- | --- | --- | ------- |
| C   | 000000400     | 2   | R   | P   | M   | <X, 0>        |

- **VMA** rappressenta le aree fondamentali in modo simbolico
- **Start address**
- **DIM**: rappresenta la dimensione in pagine dell'area
- **R/W**: read o write
- **P/S**: private o shared
- **M/A**: mapped or anonymous
- **Mapping**: <Nome file, offset in pagine>