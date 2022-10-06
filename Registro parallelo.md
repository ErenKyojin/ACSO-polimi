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
>\node[flipflop D] (FFDa) at (0,0){};
>\node[flipflop D] (FFDb) at (3,0){};
>\node[flipflop D] (FFDb) at (6,0){};
>\node[flipflop D] (FFDb) at (9,0){};
>%connections
>
>\end{tikzpicture}
>\end{document}
>```