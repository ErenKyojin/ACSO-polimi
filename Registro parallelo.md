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
>Se usassimo dei bistabili sarebbero tutti paralleli

## Registro parallelo con load
