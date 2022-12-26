Spazio degli indirizzi più alti:

FFFF 8800 0000 0000 indirizzo virtuale corrispondente all'indrizzo base della memoria fisica.



## Struttura dello spazio di indirizzamento virtuale del kernel


| Area                             | costanti simboliche per indirizzi virtuali | Indirizzo iniziale  | dimensioni |
| -------------------------------- | ------------------------------------------ | ------------------- | ---------- | 
| Mappatura memoria fisica         | PAGE_OFFSET                                | FFFF 8800 0000 0000 | 64 TB      |
| Dati dinamici del kernel         | VMALLOC_START                              | FFFF C900 0000 0000 | 32TB       |
| Mappatura della memoria virtuale | VNEMMAP_START                              | FFFF EA00 0000 0000 | 1TB        |
| Moduli a caricamento dinamico    | MODULES_VADDR                              | FFFF FFFF A000 0000 | 1.5 GB     |
| Codice e dati                    | START_KERNEL_MAP                           | FFFF FFFF 8000 0000 | 0.5 GB     |



![[Mappatura della memoria fisica.canvas]]

Quindi la dimensionedell'area di mappatura dipende dalal dimensione della memoria fisica