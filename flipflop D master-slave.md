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
\node[latch] (ANDa) at (0,0){};
\node[latch] (ORa) at (4,0){};

%connections
%\draw (ANDa.out) |- (ORa.in 1);

\end{tikzpicture}
\end{document}
```
Slave trasparente su clock basso


Quindi $Q_{M}$ non cambia nell'intervallo basso del clock (Quando slave è in trasparenza)