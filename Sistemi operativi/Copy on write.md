---
alias: cow
---

Il meccanismo copy on write permette al sistema operativo di condividere pagine tra piú processi ad esempio a seguito di una `fork`.
Le page table dei processi punteranno alle stesse pagine, che però vengono inizialmente poste come a sola lettura. Quando evenutlamente si tenterà di accedere in scrittura verrà generata un interrupt dal sistema operativo per violazione della [[Protezione]]. 
Quando questo avviene la pagina specifica viene copiata, posta anche in scrittura (controllando che sia abilitata in scrittura la VMA) e le page table vengono aggiornate per indicare alla pagina specifica di ogni processo.