
```armasm
.data
A: .word 1
B: .word 2
C: .word 3


.text
.globl MAIN
MAIN:
la t0, A
lw t1, 0(t0)
la t2, B
lw t3, 0(t2)
bne t1, t3, ELSE
la t2, C
lw t3, 0(t2)
bne t3, t2, ELSE

#Ogni etichetta ricarichiamo le variabili, non sappiamo come entriamo nell'etichetta
THEN:
la t0, A
lw t1, 0(t0)
addi t1, t1, 1
sw t1, 0(t0)
j ENDIF

ELSE:
la t0, B
lw t1, 0(t0)
addi t1, t1, 1
sw t1, 0(t0)

ENDIF:
li t0, 12
la t1, C
sw t0, 0(t1)
#exit
li a7, 10
ecall
```



# vettore

```armasm
.data
VETT: .word 1,2,3,4,5,6,7,8,9,10
MAX: .space 4
I: .space 4

.text
globl MAIN
MAIN:
la t0, VETT
lw t1, 0(t0)
la t2, MAX
sw t1, 0(t2)
la t0, I
sw zero, 0(t0)

LOOP:
#i < 10
la t0, I
lw t1, 0(t0)
li t2, 10
bge t1, t2, END_LOOP

#if vett[i] > max
la t0, VETT
la t1, I
lw t2, 0(t1)
slli t2, t2, 2
add t0, t0, t2
lw t1, 0(t0)
la t2, MAX
lw t3, MAX
lw t3, 0(t2)
ble t1, t3, END_IF
la t0, MAX
sw t1, 0(t0)

END_IF:
#i++
la t0, I
lw t1, 0(t0)
addi t1, t1, 1
sw t1, 0(t0)
j lOOP

END_LOOP:
li a7, 10
ecall

```
