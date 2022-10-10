# Half Adder

A | B | Cout |  Sum
--- | --- | --- | ---
0 | 0 | 0 | 0
0 | 1 | 0 | 1
1 | 0 | 0 | 1
1 | 1 | 1 | 0

$Sum = A \oplus B$
$Cout = AB$
Cout sta per carry out, ossia il resto.


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
\node[and port, xscale=-1] (ANDa) at (-2,-1){};
\node[xor port, rotate=270] (ORa) at (2,-4){};
\node (A) at (1.5,1){A};
\node (B) at (2.5,1){B};
\node (Acr) at (1.5,-1){};
\node (Bcr) at (2.5,-1){};
\node[left] (Cout) at (ANDa.out){Cout};
\node[below] (Sum) at (ORa.out){Sum};

%connections
\draw (A) |- (ORa.in 2);
\draw (B) |- (ORa.in 1);
\draw (Acr) |- (ANDa.in 1);
\draw (Bcr) |- (ANDa.in 2);


\end{tikzpicture}
\end{document}
```