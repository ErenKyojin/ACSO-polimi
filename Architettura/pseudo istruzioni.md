# Pseudo istruzioni
Le pseudo istruzioni sono così dette in quanto sono in realtà derivate da altre istruzioni puù semplici, tanto che dall'[[assembler]] stesso vengono convertite nelle istruzioni equivalenti.
Tra le pseudo istruzioni abbiamo:

- Move
```armasm
mv rd, rs1  ===> addi rd, rs1, x0 ; x0 = 0-
```
- Nop
```armasm
nop ===> addi zero, zero, 0 ; operazione nulla, sarà utile in futuro?
```
- Not bit a bit
```armasm
not rd, rs1 ===> xori rd, rs1, -1 ; questo deriva dal fatto che -1_{10} = 11111..11_{2}
```
- Negazione aritmetica
```armasm
neg rd, rs1 ===> sub rd, x0, rs1 ; rd <-- -rs1
```
