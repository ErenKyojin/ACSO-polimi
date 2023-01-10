Open: Testina che punta all'inizio del file.


- fd =open("F"): Associa il file descriptor di Fad fd,
	Ogni pagina 4096 byte, quindi se leggiamo da un file 4100 byte apriamo due pagine.

- lseek(fd, n)  porta indietro di n byte il file descriptor
- Read(fd, n) legge n byte successivi al file descriptor (spostando il file descriptor durante il processo)
- Write(fd, n) legge e scrive n byte successivi al file descriptor (spostando il file descriptor durante il processo)
- Close(fd) decrementa `f_count` e se è uguale a zero salva su disco le pagine sporche (le pagine rimangono in memoria ma perdono il dirty bit)