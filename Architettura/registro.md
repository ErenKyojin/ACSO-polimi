# Registro
```mermaid
flowchart LR
	A[Variabili] <======> B[Registri]
```
I registri sono gli elementi di memoria della CPU

>[!esempio] Registri [[RISC-V]]
>32 registri generali in parola dobbia (64 bit) da x0 a x31, codificati in 5 bit
>
>Indirizzo | Registro (64 bit)
>--- | ---
>00000| Registro x0
>00001| Registro x1
>00002| Registro x2
>$$\vdots$$|$$\vdots$$
>11111| Registro x31


## Registri RISC-V
Registro | nome ABI | Utilizzo
--- | ---| ---
**x0** | **zero** | costante 0 - immodificabile
**x1** | **ra**| return address - indirizzo di rientro da funzione
**x2** | **sp** | stack pointer - punta in cima alla pila
**x3** | **gp** | global pointer - puntatore all'area dati globale
**x4** | **tp** | thread pointer - puntatore a thread
**x5 - x7** | **t0 - t2** | valori temporanei (indirizzi, variabili e calcolo espressioni)
**x8** | **s0/fp** | variabile locale di funzione / frame pointer (se in uso)
**x9**| **s1** | variabile locale di funzione
**x10-x11** |**a0 - a1**| valore restituito da funzione (di solito basta a0 - se serve si aggiunge a1)
**x12-x17**|**a2 - a7**| argomenti in ingresso a funzione (max 6 argomenti, gli eccedenti in stack)
**x18-x27**|**s2 - s11**| variabili locali di funzione (max 10 o 11 variabili, le eccedenti in pila)
**x28-x31**|**t3-t6**| valori temporanei (indirizzi, variabili globali e calcolo delle espressioni)

Ci sono poi 3 registri da 32 bit non referenziabili

**.** | Registri non referenziabili
---|---
**pc** | program counter
**hi** | Registr per moltiplicazioni e divisioni
**lo** | registro per moltiplicazioni e divisoni

>[!error]
Non confondere il registro con la [[memoria]]!
