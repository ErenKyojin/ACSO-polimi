La runqueue o lista dei processi pronti è un lista gestita dallo [[ ]]che contiene due campi:
- RB: lista di puntatori ai descrittori dei [[processo|processi]] pronti
- CURR: puntatore al descrittore del processo corrente

è un lista dinamica doppia circolare (double linked circular list) con elementi inseriti e rimossi dinamicamente, ogni processo in attesa invece ha la propria [[waitqueue]]
