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
>\node(CLK) at (-3,-1){CLK};
>\node (D3) at (-1.5,3){D3};
>\node (D2) at (1.5,3){D2};
>\node (D1) at (4.5,3){D1};
>\node (D0) at (7.5,3){D3};
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
>\end{tikzpicture}
>\end{document}
>```




## Registro parallelo con load
