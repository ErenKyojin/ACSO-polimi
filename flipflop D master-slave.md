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
\node[circle] (clock) at (-3,-0.85){CLK};
\node[] (mid) at (2,-3){};

%connections
%\draw (ANDa.out) |- (ORa.in 1);
\draw(Dms.pin 6) |- (Dsl.pin 1);
\draw (clock) to[] node[](A){} (Dms.pin 3);
\draw (A) to[short, *-*] (mid);
\draw (mid) |- (Dsl.pin 3);

\end{tikzpicture}
\end{document}
```
Slave trasparente su clock basso


Quindi $Q_{M}$ non cambia nell'intervallo basso del clock (Quando slave è in trasparenza)