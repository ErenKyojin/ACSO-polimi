# Istruzioni aritmetico logiche
solitamente 3 operandi:
- due registri sorgente
- un registro di elaborazione (risultato)
Formato di tipo R e ordine degli operanti fisso

# aritmetiche
```armasm
ADD rd, r1, r2 #rd = r1 + r2
SUB rd, r1, r2 #rd = r1 + r2
MUL 
DIV
REM ;resto

ADDU ;unsigned add
SUBU ;unsigned sub
MULU
DIVU
REMU ;rem

ADDI rd, rs1, Cost ;addizzione di costante, rappresentato su 12* bit
```
*Le costanti in assembly sono a 12 bit, tuttavia per le operazioni devono essere estesa di segno a 64 bit (essenzialmente aggiungendo 64-n bit di segno)

# logiche
```armasm
AND rd, Rs1, rs2
OR rd, Rs1, Rs2
XOR rd, RS1, Rs2

NOT rd, Rs1 ;Pseudo operazione
```

Per quanto ci riguarda lavoriamo solo con i numeri naturali, in realtà esiste un'altra [[Unità aritmetico logica|ALU]] che svolge i calcoli in formato IEEE 756, e che quindi copre i numeri reali, ma non ce ne occupiamo in questo corso
