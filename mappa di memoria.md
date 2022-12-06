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
- **Mapping**: <Nome file, offset in pagine> ( <-1,0> se VMA anonima)



>[!esempio]
>
>| VMA | start address | dim | R/W | P/S | M/A | mapping |
| --- | ------------- | --- | --- | --- | --- | ------- |
| --- | ------------- | --- | --- | --- | --- | ------- |
| C   | 000000400     | 2   | R   | P   | M   | <X, 0>  |
| K   | 000000600     | 1   | R   | P   | M   | <X,2>   |
| S   | 000000601     | 1   | W   | P   | M   | <X,3>   |
| D   | 000000602     | 2   | W   | P   | A   | <-1,0>  |
| P   | 7FFFFFFFFC    | 3   | W   | P   | A   | <-1,0>  |
> 
>
>| 000000400 | Pc0 |
>| --------- | --- |
| 000000401 | Pc1 |
| --------- | --- |
| 000000600 | PkO |
| 000000601 | Ps0 |
| 000000602 | Pd0 |
| 000000603 | Pd1 |
|           |     |
| 7FFFFFFFC | Pp2 |
| 7FFFFFFFD | Pp1 |
| 7FFFFFFFE | Pp0 |


