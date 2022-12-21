Un volume è composto da una sequenza di blocchi logici  di dimensioni pari ad un multiplo di 512 B.
L'indirizzamento dei dati nel volume si basa sul conetto di Logical Block Address che può essere interpretato come l'indice del [[blocco]] nel volume.




# struttura di un volume


| Blocco di boot | Super block | lista [[i-node]] | blocchi dati |
| -------------- | ----------- | ---------------- | ------------ |
|                |             |                  |              |


- **Blocco 0 (o blocco di bootstrap**) cotnenuto tipicamente nle primo settore del disco, contiene il codice di inizializzazione del SO
- **Blocco 1 (o Superblock)** informazioni globali del file system
- **Lista degli i-node**: ogni elemento della lista è un i-node che contiene la lista degli indirizzi dei blocchi dati del file su disco
- **Blocchi di dati**: blocchi che contengono il contenuto dei file e dei direttori nel caso di una directory, il corrispondente blocco contiene una tabella con la lista di file / direttori nel vettore <nome file/nome_dir, i_node>

![[Esempio directory.canvas]]
| blocco di boot | Super blocco | i-node 6:  ... \| 800 \|... \|... </br>  i-node 10: ... \| 910 \|1040 \| ... | blk 800:</br> .\| 6 </br> .. \| 1 </br> f1 \| 10 </br> f2 \| 20 </br> sub_dir \| 40 |
| -------------- | ------------ | ------------------------------------- | ----------------------------------------------------------------------------------- |
|                |              |                                       |                                                                                     |
