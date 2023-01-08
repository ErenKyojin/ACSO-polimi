


# Evento di fork
L'esecuzione di una fork() crea lo spazio virtuale della [[aree di memoria virtuale|VMA]] di Q ma le pagine virtuali presenti in memoria fisica sono tutte condivise tra i due processi, allora vengono inizialmente poste con il flag R, ossia Read-Only.
L'unica eccezzione è la pagina in cima alla pila (la pagina puntata dallo stack pointer) che viene duplicata e la nuova pagina viene attribuita al padre mentre la pagina fisica originale è attribuita al figlio.

Nel caso invece di scrittura di una pagina dati da parte di P si utilizza il meccanismo [[Copy on write|cow]]




## LRU
Nelle liste LRU le nuove pagine vengono poste all'inizio con flag ref uguale al padre