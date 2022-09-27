# Sottoprogrammi

### Chiamante (caller)
- Predispone i parametri da passare tramite i registri a2-a7
- Trasferisce il controllo al sotto programma tramite jump and link `jal`


### Chiamato (callee)
- Allocazione dell'area di attivazione su stack
- esecuzione
- Memorizza il risultato in a0/a1
- Restituisce tramite jr ra, ret


>[!esempio]
>
>#### chiamata:
>```armasm
>d
>```