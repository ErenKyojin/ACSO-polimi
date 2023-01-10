Open: Testina che punta all'inizio del file.

`f_count` conta il numero di file descriptor che puntano al file.

## singolo processo
- fd =open("F"): Associa il file descriptor di Fad fd,
	Ogni pagina 4096 byte, quindi se leggiamo da un file 4100 byte apriamo due pagine.

- lseek(fd, n)  porta indietro di n byte il file descriptor
- Read(fd, n) legge n byte successivi al file descriptor (spostando il file descriptor durante il processo)
- Write(fd, n) legge e scrive n byte successivi al file descriptor (spostando il file descriptor durante il processo)
- Close(fd) decrementa `f_count` e se è uguale a zero salva su disco le pagine sporche (le pagine rimangono in memoria ma perdono il dirty bit)

## Context switch
Se la fork avviene prima dell'apertura del file allora `f_count` è = 1, e rimane indipendente per i diversi processi, se invece la fork avviene dopo l'apertura `f_count` = 2 (vengono duplicate i descrittori dei file)
P fork e crea Q

#### contextswitch -> open 

- fd1 = Open("F") `//f_count = 1`
- contextSwitch("Q"), si caricano program counter e stack pointer
- fd2 = open("F") `//f_count = 1`

#### open -> contextSwitch
- fd1 = open("F") `//f_count = 1`
- Fork(Q) + contextSwitch(Q) `// duplica i descrittori dei file, f_count = 2`
- read(fd1)
- close(fd1) `//ref_count = 1`
- contextSwitch(Q)
- close(fd1) `//ref_count = 0`