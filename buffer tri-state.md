# Buffer tri state

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
\node (B) at (-3,2){};

%connections
\draw (B) to (ANDa.up);
\end{tikzpicture}
\end{document}
```