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
>\node (D3) at (0,0){D3};
>\node[flipflop D] (FFDa) at (0,0){};
>\node[flipflop D] (FFDb) at (3,0){};
>\node[flipflop D] (FFDc) at (6,0){};
>\node[flipflop D] (FFDd) at (9,0){};
>\node at (FFDa.bpin 3)[ocirc, left]{};
>\node at (FFDb.bpin 3)[ocirc, left]{};
>\node at (FFDc.bpin 3)[ocirc, left]{};
>\node at (FFDd.bpin 3)[ocirc, left]{};
>%connections
>
>\end{tikzpicture}
>\end{document}
>```




## Registro parallelo con load
