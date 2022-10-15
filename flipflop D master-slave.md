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
\node[latch] (Dms) at (0,0){};
\node[latch] (Dsl) at (4,0){};
\node (clock) at (-3,Dms.pin 1){CLK};

%connections
%\draw (ANDa.out) |- (ORa.in 1);
\draw(Dms.pin 6) |- (Dsl.pin 1);
\draw (clock) -- (Dms.pin 3);

\end{tikzpicture}
\end{document}
```
Slave trasparente su clock basso


Quindi $Q_{M}$ non cambia nell'intervallo basso del clock (Quando slave è in trasparenza)