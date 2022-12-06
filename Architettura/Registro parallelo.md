# Registro parallelo

>[!esempio] Registro parallelo a 4 bit
>Composto da 4 [[flipflop D master-slave]]
>
>```tikz
\usepackage{circuitikz}
\usetikzlibrary{calc}
>
>\begin{document}
>\begin{tikzpicture}
>
>\ctikzset{
>logic ports/scale = 1,
>logic ports/fill = darkgray,
>}
>
>%nodes
>\node(CLK) at (-3,-2){CLK};
>\node (D3) at (-1.5,3){D3};
>\node (D2) at (1.5,3){D2};
>\node (D1) at (4.5,3){D1};
>\node (D0) at (7.5,3){D3};
>\node(Q3) at (1.5,2){Q3};
>\node(Q2) at (4.5,2){Q2};
>\node(Q1) at (7.5,2){Q1};
>\node(Q0) at (10.5,2){Q0};
>\node[flipflop D] (FFDa) at (0,0){};
>\node[flipflop D] (FFDb) at (3,0){};
>\node[flipflop D] (FFDc) at (6,0){};
>\node[flipflop D] (FFDd) at (9,0){};
>\node at (FFDa.bpin 3)[ocirc, left]{};
>\node at (FFDb.bpin 3)[ocirc, left]{};
>\node at (FFDc.bpin 3)[ocirc, left]{};
>\node at (FFDd.bpin 3)[ocirc, left]{};
>
>%connections
>\draw (D3) -| (FFDa.pin 1);
>\draw (D2) -| (FFDb.pin 1);
>\draw (D1) -| (FFDc.pin 1);
>\draw (D0) -| (FFDd.pin 1);
>
>\draw (CLK) -| (FFDa.pin 3);
>\draw (CLK) -| (FFDb.pin 3);
>\draw (CLK) -| (FFDc.pin 3);
>\draw (CLK) -| (FFDd.pin 3);
>
>\draw (FFDa.pin 6) |- (Q3);
>\draw (FFDb.pin 6) |- (Q2);
>\draw (FFDc.pin 6) |- (Q1);
>\draw[->] (FFDd.pin 6) |- (Q0);  
>\end{tikzpicture}
>\end{document}
>```


Sincroni sul fronte di discesa del [[clock]]

>[!oss]
>Se usassimo dei [[Bistabili]] D avremmo il problema della trasparenza, non potremmo garantire il comportamento corretto

## Registro parallelo con load

Registro parallelo ad $n$ bit con un comando di ingresso di caricamento, detto load.
- Se L è attivo, ossia se $L=1$, la parola in ingresso al registro viene memorizzata nel registro
- Altrimenti, se $L=0$, la parola in ingresso al registro viene ignorata e mantiene il suo stato

Il circuito è analogo a quello sopra ma con un ingresso selettore L (load) in più che, attraverso un MUX con le varie $D_{n}$ in ingresso, sceglie se far passare o meno $D_{n}$ nei flipflop.



## Registro a scorrimento a destra
Realizzato da
- $n \geq 1$ [[flipflop D master-slave]] a cascata:
- un ingresso seriale $S$
- $n \geq 1$ uscite parallele $Q_{0},\dots,Q_{n}$
- L'ingresso del clock

>[!esempio] Registro a scorrimento a 4 bit
>Composto da 4 [[flipflop D master-slave]]
>
>```tikz
\usepackage{circuitikz}
\usetikzlibrary{calc}
>
>\begin{document}
>\begin{tikzpicture}
>
>\ctikzset{
>logic ports/scale = 1,
>logic ports/fill = darkgray,
>}
>
>%nodes
>\node(CLK) at (-3,-2){CLK};
>\node (S) at (-1.5,3){S};
>\node(Q3) at (1.5,2){Q3};
>\node(Q2) at (4.5,2){Q2};
>\node(Q1) at (7.5,2){Q1};
>\node(Q0) at (10.5,2){Q0};
>\node[flipflop D] (FFDa) at (0,0){};
>\node[flipflop D] (FFDb) at (3,0){};
>\node[flipflop D] (FFDc) at (6,0){};
>\node[flipflop D] (FFDd) at (9,0){};
>\node at (FFDa.bpin 3)[ocirc, left]{};
>\node at (FFDb.bpin 3)[ocirc, left]{};
>\node at (FFDc.bpin 3)[ocirc, left]{};
>\node at (FFDd.bpin 3)[ocirc, left]{};
>
>%connections
>\draw (S) -| (FFDa.pin 1);
>\draw (CLK) -| (FFDa.pin 3);
>\draw (CLK) -| (FFDb.pin 3);
>\draw (CLK) -| (FFDc.pin 3);
>\draw (CLK) -| (FFDd.pin 3);
>
>\draw (FFDa.pin 6) |- (Q3);
>\draw (FFDb.pin 6) |- (Q2);
>\draw (FFDc.pin 6) |- (Q1);
>\draw[->] (FFDd.pin 6) |- (Q0);  
>
>\draw(FFDa.pin 6) |- (FFDb.pin 1);
>\draw(FFDb.pin 6) |- (FFDc.pin 1);
>\draw(FFDc.pin 6) |- (FFDd.pin 1);
>%\draw(FFDd.pin 6) |- (FFDb.pin 1);
>\end{tikzpicture}
>\end{document}
>```


## Altri registri:
- Registro a scorrimento a sinistra
- Registro a scorrimento universaleRegistro a scorrimento con funzione di caricamento
- Registro parallelo / a scorrimento universale
- Registro IN seriale / OUT seriale
- Registro IN parallelo / OUT seriale
- Registro IN parallelo / seriale OUT parallelo / seriale