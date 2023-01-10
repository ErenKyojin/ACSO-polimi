Open: Testina che punta all'inizio del file.


Ogni pagina 4096 byte, quindi se leggiamo da un file 4100 byte apriamo due pagine.

lseek(fd, n) torna indietro di n byte