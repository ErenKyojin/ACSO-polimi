Fino a quando c'è sufficiente [[memoria|RAM]] , linux alloca memoria fisica senza, praticamente, alcun controllo, mentre gli unici casi in cui la memoria è deallocata spontaneamente sono:
- Quando un processo termina [[exit]]
- Quando un processo rilascia la memoria
Quindi la memoria di linux tende ad aumentare continuamente


Se la memoria libera dovesse scendere sotto un livello critico ([[minFree]]) si attiva l'alogritmo [[PFRA]] che riporta il livello di memoria libera a [[maxFree]]


# [[PFRA]] e strategia di deallocazione

Gli interventi di deallocazione si svolgono applicando i seguenti tipi di azioni:
1. Le pagine di [[page cache]] non utilizzate dai processi, quindi con ref_count = 1 vengono deallocate, se non sufficente al raggiungimento di maxFree
2. Alcune pagine utilizzate dai processi vengono deallocate, se questo non è sufficiente al raggiungimento di maxFree
3. Un processo viene eliminato (killed)

Inoltre quando una pagina viene deallocata vengono svolte le seguenti operazioni:
- Se la pagina in memoria è stata letta da disco e non è stata mai modificata viene subito resa disponibile (perchè è già presente su disco)
- Se la pagine in memoria è stata modificata, e quindi il suo [[dirty bit]] è 1, prima di rendere la pagina disponibile deve essere scritta su disco.