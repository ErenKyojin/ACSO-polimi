L'unità di propagazione è un'unità funzionale che prende come ingresso i registri nell'[[registri interstadio|registro interstadio]] MEM/EX e li compara coi registri in uscita sia da EX/MEM che da MEM/WB.

Se riscontra conflitti attiva uno o entrambi i segnali in uscita, chiamati:
- PropA: segnale di controllo del [[MUX]] in ingresso al primo operando dell'[[Unità aritmetico logica|ALU]], questo MUX sceglie se mandare in ingresso dal register file(in caso di assenza di collisioni), da EX/EX, o da MEM/EX, 
- PropB: segnale di controllo del MUX in ingresso al secondo operando dell'ALU (in realtà è in ingresso al MUX che sceglie se usare il secondo registro o l'immediato), il primo MUX si occupa di selezionare se mandare al secondo mux rs2, EX/EX rs2, o MEM/EX rs2


>[!TLDR] Tabella di output
>
>Output | sorgente | effetto
> --- | --- | ---
> PropA = 00 | ID/EX | Rs1 dal [[Register file]]
> PropA = 10 | EX/MEM | Rs1 dal ciclo precedente
> PropA = 01 | MEM/WB | Rs1 da due cicli precedenti
> PropB = 00 | ID/EX |Rs2 dal register file
> PropB = 10 | EX/MEM | Rs2 dal ciclo precedente
> PropB = 01 | MEM/WB | Rs2 da due cicli precedenti




