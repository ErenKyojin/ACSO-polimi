# Buffer tri state

Circuito elementare modellabile come un contatto a $3$ posizioni:
In stato di bassa impedenza ha: 
- livello logico basso (0)
- livello logico alto (1)
- stato di alta [[impedenza]] (Z) che isola l'uscita elettricamente

Viene gestita

```tikz
\usepackage{circuitikz}
\usetikzlibrary{calc}

\begin{document}
\begin{tikzpicture}

\ctikzset{
logic ports/scale = 1,
logic ports/fill = darkgray,
}

%nodes
\node[buffer port] (ANDa) at (0,0){};

%connections

\end{tikzpicture}
\end{document}
```